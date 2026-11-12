# DML 
DML bevat instructies om de inhoud van de tabellen te wijzigen: 
- INSERT 
- UPDATE 
- DELETE 
- TRUNCATE 

Mogelijke uitdagingen bij multi-user toegang: 
- **Data Concurrency:** Meerdere gebruikers proberen gelijktijdig dezelfde gegevens te raadplegen of wijzigen. 
- **Data Consistency:** De database bevat geen tegenstrijdigheden; gebruikers zien een consistente staat (eigen wijzigingen zijn direct zichtbaar; wijzigingen van anderen pas nadat ze gecommit zijn). 
- **Data Integriteit:** Het DBMS valideert voortdurend of alle regels en constraints (PRIMARY KEY, FOREIGN KEY, CHECK) gerespecteerd blijven. 
--- 
# TCL (Transaction Control Language) Een transactie is een logische eenheid van bewerkingen die voldoet aan **ACID** (Atomicity, Consistency, Isolation, Durability). 
## Wanneer start en eindigt een transactie? 
### Start: 
- Expliciet met de instructie `BEGIN;` (of `START TRANSACTION;`). 
- Zodra de eerste SQL-instructie wordt uitgevoerd na een vorige `COMMIT` of `ROLLBACK`. 
### Einde: 
- **COMMIT:** Maakt alle wijzigingen sinds het begin van de transactie permanent. 
- **ROLLBACK:** Maakt alle wijzigingen sinds het begin ongedaan. - **Impliciete beëindiging:** 
- Normaal afsluiten van de sessie $\rightarrow$ automatische \`COMMIT\`. 
- Abnormaal afsluiten / crash / verbindingsverlies $\rightarrow$ automatische `ROLLBACK`.
- **PostgreSQL-uitzondering bij DDL:** In de meeste RDBMS'en veroorzaakt DDL (`CREATE`, `ALTER`, `DROP`) een automatische impliciete commit. **In PostgreSQL niet!** DDL is in PostgreSQL transactioneel en kan dus gewoon via `ROLLBACK` worden teruggedraaid. 
--- 
## Savepoints Met een savepoint rol je een transactie gedeeltelijk terug zonder eerdere stappen te verliezen: 
```sql BEGIN; UPDATE emp SET sal = 2000 WHERE ename = 'BLAKE'; SAVEPOINT sal_blake; UPDATE emp SET sal = 1500 WHERE ename = 'CLARK'; SAVEPOINT sal_clark; 
-- Terugrollen naar het eerste savepoint: 
ROLLBACK TO SAVEPOINT 
sal_blake; 
-- Salaris van CLARK is ongedaan gemaakt; wijziging van BLAKE blijft behouden!
```

## anomalieen
- **Dirty read**
	- Wijzigingen van een andere transactie zijn nog niet gecommit en je ziet de oude commits nog
- **Non-repeatable read**
	- Twee keer hetzelfde record lezen in één transactie levert een andere waarde op omdat iemand anders tussendoor een `UPDATE` of `DELETE` heeft gecommit;
- **Phantom Read** 
	- Twee keer een query uitvoeren over een bereik levert ineens méér (of minder) rijen op omdat iemand anders tussendoor nieuwe rijen heeft ge-`INSERT` en gecommit


## SQL Isolatieniveaus & PostgreSQL 

Gedrag Standaard garandeert PostgreSQL leesconsistentie op **statement-niveau** via `READ COMMITTED` (elke query ziet data van het begin van die specifieke query). Op **transactieniveau** moet je dit zelf instellen: ```sql SET TRANSACTION ISOLATION LEVEL REPEATABLE READ; -- of READ COMMITTED / SERIALIZABLE```
### Hoe ga je dit tegen?

In postgres doe je dit via 
```sql
BEGIN TRANSACTION ISOLATION LEVEL REPEATABLE READ; -- of SERIALIZABLE
```

postgres maakt het onmogelijk voor dirty reads want als je ```sql READ UNCOMMITED``` doet dan maakt postgres daar automatisch ```sql READ COMMITED``` van


## Wanneer start je een transactie

- BEGIN instructie start de sessie
- Na een COMMIT of een ROLLBACK 
	- COMMIT maakt de verandering defenitief 
	- ROLLBACK maakt de instructie ongedaan tot de laatst gegeven COMMIT 
- DDL instruction  (CREATE, ALTER, DROP)
	- impliciet commit in de meeste databanken **maar niet in POSTGRES**
	- daar kan een CREATE TABLE alleen mar teruggezet worden via ROLLBACK binnen een transactie
- after a DCL instruction (GRANT, REVOKE)
	- impliciete commit

## Wanneer eindigt een transactie

- in geval van een expleciete COMMIT of ROLLBACK
- in geval van een impliciete COMMIT of ROLLBACK als resultaat van een speciale DDL instructie
- in geval van impliciete COMMIT als resultaat van een DCL transactie 
- bij het einde van een sessie 
- bij een onjuiste beeindiging van een sessie (computer faalt)
