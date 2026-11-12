# Hoofdstuk 4: DDL (Data Definition Language) & Fysieke Opslag 
DDL bevat instructies om databasestructuren (tabellen, indexen, views, sequences) aan te maken, te wijzigen of te verwijderen: 
- `CREATE` 
- `ALTER` 
- `DROP` 
- *(Let op: In PostgreSQL kan DDL binnen een transactie draaien en met `ROLLBACK` worden teruggedraaid!)* 
--- 
## 1. Constraints (Beperkingen)
Constraints waarborgen de data-integriteit (sleutel-, entiteits- en referentiële integriteit). 
### In-line (kolomniveau) vs. Out-of-line (tabelniveau) 
- **In-line constraint:** Wordt direct achter de kolomdefinitie geplaatst (werkt enkel op die specifieke kolom). 
- **Out-of-line (tabel) constraint:** Wordt onderaan de tabeldefinitie geplaatst. 
- **Verplicht bij:** 
	1. **Samengestelde sleutels** (Composite Primary Key of Composite Foreign Key bestaande uit meerdere kolommen). 
	2. **Checks over meerdere kolommen** (bv. `CHECK (einddatum >= begindatum)`).
```sql 
CREATE TABLE project_toewijzing ( empno NUMERIC(4), project_id NUMERIC(4), begindatum DATE, einddatum DATE, 
-- Out-of-line constraints: 
CONSTRAINT pk_proj PRIMARY KEY (empno, project_id), 
CONSTRAINT fk_proj_emp FOREIGN KEY (empno) REFERENCES emp(empno) ON DELETE CASCADE,
CONSTRAINT chk_data CHECK (einddatum >= begindatum) );
```

- **Soorten integriteit:** 
- *Sleutel- en entiteitsintegriteit:* `PRIMARY KEY` (uniek + niet-null). 
- *Referentiële integriteit:* `FOREIGN KEY` (verwijst naar bestaande PK of is NULL; acties: RESTRICT, CASCADE, SET NULL). 
- *Domeinintegriteit:* `CHECK` en `NOT NULL`. 
- *Uniekheid:* `UNIQUE`.
- **In-line vs. Out-of-line:** 
	- *In-line:* Direct achter de kolomdefinitie (enkelvoudige kolom). 
	- *Out-of-line:* Onderaan de tabel. Verplicht bij samengestelde sleutels (`PRIMARY KEY (col1, col2)`) en checks over meerdere kolommen (`CHECK (col2 >= col1)`). 
- **Gedeeltelijke NULL-valkuil bij FK:** 
	- Bevat een samengestelde FK deels NULL (bv. `(3, NULL)`), dan faalt de controle niet! 
	- Oplossen met: `CHECK ((a IS NOT NULL AND b IS NOT NULL) OR (a IS NULL AND b IS NULL))`. 
- **ALTER TABLE Geavanceerd:** 
	- `ADD CONSTRAINT ... NOT VALID`: Voegt CHECK of FK toe zonder bestaande data te scannen. Valideert enkel nieuwe bewerkingen. 
	- `VALIDATE CONSTRAINT naam`: Scant bestaande data achteraf alsnog. 
	- `DEFERRABLE INITIALLY DEFERRED`: Stelt FK/UNIQUE checks uit tot aan de `COMMIT` (via `SET CONSTRAINTS`). Faalt de check bij commit -> automatische ROLLBACK. 
	- `DISABLE TRIGGER ALL`: Noodgreep om FK-controles tijdelijk uit te schakelen (vereist superuser).
---
# DROP TABLE

DROP TABLE verwijderd alle informatie dat in de tabel bestaat

