![voorbeeldexamen](examen_OS.pdf)

---
1. Hoe maak je een netwerkverbinding naar een andere Linux-machine om daar een shell te openen?
	1. `ssh username@host`
2. De gebruiker 'student' werkt vanuit de directory '/home/student'. Hoe maak hij een map 'examen' in '/tmp' en een submap 'week1' daarin, zonder de 'cd'-opdracht te gebruiken? Gebruik hiervoor een absoluut pad
	- `mkdir -p /tmp/examen/week1`
3. Nu wil de gebruiker ook een bestand met de naam 'bestand.txt' aanmaken in de map week1.
	Veronderstel dat hij nog steeds werkt vanuit zijn home directory en gebruik een relatief pad. Geef het commando
	- `touch ../../tmp/examen/week1/bestand.txt`
4. Hoe verplaats de gebruiker het bestand 'bestand.txt' naar zijn home directory? Veronderstel dat zijn pwd ‘/tmp/examen/week1’ is. Hernoem het ‘bestand.txt’ naar ‘bestand’ terwijl je dit commando uitvoert.
	-  `mv ./bestand.txt ~/bestand`
5. Een gebruiker wil een kopie van '/etc/passwd' in zijn thuismap maken als 'passwd.backup'. Hoe
	doet hij dit, ongeacht zijn gebruikersnaam of huidige locatie in het systeem?
	- `cp /etc/passwd ~/passwd.backup`
6. Wat is het doel van het bestand '/etc/shadow'? Dit mag in het Nederlands of het Engels.
	- betand met verlsutelde paswoorden en wanneer ze vervallen
7. Een gebruiker wil de inhoud van '/etc/sudoers' bekijken met 'cat /etc/sudoers', maar krijgt een
	foutmelding. Hoe kan de gebruiker zichzelf tijdelijk de juiste rechten geven om het bestand toch te bekijken? 
	- `sudo !!`
8. Een gebruiker bewerkt het bestand '.ssh/known_hosts' met de vi(m) editor. Hoe verlaat de
	gebruiker vi(m) zonder wijzigingen op te slaan?
	1. `<ESC>`
	2. `:q!`
9. Een gebruiker wil hetzelfde effect bereiken als 'cat adressen.txt | sort | cat > adressen2.txt', maar zonder pipelining te gebruiken. Wat is het alternatieve commando?
	- `sort adressen.txt > adressen2.txt`
10. Een Linux-gebruiker wil alleen foutmeldingen zien van het commando 'find / -print'. Hoe doet hij dit?
	- `find / -print 2> &1`
```
Nils Cant;55km/h;Antwerpen
Guy Crets;140km/h;Mechelen
Nils Cant;56km/h;Mortsel
Nils Cant;54km/h;Aartselaar
Kris Demuynck;182km/h;Brussel
Guy Crets;31km/h;Lier
```
11. Hoe toon je alleen de regels met de naam "Guy Crets"?
	- `grep 'Guy Crets snelheidsovertredingen.txt`
12. Hoe verkrijg je een gesorteerde, unieke lijst van alleen de namen van overtreders?
	- `cat snelheidsovertredingen.csv | uniq | sort `
13. Hoe toon je alle regels uit het bestand waar de naam "Nils Cant" niet voorkomt?
	- `grep -v 'Nils Cant'`
14. Hoe vervang je de naam "Kris Demuynck" door "Jill Claes" en vervang je de puntkomma's (;)
	door komma's (,)? De uitvoer moet naar een nieuw bestand genaamd
	"ernstige_snelheidsovertredingen_05_2023.csv" gaan.
	- `cat snelheidsovertredingen.csv | tr 'Kris Demuynck' 'Jill Claes' | cut -d ';' -f 1| tr ';' ',' > ernstige_snelheidsovertredingen_05_2023.csv`
15. Hoe toon je alleen snelheidsovertredingen tussen 100 km/u en 999 km/u uit het bestand
	"ernstige_snelheidsovertredingen_05_2023.csv"? Tip: gebruik reguliere expressies.
	- `grep -E "[0-9]{3}" ernstige_snelheidsovertredingen_05_2023.csv`
16. Hoe maakt een gebruiker een symbolische (soft) link genaamd "htdocs" in zijn thuismap, die
	verwijst naar de directory '/var/www/html'?
	- `ln -s /var/www/html htdocs`
17. Hoe bepaal je of het '/usr/bin/man'-commando een script (shell, Perl, enz.) of een uitvoerbaar
	(gecompileerd) programma is?
	- `file /usr/bin/man`
18. Hoe maak je een back-up van alle thuismappen van gebruikers naar het bestand
	'/tmp/backup-home.tar.gz' met absolute paden?
	- `tar -czf /home/* /tmp/backup-home.tar.gz`
19. Een gebruiker voert het commando `ls /home/student/documenten/*` uit om een lijst van alle bestanden in de map 'documenten' weer te geven. De gebruiker merkt op dat er sommige bestanden zijn	waarvoor hij geen toegangsrechten heeft, wat resulteert in foutmeldingen op het scherm. De gebruiker wil deze foutmeldingen vastleggen in een bestand genaamd 'errors.txt' voor latere referentie. Geef het commando dat de gebruiker moet gebruiken om deze foutmeldingen aan 'errors.txt' toe te voegen.
	- `ls /home/student/documenten/* 2> errors.txt`
20. Wat moet een Linux-gebruiker doen om het volgende resultaat te bereiken?
	- `MSG="Doe dat goed"`
---
