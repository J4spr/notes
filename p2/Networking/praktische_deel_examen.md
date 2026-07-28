

|NETCAT:  TCP||
|-|-|
|ncat -l -p 8080|start luisterende tcp poort|
|ncat 127.0.0.1 8080|verbind met poort via loopback connector|

|NETCAT: UDP||
|-|-|
|ncat -l -u -p 8080|start udp server|
|ncat -u 127.0.0.1 8080|verdind met poort via loopback connector|

|NETCAT algemeen||
|-|-|
|ncat -l -p 9999 -e /bin/bash|(Linux) Start een listener die een bind shell (terminal) weggeeft bij verbinding|
|ncat -l -p 9999 -e cmd.exe|(Windows) Start een listener die een bind shell weggeeft|
|ncat 127.0.0.1 8080 < bestand.txt|Stuur de inhoud van een bestand over de lijn naar de server|
|ncat -l -p 8080 > bestand.txt|Vang inkomende data op en sla op in een bestand|





|NMAP||
|-|-|
|nmap 127.0.0.1|tcp scan, scant 1000 meest gangbare poorten|
|nmap -p 8080 127.0.0.1|scant een specifieke poort en kan checken of bv ncat server draait|
|nmap -sV 127.0.0.1|nmap probeert te checken welke applicatie er op de poort draait|
|nmap -sU -p 8080 127.0.0.1|udp scan, vereist admin/root rechten|
|nmap -A 127.0.0.1|Combineert -sV, -O, script scanning (-sC) en een traceroute|
|nmap -O 127.0.0.1|probeert het besturingssysteem van het doelwit te achterhalen|
|nmap -sS 127.0.0.1|SYN Stealth scan: Halve TCP-handshake scan (stuurt SYN, wacht op SYN-ACK, reageert met RST). Valt minder op in logs. Vereist root/admin|
|nmap -sn 192.168.1.0/24|Scant geen poorten, maar controleert alleen welke IP-adressen in het subnet online zijn.|

|WIRESHARK||
|-|-|
|tcp.port == 8080|Alleen TCP op poort 8080|
|udp.port == 8080|Alleen UDP op poort 8080|
|ip.addr == 127.0.0.1|Alleen het verkeer tussen jouw client en server (IP)|
|tcp.flags.syn == 1|Een specifieke TCP flag zoeken (bijv. de SYN handshake)|
|tcp.flags.syn == 1 \&\& tcp.flags.ack == 1|Zoeken naar specifiek de SYN-ACK stap van de handshake|
|ip.src == 10.0.0.5|Toon alleen pakketjes waarbij dit IP-adres de bron (source) is|
|ip.dst == 10.0.0.5|Toon alleen pakketjes waarbij dit IP-adres de bestemming (destination) is|
|dns \|\| dhcp|toon pakketjes die of DNS of DHCP gebruiken|
|tcp.stream == 0|Toon alleen de pakketjes die horen bij TCP-verbinding nr 0 (rechtermuisknop -> Follow -> TCP Stream)|
|http.request.method == "POST"|Toon alleen HTTP POST-requests|

|COMMANDO'S||
|-|-|
|netstat -ano \| findstr 8080|Actieve connecties bekijken|
|ipconfig /all|Je eigen IP en MAC opvragen|
|arp -a|Je lokale ARP tabel bekijken|
|arp -d \*|De lokale ARP-tabel volledig leegmaken|
|ping -n 5 8.8.8.8|Stuur exact 5 ICMP Echo Requests naar een IP om de responstijd en packet loss te testen|
|nslookup google.com|Vraag aan de ingestelde DNS-server welk IP-adres (A-record) bij deze domeinnaam hoort|
|tracert 8.8.8.8|Toont elke router (hop) waar het pakketje langskomt om de bestemming te bereiken|



