
# Samenvatting Operating System Fundamentals

## Hoofdstuk 8: Scripting Deel 1
Introductie tot het automatiseren van taken met Bash-scripts.

* **Basis**: Een script is een tekstbestand met commando's. Het begint met een "shebang" (bv. `#!/bin/bash`) om de interpreter aan te geven.
* **Uitvoeren**: Maak het bestand uitvoerbaar met `chmod +x bestandsnaam.sh` en voer uit met `./bestandsnaam.sh`.
* **Variabelen**:
    * Toewijzen: `naam=waarde` (geen spaties rond `=`).
    * Gebruiken: `${naam}` of `$naam`.
    * Quoting: Dubbele quotes `""` behouden variabelen, enkele quotes `''` behandelen alles als letterlijke tekst.
* **Input/Output**:
    * `read`: Leest invoer van de gebruiker.
    * `echo`: Print tekst naar het scherm (stdout).
* **Argumenten**: Parameters die aan een script worden meegegeven (`$1`, `$2`, ...). `$#` is het aantal argumenten, `$@` zijn alle argumenten.

## Hoofdstuk 9: Scripting Deel 2
Geavanceerdere scriptingtechnieken voor logica en controle.

* **Exit Codes**: Elk commando geeft een status terug. `0` betekent succes, elk ander getal is een fout. Op te vragen met `$?`.
* **Condities (if-else)**:
    * Wordt gebruikt om beslissingen te nemen op basis van exit codes of test-condities (`[ ... ]`).
    * Testen: `-f` (bestand bestaat), `-d` (directory), `-eq` (gelijk aan getal), `==` (gelijk aan string).
* **Lussen (Iteraties)**:
    * `for`: Itereer over een lijst items (bv. bestanden).
    * `while`: Blijf herhalen zolang een conditie waar is.
* **Functies**: Herbruikbare stukken code binnen een script. Parameters worden binnen de functie benaderd met `$1`, `$2`, etc..

## Hoofdstuk 10: Lokale Gebruikers en Groepen
Beheer van gebruikersaccounts en groepen op een Linux-systeem.

* **Configuratiebestanden**:
    * `/etc/passwd`: Gebruikersinformatie (naam, UID, GID, home, shell).
    * `/etc/shadow`: Versleutelde wachtwoorden en verloopdatum.
    * `/etc/group`: Groepsinformatie.
* **Gebruikersbeheer**:
    * `useradd`: Nieuwe gebruiker aanmaken.
    * `usermod`: Gebruiker aanpassen (bv. toevoegen aan groep met `-aG`).
    * `userdel`: Gebruiker verwijderen.
    * `passwd`: Wachtwoord instellen.
* **Root & Sudo**:
    * `su`: Overschakelen naar een andere gebruiker (of root).
    * `sudo`: Commando's uitvoeren met root-rechten. Geconfigureerd in `/etc/sudoers` (vaak via de `wheel` groep).

## Hoofdstuk 11: Toegangscontrole
Het instellen van rechten op bestanden en mappen.

* **Permissies**: Lezen (`r=4`), Schrijven (`w=2`), Uitvoeren (`x=1`). Ingesteld voor User (u), Group (g) en Others (o).
* **Commando's**:
    * `chmod`: Permissies wijzigen (bv. `chmod 755 bestand` of `chmod u+x bestand`).
    * `chown`: Eigenaar (user/group) wijzigen.
* **Speciale Permissies**:
    * **SUID**: Voer bestand uit met rechten van de eigenaar.
    * **SGID**: Voer uit met rechten van de groep (of bestanden in dir erven groep).
    * **Sticky Bit**: Alleen eigenaar kan bestanden in een map verwijderen (bv. `/tmp`).
* **Umask**: Bepaalt de standaardrechten voor nieuwe bestanden.

## Hoofdstuk 12: Procesbeheer
Het monitoren en beheren van processen.

* **Processen**: Programma's in uitvoering, geïdentificeerd door een PID. Systemd is PID 1.
* **Monitoring Tools**:
    * `ps`: Toont huidige processen (bv. `ps aux`).
    * `top`: Interactief overzicht van systeemactiviteit en CPU-gebruik.
    * `uptime`: Toont systeembelasting (load average).
* **Signalen**:
    * `kill`: Stuur een signaal naar een proces (standaard TERM, `-9` is KILL).
    * `jobs`, `fg`, `bg`: Beheer van voorgrond- en achtergrondtaken.
* **Scheduling**:
    * `cron`: Periodiek uitvoeren van taken (via `crontab -e`).
    * `at`: Eenmalig uitvoeren op een later tijdstip.

## Hoofdstuk 13: Softwarebeheer
Installeren en updaten van softwarepakketten.

* **Pakketten**: Software gebundeld met metadata, scripts en dependencies (meestal `.rpm` of `.deb`).
* **Repositories**: Online opslagplaatsen voor softwarepakketten.
* **Package Manager (DNF)**: Gebruikt op RedHat-systemen.
    * `dnf install <pakket>`: Installeren.
    * `dnf update`: Systeem bijwerken.
    * `dnf search`: Zoeken naar pakketten.
    * `dnf list installed`: Geïnstalleerde software tonen.

## Hoofdstuk 14: Services en Daemons
Beheer van achtergrondservices die opstarten met het systeem.

* **Daemons**: Processen die op de achtergrond draaien (eindigen vaak op 'd', zoals `sshd`).
* **Systemd**: Het init-systeem dat services start en beheert.
* **Systemctl**: Commando om systemd aan te sturen:
    * `start` / `stop`: Service nu starten/stoppen.
    * `enable` / `disable`: Service wel/niet automatisch starten bij boot.
    * `status`: Status van een service bekijken.

## Hoofdstuk 15: Configureer en Beveilig SSH
Veilig verbinden met externe systemen.

* **SSH (Secure Shell)**: Versleutelde verbinding.
* **Encryptie**: Gebruikt asymmetrische encryptie (public/private key) voor de handshake en symmetrische encryptie voor de sessie.
* **Authenticatie**:
    * **Wachtwoord**: Minder veilig.
    * **Keys**: Veiliger. Genereer met `ssh-keygen`, kopieer public key naar server met `ssh-copy-id`.
* **Configuratie**:
    * Server: `/etc/ssh/sshd_config` (bv. root login uitschakelen: `PermitRootLogin no`).
    * Client: `~/.ssh/config` (voor shortcuts naar servers).

## Hoofdstuk 16: Schijf- en Partitiebeheer
Opslagbeheer in Linux.

* **Block Devices**: Fysieke schijven worden weergegeven in `/dev` (bv. `/dev/sda` of `/dev/nvme0n1`).
* **Partities**: Indeling van een schijf. Tools: `fdisk` (MBR) of `gdisk` (GPT).
* **Bestandssystemen (Filesystems)**:
    * Formatteren met `mkfs` (bv. `mkfs.ext4`, `mkfs.xfs`).
* **Mounten**: Het koppelen van een bestandssysteem aan een map (mount point) met `mount`.
    * Gebruik `/etc/fstab` om schijven automatisch te koppelen bij het opstarten.
    * UUID's worden gebruikt voor persistente identificatie van schijven.

---
## Hoofdstuk 18: Netwerken
### 1. Network Interface Fundamentals
* **Recap:** Network adapters possess IP addresses which can be viewed using the command `ip a` (short for `ip address show`).
* **Active Services:** Servers listen on specific ports (e.g., SSH on 22, HTTP on 80, HTTPS on 443). Tools like `ping` check activity, and `ssh` establishes connections.
* **Interface Naming:** Network connections are called "links" and follow specific naming conventions:
    * Ethernet adapters: Start with "eth" or "en".
    * Wireless adapters: Start with "wl" or "wlan".
    * Loopback adapter: Starts with "lo".
    * VPN links: Start with "tun".
* **Link Properties:** Links have a MAC address, at least one IP address, a network mask, a default gateway, and a DNS server address.

### 2. Network Configuration
* **DHCP:** IP addresses are typically assigned automatically by a DHCP server, often built into routers.
* **Configuration Tools:**
    * **GUI:** Operating systems like Windows, Linux, and MacOS provide graphical interfaces to toggle between Manual and Automatic (DHCP) assignments.
    * **NMTUI:** A semi-graphical text interface available in the terminal via the command `nmtui`.
    * **NMCLI:** A command-line tool useful for scripting. Key commands include:
        * `nmcli con show`: Shows links.
        * `nmcli con up <name>` / `down <name>`: Activates or deactivates a link.
        * `nmcli con add` / `del`: Adds or deletes links.
* **Configuration Files:** Network info is stored in `/etc/NetworkManager/system-connections`. Changes made directly to files require `nmcli con reload` to take effect.

### 3. DNS and Hosts Files
* **Function:** DNS servers translate names (e.g., www.kdg.be) into IP addresses.
* **Files:**
    * Used DNS servers are listed in `/etc/resolv.conf`.
    * Manual name-to-IP mappings can be added to the hosts file: `/etc/hosts` (Linux/Mac) or `C:\Windows\System32\drivers\etc\hosts` (Windows).
* **Lookup Tool:** The `nslookup` command is used to find the IP address of a domain.

### 4. Virtual Networking (Virtual Machines)
Hypervisors like VirtualBox create virtual networks using different modes:
* **NAT (Network Address Translation):** The host OS acts as a NAT router and DHCP server. It translates the guest's private IP into a public IP for internet access.
* **Host-only:** Creates an internal network isolated to the host and guests.
* **Bridged:** The guest connects directly to the external network via the host's adapter, appearing as a separate device.

### 5. Firewall Configuration
* **Management:** Firewalls block or open ports. On Linux, this is managed via `firewall-cmd`.
* **Commands:**
    * Check status: `sudo firewall-cmd --state` or `--list-all`.
    * Add services/ports: `sudo firewall-cmd --add-service=http --permanent` or `--add-port=80/tcp`.
    * Reload configuration: `sudo firewall-cmd --reload`.
* **Cockpit:** A web-based administration interface available at `http://localhost:9090`.

### 6. Additional Network Commands
* **`ss -tuln`**: Displays listening ports.
* **`tcpdump -i <interface>`**: Shows network traffic passing through a specific link.
* **`tracepath <host>`**: Displays the route (routers) to a specific machine.
* **`mtr <host>`**: Provides an interactive report of the routers between the local and remote machine.