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
# DML instructies 

