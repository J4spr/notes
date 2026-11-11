# DML

DML bevat instructies om de inhoud van de tabellen te wijzigen

- INSERT
- UPDATE
- DELETE 
- TRUNCATE

mogelijke problemen:
- Data Concurrency 
	- meerdere gebruikers proberen tegelijkertijd de inhoud van tabellen te wijzigen
- Data Consitency
	- de database mag geen tegenstrijdigheden bevatten 
	- elke gebruiker ziet een consistent beeld van de gegevens
		- wijzigingen in zijn eigen transactie zijn zichtbaar evenals die van andere gebruikers
- Data integriteit
	- DBMS moet nagaan of alle constraints gevalideerd zijn

---
# TCL 

## Savepoints 

Met een savepoint kan je een transactie gedeeltelijk terugdraaien

```sql
BEGIN;
UPDATE emp SET sal = 2000 WHERE ename = 'BLAKE'; 
SAVEPOINT sal_blake;

UPDATE emp SET sal = 1500 WHERE ename = 'CLARK';
SAVEPOINT sal_clark;
-- Terugrollen naar het eerste savepoint:
ROLLBACK TO SAVEPOINT sal_blake;
-- Salaris van CLARK wordt teruggedraaid, maar BLAKE blijft 2000!
```

## anomalieen
- **Dirty read**
	- Wijzigingen van een andere transactie zijn nog niet gecommit en je ziet de oude commits nog
- **Non-repeatable read**
	- Twee keer hetzelfde record lezen in één transactie levert een andere waarde op omdat iemand anders tussendoor een `UPDATE` of `DELETE` heeft gecommit;
- **Phantom Read** 
	- Twee keer een query uitvoeren over een bereik levert ineens méér (of minder) rijen op omdat iemand anders tussendoor nieuwe rijen heeft ge-`INSERT` en gecommit


## SQL Isolatieniveaus & PostgreSQL 

Gedrag Standaard garandeert PostgreSQL leesconsistentie op **statement-niveau** via `READ COMMITTED` (elke query ziet data van het begin van die specifieke query). Op **transactieniveau** moet je dit zelf instellen: ```sql SET TRANSACTION ISOLATION LEVEL REPEATABLE READ; -- of READ COMMITTED / SERIALIZABLE
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
- 
