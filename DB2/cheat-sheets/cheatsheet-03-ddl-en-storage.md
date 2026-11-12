# Cheat Sheet 3: DDL, Constraints & PostgreSQL Fysieke Opslag (DB2)

> **Doel:** Kennis van geavanceerd constraintbeheer (`NOT VALID`, `DEFERRABLE`), page layouts van 8 kB, TOAST-architectuur, dead tuples, `VACUUM`, FSM en VM.

---

## 1. DDL Constraints & Beheer

### In-line vs. Out-of-line (Tabel) Constraints
* **In-line:** Direct achter het kolomtype (werkt enkel op die ene kolom).
* **Out-of-line (tabelniveau):** Onderaan de tabeldefinitie.
  * **Verplicht in 2 gevallen:**
    1. **Samengestelde sleutels:** (bv. `CONSTRAINT pk PRIMARY KEY (empno, proj_id)`).
    2. **Multi-column validaties:** (bv. `CONSTRAINT chk_datum CHECK (einddatum >= begindatum)`).

### Gedeeltelijk NULL Valkuil bij Samengestelde FK's
Als een samengestelde buitenlandse sleutel `(a, b)` gedeeltelijk `NULL` is (bv. `a = 3, b = NULL`), wordt de referentiële integriteitscontrole door SQL overgeslagen! De rij wordt ingevoegd, zelfs als `a = 3` niet bestaat in de parenttabel.
* **Oplossing via CHECK-constraint:**
  ```sql
  CONSTRAINT chk_fk_complete CHECK (
      (a IS NOT NULL AND b IS NOT NULL) OR 
      (a IS NULL AND b IS NULL)
  )
  ```

### Geavanceerd Constraintbeheer met `ALTER TABLE`
1. **`NOT VALID` en `VALIDATE CONSTRAINT`:**
   * Normaal: Het toevoegen van een constraint voert een trage, blokkerende scan uit over de hele tabel.
   * `NOT VALID`: Voegt de constraint toe **zonder bestaande rijen te scannen**. Nieuwe `INSERT`s en `UPDATE`s moeten er wel direct aan voldoen.
   * `VALIDATE CONSTRAINT`: Scant later op een rustig moment de bestaande data en maakt de constraint definitief.
   ```sql
   ALTER TABLE dept ADD CONSTRAINT chk_upper CHECK (dname = UPPER(dname)) NOT VALID;
   -- data opschonen...
   ALTER TABLE dept VALIDATE CONSTRAINT chk_upper;
   ```
2. **`DEFERRABLE INITIALLY DEFERRED`:**
   * Standaard (`NOT DEFERRABLE`): Validatie direct na **elk SQL-statement**.
   * `DEFERRABLE INITIALLY DEFERRED`: De validatie wordt uitgesteld tot de **`COMMIT`** van de transactie (kan geactiveerd worden via `SET CONSTRAINTS ... DEFERRED;`).
   * Ideaal bij wederzijdse/circulaire afhankelijkheden. Faalt de constraint bij de `COMMIT`, dan volgt een **automatische rollback**.
3. **`DISABLE TRIGGER ALL` (Noodoplossing):**
   * PostgreSQL heeft geen `DISABLE CONSTRAINT`. Je schakelt de achterliggende systeemtrigger uit (vereist superuser):
   ```sql
   ALTER TABLE emp DISABLE TRIGGER ALL;
   -- updates uitvoeren...
   ALTER TABLE emp ENABLE TRIGGER ALL;
   ```

### DROP TABLE regels
```sql
DROP TABLE tabelnaam [ RESTRICT | CASCADE ];
```
* **`RESTRICT` (standaard):** Weigert verwijdering als er views of foreign keys naar verwijzen.
* **`CASCADE`:** Verwijdert de tabel én verwijdert afhankelijke **views** volledig; bij buitenlandse sleutels verwijdert het **enkel de Foreign Key constraint** in de gekoppelde tabel (de gekoppelde tabel zelf blijft intact!).

---

## 2. Fysieke Opslagarchitectuur in PostgreSQL

### Datablokken (Pages)
* Vaste paginagrootte: standaard **8 kB (8192 bytes)**.
* **Gouden regel:** Een tuple (rij) mag in PostgreSQL **nooit** over meerdere pagina's heen lopen.
* **Page Layout:**
  * **Page Header:** Bevat metadata (`pd_lsn`, `pd_checksum`, `pd_lower`, `pd_upper`).
  * **Line Pointers:** Pointers die van boven naar beneden groeien en wijzen naar de fysieke startpositie van een tuple.
  * **Free Space:** Vrije ruimte tussen line pointers en heap tuples.
  * **Heap Tuples:** De feitelijke data, die vanaf de onderkant van de pagina naar boven groeit.

---

## 3. TOAST (The Oversized-Attribute Storage Technique)

Omdat een rij nooit groter mag zijn dan 8 kB, gebruikt PostgreSQL **TOAST** voor grote velden (`TEXT`, `VARCHAR`, `BYTEA`, `JSONB`).
* **Drempelwaarde:** Wordt geactiveerd zodra een tuple groter is dan **2 kB** (`toast_tuple_target`).
* **De 3 TOAST-stappen:**
  1. **Compressie:** Probeert eerst lange kolomwaarden inline te comprimeren (via pglz of lz4).
  2. **Out-of-line opslag:** Als de rij nog steeds te groot is, splitst TOAST de waarde in chunks van ~2 kB en slaat deze op in een aparte, gekoppelde **TOAST-tabel**.
  3. **Pointer:** In de originele tabelrij wordt de data vervangen door een compacte **18-byte pointer** die verwijst naar de chunks in de TOAST-tabel.
* **Voordeel:** Snelheid! Queries die het grote veld niet nodig hebben, kunnen gewone pagina's scannen zonder de zware TOAST-data in het geheugen te laden.

---

## 4. MVCC, Dead Tuples & VACUUM

* **Dead Tuples:** Bij een `UPDATE` of `DELETE` wordt de oude rijversie niet direct gewist van schijf, maar gemarkeerd als dood (nodig voor MVCC zodat andere actieve transacties de oude versie nog kunnen zien).
* **Probleem:** Opeenhoping van dead tuples leidt tot **tabel-bloat** (onnodig schijfverbruik en tragere scans).
* **`VACUUM`:**
  * Wist dead tuples fysiek uit de pagina's.
  * Herschikt tuples binnen pagina's om interne fragmentatie te herstellen.
  * Maakt ruimte vrij voor **nieuwe inserts in dezelfde tabel** (geeft de ruimte normaal niet terug aan het OS).
* **`VACUUM FULL`:** Herschrijft de hele tabel naar een nieuw compact bestand en geeft ruimte wél terug aan het OS (vereist een exclusieve tabel-lock!).
* **`autovacuum daemon`:** Draait continu op de achtergrond op basis van drempelwaarden.

---

## 5. De Vorken (Forks): FSM, VM & Tablespaces

Elke tabel heeft op schijf een hoofdbestand (`main`) en secundaire metadata-bestanden:

### Free Space Map (FSM)
* Houdt per pagina bij hoeveel vrije bytes er beschikbaar zijn.
* Gestructureerd als een **binaire boom van FSM-pagina's**.
* Zorgt ervoor dat nieuwe `INSERT`s direct een pagina met voldoende vrije ruimte vinden zonder de hele heap te scannen.

### Visibility Map (VM)
* Houdt voor elke heap-pagina 2 bits bij:
  * **Bit 0 (all-visible):** Bevat de pagina enkel tuples die voor alle transacties zichtbaar zijn (géén dead tuples)?
  * **Bit 1 (all-frozen):** Zijn alle tuples bevroren (ter preventie van transaction ID wraparound)?
* **Groot voordeel voor performance:**
  1. **Versnelt `VACUUM`:** Pagina's gemarkeerd als `1` (geen dead tuples) worden door `VACUUM` **volledig overgeslagen**!
  2. **Index-Only Scans:** Als de VM aangeeft dat de pagina `all-visible` is, hoeft de database de heap niet meer te controleren om de zichtbaarheid van rijen te verifiëren.

### Tablespaces
* Koppelt een logische naam aan een fysiek pad op de server (bv. `/mnt/fast_nvme/`).
* **Toepassing:** DBA kan intensief geraadpleegde tabellen of indexen op snelle SSD's plaatsen en historische archieftabellen op trage HDD's (`CREATE TABLE ... TABLESPACE fastspace;`).
* Standaard tablespaces: `pg_default` (voor gebruikersdata) en `pg_global` (voor gedeelde systeemcatalogi).
