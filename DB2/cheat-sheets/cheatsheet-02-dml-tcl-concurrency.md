# Cheat Sheet 2: DML, Transacties, TCL & Concurrency (DB2)

> **Doel:** Foutloos antwoorden op vragen rond transactiegrenzen, savepoints, ACID-eigenschappen, SQL-isolatieniveaus in PostgreSQL, locks en deadlocks.

---

## 1. DML & Integriteitsbeperkingen
DML manipuleert data: `INSERT`, `UPDATE`, `DELETE`, `TRUNCATE`.
* **TRUNCATE vs DELETE:** `TRUNCATE` wist de hele tabel direct op schijf en geeft blokken onmiddellijk vrij zonder MVCC dead tuples achter te laten (`VACUUM` is niet nodig).
* **Referentiële Integriteit acties bij DELETE/UPDATE van parent record:**
  * `RESTRICT` / `NO ACTION` (standaard): Weigert verwijdering als er nog child-records naar verwijzen.
  * `CASCADE`: Verwijdert automatisch alle gekoppelde rijen in de kindtabel.
  * `SET NULL`: Zet de foreign key waarden in de kindtabel op `NULL` (alleen mogelijk als de foreign key géén `NOT NULL` heeft).

---

## 2. Transactiebeheer (TCL) & ACID
Een transactie is een logische eenheid van bewerkingen die gezamenlijk slagen of falen:
* **A - Atomicity (Atomiciteit):** Alles of niets. Geen half uitgevoerde transacties.
* **C - Consistency (Consistentie):** De database gaat van één geldige toestand over naar een andere; alle constraints blijven gerespecteerd.
* **I - Isolation (Isolatie):** Transacties hebben geen last van elkaars tussenresultaten (lijkt alsof ze sequentieel draaien).
* **D - Durability (Duurzaamheid):** Na een `COMMIT` zijn wijzigingen permanent opgeslagen en bestand tegen crashes/stroomuitval (door WAL/Write Ahead Logging).

### Start en Einde van een transactie
* **Start:**
  * Expliciet via `BEGIN;` (of `START TRANSACTION;`).
  * Impliciet: Het eerste statement na een vorige commit/rollback in een sessie.
* **Einde:**
  * Expliciet: `COMMIT;` (wijzigingen definitief) of `ROLLBACK;` (alles ongedaan maken).
  * Impliciet: Normale sessiebeëindiging $\rightarrow$ `COMMIT;`. Abnormale crash/verbinding verbroken $\rightarrow$ `ROLLBACK;`.
* **PostgreSQL-valkuil bij DDL:** In PostgreSQL veroorzaakt DDL (`CREATE TABLE`, `ALTER TABLE`, `DROP`) **géén** impliciete commit! DDL is volledig transactioneel en kan binnen een transactie worden teruggerold met `ROLLBACK;`.

---

## 3. Savepoints & Rollbacks

Een savepoint is een tijdelijk markeerpunt binnen een lopende transactie.

```sql
BEGIN;
UPDATE emp SET sal = 2000 WHERE ename = 'BLAKE';
SAVEPOINT sp_blake;

UPDATE emp SET sal = 1500 WHERE ename = 'CLARK';
SAVEPOINT sp_clark;

UPDATE emp SET sal = 1800 WHERE ename = 'JONES';

-- Terugrollen naar het eerste savepoint:
ROLLBACK TO SAVEPOINT sp_blake;
-- Wijzigingen aan CLARK en JONES zijn ongedaan gemaakt; BLAKE blijft 2000!

COMMIT;
```

> ⚠️ **De Savepoint Vernietigingsvalkuil (Examenvraag!):**
> Zodra je terugrolt naar een eerder savepoint (`ROLLBACK TO SAVEPOINT sp_blake`), worden **alle latere savepoints (zoals `sp_clark`) automatisch vernietigd**.
> Voer je daarna alsnog `ROLLBACK TO SAVEPOINT sp_clark;` uit, dan leidt dit tot een **foutmelding** (`ERROR: savepoint "sp_clark" does not exist`) en wordt de **volledige transactie geaborteerd**!

---

## 4. Concurrency Anomalieën (Data-afwijkingen)
Treden op wanneer meerdere sessies gelijktijdig dezelfde rijen benaderen:
1. **Dirty Read:** Transactie A leest wijzigingen van Transactie B die nog **niet** zijn gecommit. (Als B een rollback doet, heeft A "spookdata" gelezen).
2. **Non-repeatable Read:** Transactie A leest een rij, Transactie B wijzigt (`UPDATE`) of verwijdert (`DELETE`) die rij en commit. Transactie A leest dezelfde rij opnieuw en ziet andere waarden.
3. **Phantom Read:** Transactie A voert een SELECT uit over een bereik (`WHERE sal > 2000`). Transactie B voegt een nieuwe rij toe (`INSERT`) die binnen dat bereik valt en commit. Transactie A voert dezelfde query opnieuw uit en ziet ineens extra rijen.

---

## 5. SQL Isolatieniveaus in PostgreSQL

PostgreSQL garandeert standaard leesconsistentie op **statement-niveau** (`READ COMMITTED`).

```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ; -- of SERIALIZABLE / READ COMMITTED
```

| Isolatieniveau | Dirty Read | Non-repeatable Read | Phantom Read |
| :--- | :---: | :---: | :---: |
| **Read Uncommitted** | Voorkomen *(in PG)* | Mogelijk | Mogelijk |
| **Read Committed** *(standaard)* | Voorkomen | Mogelijk | Mogelijk |
| **Repeatable Read** | Voorkomen | Voorkomen | Voorkomen *(in PG)* |
| **Serializable** | Voorkomen | Voorkomen | Voorkomen |

### Cruciale PostgreSQL eigenschappen:
* **Dirty Read is NOOIT mogelijk in PostgreSQL:** `READ UNCOMMITTED` bestaat niet echt als apart mechanisme en wordt intern stilzwijgend uitgevoerd als `READ COMMITTED`.
* **Repeatable Read in PostgreSQL:** 
  * Maakt een snapshot op het moment dat de **allereerste query** binnen de transactie wordt uitgevoerd.
  * Voorkomt in PostgreSQL óók Phantom Reads!
  * **Conflict-regel:** Als twee transacties in `REPEATABLE READ` proberen dezelfde rij te updaten, krijgt de tweede transactie direct een error (`could not serialize access due to concurrent update`) en moet deze opnieuw starten.
* **Serializable:** Garandeert een strikte seriële volgorde (alsof transacties één voor één achter elkaar draaien) via SSI (Serializable Snapshot Isolation).

---

## 6. Locking & Deadlocks

* **Impliciete row locks:** Elk `UPDATE`- of `DELETE`-statement vergrendelt automatisch de getroffen rijen. Andere lezers worden niet geblokkeerd (zien de oude staat via MVCC), maar concurrerende schrijvers moeten wachten.
* **Expliciet vergrendelen (`SELECT ... FOR UPDATE`):**
  ```sql
  -- Vergrendelt de rij voor komende updates in dezelfde transactie:
  SELECT sal FROM emp WHERE empno = 7566 FOR UPDATE;

  -- Met NOWAIT: geeft direct een error als de rij al gelockt is i.p.v. te blokkeren:
  SELECT sal FROM emp WHERE empno = 7566 FOR UPDATE NOWAIT;

  -- Vergrendel enkel een specifieke tabel in een join:
  SELECT * FROM emp e JOIN dept d ON e.deptno = d.deptno FOR UPDATE OF e;
  ```
* **Deadlock:**
  * Situatie waarin Transactie 1 wacht op een lock van Transactie 2, en Transactie 2 tegelijkertijd wacht op een lock van Transactie 1 (wederzijdse blokkade).
  * **Oplossing door PostgreSQL:** Na een time-out (`deadlock_timeout`, standaard 1 seconde) detecteert het DBMS de kringloop en **breekt automatisch één van de transacties af met een rollback**, zodat de andere kan doorgaan.
