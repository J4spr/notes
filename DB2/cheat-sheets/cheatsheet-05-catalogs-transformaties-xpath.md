# Cheat Sheet 5: System Catalogs, ETL & XML/XPath Transformaties (DB2)

> **Doel:** Direct het verschil kunnen uitleggen tussen System Views en het Information Schema, en foutloze XPath-expressies en transformatielogica opstellen.

---

## 1. Systeemmetadata: System Catalogs vs. Information Schema

PostgreSQL biedt twee manieren om metadata op te vragen over tabellen, kolommen, indexen en prestaties:

| Kenmerk | System Catalogs & Views | Information Schema |
| :--- | :--- | :--- |
| **Definitie** | PostgreSQL-eigen tabellen (in schema `pg_catalog`, bv. `pg_class`, `pg_stat_user_tables`). | ANSI SQL-gestandaardiseerde verzameling read-only views (in schema `information_schema`). |
| **Portabiliteit** | **Niet overdraagbaar.** Specifiek ontworpen voor PostgreSQL. | **Zeer overdraagbaar.** Werkt met dezelfde syntax en kolomnamen in Oracle, MySQL, SQL Server, etc. |
| **Detailniveau** | Biedt diepgaande interne motordetails: fysieke schijflocaties, buffer-hits, lock-status, TOAST-statistieken en OID's. | Biedt algemene relationele metadata (tabelnamen, datatypes, constraint-namen). |
| **Prestatiegegevens** | Bevat realtime statistieken (bv. `seq_scan`, `idx_scan`, aantal `n_dead_tup`). | Bevat **géén** prestatie- of bufferstatistieken. |

### Belangrijke System Views om te Herkennen:
* **`pg_stat_user_tables`:** Toont het aantal sequentiële scans (`seq_scan`), index-scans (`idx_scan`), live tuples (`n_live_tup`) en dead tuples (`n_dead_tup`).
* **`pg_statio_user_indexes`:** Toont hoeveel blokken uit RAM (`idx_blks_hit`) vs. van schijf (`idx_blks_read`) zijn gelezen via indexen.
* **`pg_stat_activity`:** Toont actieve gebruikerssessies, hun backend PID en huidige lopende query (handig om vastgelopen queries op te sporen).
* **`pg_class`:** De centrale catalogustabel die tabellen, indexen, sequences en views beschrijft (met o.a. `relpages` en `reltuples`).

---

## 2. ETL (Extract, Transform, Load) Principes

Data-integratie tussen diverse heterogene systemen verloopt volgens het ETL-proces:
1. **Extract (Extraheren):** Ophalen van brondata uit verschillende bronnen (SQL databases, platte CSV-bestanden, ERP-systemen, REST API's).
2. **Transform (Transformeren):**
   * *Data Cleaning:* Opschonen van ongeldige data, omgaan met ontbrekende waarden.
   * *Harmonisatie:* Oplossen van synoniemen en homoniemen, datumnotaties uniform maken (bv. `DD/MM/YYYY` $\rightarrow$ `YYYY-MM-DD`).
   * *Validatie & Verrijking:* Toepassen van bedrijfsregels, toevoegen van berekende kolommen of lookup-codes.
3. **Load (Laden):** Wegschrijven van de getransformeerde data naar het doel-datawarehouse of operationele database.
* **Staging Area:** Een tussenliggende tijdelijke opslagruimte waar data wordt geparkeerd tijdens de extractie voordat zware transformaties draaien, om bronsystemen zo min mogelijk te belasten.

---

## 3. XML & XPath Cheat Sheet

XPath (XML Path Language) navigeert door de knooppunten (nodes) van een XML-document.

### Belangrijkste Pad-operatoren:
* `/` : Selecteert vanaf de root-node (absoluut pad), of directe afstammeling (kind).
* `//` : Selecteert knooppunten overal in het document (ongeacht het diepteniveau).
* `.` : Het huidige knooppunt.
* `..` : Het ouderknooppunt (parent).
* `@` : Selecteert een **attribuut** in plaats van een element (bv. `@id`).
* `*` : Wildcard voor elk willekeurig element.
* `@*` : Wildcard voor elk willekeurig attribuut.

### Predikaten (Filters met `[...]`):
Predikaten filteren knooppunten op positie of inhoud (equivalent aan SQL `WHERE`):

```xpath
-- Eerste student selecteren:
/school/students/student[1]

-- Laatste cursus selecteren:
//course[last()]

-- Cursussen met jaar gelijk aan 2 (waarbij year een kind-element is):
//course[year='2']/title

-- Cursussen met jaar gelijk aan 2 (waarbij year een attribuut is van <course>):
//course[@year='2']/title

-- Cursussen met studiepunten groter dan 5:
//course[credits > 5]/title

-- Meerdere voorwaarden combineren (AND / OR):
//course[@year='2' and credits >= 6]/title
```

### Handige XPath Functies:
* `text()` : Haalt enkel de tekstinhoud van een knooppunt op (zonder tags): `//course/title/text()`.
* `count(...)` : Telt het aantal voorkomens: `count(//course)`.
* `contains(string, substring)` : Controleert op deeltekst: `//course[contains(title, 'Data')]`.
* `starts-with(string, substring)` : Controleert of string begint met: `//student[starts-with(@id, 'S')]`.

---

## 4. JSON Structuren

* **JSON Object (`{ ... }`):** Ongeordende verzameling van `sleutel : waarde` paren, gescheiden door komma's.
  ```json
  {
    "course_id": "DB2",
    "name": "Databanken 2",
    "credits": 6,
    "active": true
  }
  ```
* **JSON Array (`[ ... ]`):** Geordende lijst van waarden (kunnen primitieven of geneste objecten zijn).
  ```json
  [
    {"id": 1, "city": "Brussel"},
    {"id": 2, "city": "Antwerpen"}
  ]
  ```
* **PostgreSQL JSON types:**
  * `JSON`: Slaat ruwe JSON-tekst exact op (inclusief spaties en volgorde); moet bij elke query opnieuw geparsed worden.
  * `JSONB`: Slaat JSON binair en gedecompresseerd op. Veel sneller te bevragen en ondersteunt **GIN-indexen**.
