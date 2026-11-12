# Cheat Sheet 4: Optimizer, EXPLAIN & Performance Tuning (DB2)

> **Doel:** EXPLAIN plannen binnen 30 seconden lezen en begrijpen, de juiste scan- en join-algoritmes herkennen en weten hoe de database-optimizer keuzes maakt.

---

## 1. De Levenscyclus van een SQL-Query

Een query doorloopt 5 fasen in de PostgreSQL-engine:
1. **Parser:** Controleert de SQL-syntax en bouwt een parse-tree.
2. **Analyzer:** Controleert de semantiek tegen de systeemcatalogus (bestaan de tabellen en kolommen? Heeft de gebruiker rechten?) $\rightarrow$ produceert een query tree.
3. **Rewriter:** Past rewrite-regels en view-definities toe.
4. **Planner / Optimizer:** Berekent de kosten (`cost`) van verschillende uitvoeringspaden en selecteert het goedkoopste plan.
5. **Executor:** Voert de geselecteerde stappen top-down uit en retourneert de data.

---

## 2. EXPLAIN Output Interpreteren

### Syntax
```sql
EXPLAIN SELECT ...;                           -- Toont enkel geschatte kosten
EXPLAIN ANALYZE SELECT ...;                   -- Voert de query effectief uit en toont werkelijke tijden
EXPLAIN (ANALYZE, BUFFERS) SELECT ...;        -- Toont ook buffer hits/reads (8 kB blokken)
```

### De Structuur van een Plan Node
```text
Hash Join (cost=21.19..32.98 rows=157 width=266) (actual time=0.048..0.052 rows=7 loops=1)
```
* **Geschatte kosten (`cost=21.19..32.98`):**
  * `21.19` = **Start-up cost:** De geschatte I/O en CPU-tijd voordat de eerste rij kan worden teruggegeven.
  * `32.98` = **Total cost:** De geschatte tijd om alle rijen op te halen.
* **`rows=157`:** Het geschatte aantal rijen dat deze stap oplevert.
* **`width=266`:** De geschatte gemiddelde breedte van een resultaatrij in bytes.
* **Werkelijke cijfers (`actual` bij ANALYZE):**
  * `actual time=0.048..0.052` = Werkelijke start-up en totale tijd in **milliseconden**.
  * `rows=7` = Werkelijk aantal opgehaalde rijen.
  * `loops=1` = Hoe vaak deze specifieke node is uitgevoerd (bij bv. Nested Loops kan dit veel hoger zijn; totale tijd = `time * loops`!).
* **Buffers:**
  * `shared hit=4`: 4 blokken van 8 kB rechtstreeks uit het RAM-geheugen (`shared_buffers`) gelezen (zeer snel).
  * `shared read=2`: 2 blokken fysiek van de schijf moeten inlezen (trager).

---

## 3. Scan Algoritmes (Hoe leest het DBMS data?)

| Scan Methode | Hoe het werkt | Wanneer gekozen door Optimizer? |
| :--- | :--- | :--- |
| **Sequential Scan (`Seq Scan`)** | Leest alle 8 kB-pagina's van de heap van begin tot eind sequentieel. | Kleine tabellen, queries zonder `WHERE`, of queries die een groot percentage (>10-20%) van de tabel nodig hebben. |
| **Index Scan** | Navigeert door de B-tree index naar de sleutelwaarde, haalt de rijpointer (`TID`) op en leest daarna de bijbehorende pagina uit de heap. | Zeer selectieve queries (weinig rijen resultaat) met een index op de filterkolom. |
| **Index Only Scan** | Leest **enkel** de indexpagina's; de heap wordt niet geraadpleegd omdat alle benodigde kolommen al in de index zitten en de Visibility Map aangeeft dat pagina's `all-visible` zijn. | Bijzonder efficiënt wanneer de query alleen geïndexeerde kolommen selecteert. |
| **Bitmap Index Scan + Bitmap Heap Scan** | 1. `Bitmap Index Scan`: Leest de index en bouwt in het geheugen een bitmap van relevante paginanummers en offsets.<br>2. `Bitmap Heap Scan`: Leest die pagina's in fysieke volgorde van schijf. | Middelgrote resultaatsets, of bij het combineren van meerdere indexen met `AND`/`OR`. Voorkomt willekeurige I/O. |
| **TID Scan** | Haalt een record direct op via zijn fysieke Tuple ID: `ctid = '(bloknr, offset)'`. | Enkel wanneer `ctid` expliciet in de query staat. |

---

## 4. Join Algoritmes (Hoe combineert het DBMS tabellen?)

| Join Algoritme | Werking | Geschikt voor | Beperkingen |
| :--- | :--- | :--- | :--- |
| **Nested Loop Join** | Voor elke rij in de buitenste tabel scant hij de binnenste tabel (eventueel via een index). | Eén zeer kleine buitentabel en een geïndexeerde binnentabel. | Zeer traag bij twee grote tabellen zonder bruikbare index. |
| **Hash Join** | **Fase 1 (Build):** Bouwt een in-memory hashtabel van de kleinste tabel.<br>**Fase 2 (Probe):** Scant de grotere buitentabel en hasht de sleutel om matches direct op te zoeken. | Grote, ongeordende tabellen. | Werkt **alleen met gelijkheid (`=`)** als join-conditie. Vereist voldoende `work_mem`. |
| **Merge Join (Sort-Merge)** | Sorteert beide tabellen op de join-sleutel (indien nog niet gesorteerd) en loopt er synchroon doorheen om overeenkomsten te mergen. | Grote tabellen die al gesorteerd zijn (bv. door een B-tree index) of wanneer de output gesorteerd moet zijn. | Werkt alleen met `=`, vereist sorteerstappen als er geen index is. |

---

## 5. Aggregatie Algoritmes (`GROUP BY`)

1. **`HashAggregate`:**
   * Bouwt een hashtabel in het geheugen (`work_mem`) met de `GROUP BY`-sleutel als hash-key.
   * Terwijl de tabel wordt gescand, worden aggregatiewaarden (`COUNT`, `SUM`) direct geüpdatet.
   * Zeer snel voor ongeordende data zolang de hashtabel in het RAM past.
2. **`GroupAggregate`:**
   * Vereist dat de invoer **vooraf gesorteerd** is op de groeperingssleutel.
   * Scant sequentieel door de gesorteerde rijen en berekent de aggregaten zodra de groepswaarde omslaat.

---

## 6. Index Types in PostgreSQL

* **B-Tree (standaard):** Meest universeel; ondersteunt `=`, `<`, `<=`, `>`, `>=`, `BETWEEN`, `IN`.
* **Hash:** Enkel voor exacte gelijkheid (`=`); iets compacter dan B-Tree maar minder veelzijdig.
* **BRIN (Block Range Index):** Slaat enkel min/max waarden op per blokreeks. Extreem klein. Ideaal voor gigantische, chronologisch oplopende data (bv. sensor logs, tijdstempels).
* **GIN (Generalized Inverted Index):** Slaat elementen op die verwijzen naar meerdere rijen. Ideaal voor arrays, `JSONB` en Full Text Search (`tsvector`).
* **GiST (Generalized Search Tree):** Voor geometrische/ruimtelijke data (PostGIS) en netwerkbereiken.

---

## 7. Write Ahead Log (WAL) & Crash Recovery
* **Werking:** Wijzigingen worden **eerst** sequentieel weggeschreven naar het WAL-bestand op schijf voordat de gewijzigde datapagina's in de `shared_buffers` naar de databestanden worden geflusht.
* **Noodzaak (Durability):** Bij een stroomuitval of crash kan PostgreSQL de database herstellen door het logboek opnieuw af te spelen (**REDO**).
* **Checkpoint:** Periodiek proces dat alle 'vuile' pagina's uit het geheugen naar schijf schrijft en een veilig herstelpunt in het WAL markeert.
