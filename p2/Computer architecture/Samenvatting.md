# Computer Architecture & Embedded Systems Samenvatting

## 1. Introductie Embedded Systems & Arduino
* De **Arduino Uno** maakt gebruik van de **ATmega328P** microcontroller .
* Deze microcontroller bevat een CPU, Flash geheugen (31.50KB voor code) en RAM (2KB voor data) .
* Hardware aansturing gebeurt rechtstreeks via registers:
  * **DDRB / DDRC**: Data Direction Registers bepalen of een pin een in- of uitgang is .
  * **PORTB/PORTC**: Bepalen de output waarde (0 of 1) van de pinnen op een specifieke poort .
* **Let op**: Bij het in de cursus gebruikte multifunction shield is de LED-logica geïnverteerd. Een `0` schrijven zet de LED aan, en een `1` schrijven zet de LED uit .

## 2. Bitwise Operaties (Bitmanipulatie)
* Omdat we vaak specifieke pinnen willen aansturen zonder andere te beïnvloeden, gebruiken we bitwise operaties met een **bitmask** .
* **OR (`|`)**: Wordt gebruikt om specifieke bits op 1 te zetten (bijv. een LED uitzetten op het shield: `PORTB |= 0b00100000;`) .
* **AND (`&`)**: Wordt (vaak met een bitwise NOT `~`) gebruikt om bits veilig op 0 te zetten (bijv. een LED aanzetten: `PORTB &= ~_BV(LED1);`) .
* **XOR (`^`)**: Inverteert ('toggelt') specifieke bits .
* **Bit Shift (`<<`, `>>`)**: Schuift bits op. `1 << 5` maakt `0b00100000` . Rekenkundig komt naar links schuiven (`shl`) overeen met vermenigvuldigen met machten van 2, en naar rechts schuiven (`ashr`) met delen door machten van 2 .

## 3. De Moncky-2 Processor
* De Moncky-2 is een minimale 16-bit RISC processor ontworpen om de werking van een processor te begrijpen .
* **Architectuur**: Harvard-stijl met gescheiden geheugens .
  * **Code-RAM**: 65536 x 16 bit, bevat de instructies .
  * **Data-RAM**: 65536 x 16 bit, bevat waarden van variabelen .
  * **Registers**: 16 registers (`r0` t/m `r15`) van 16-bit voor tijdelijke data. Register `r15` is de **Program Counter (PC)** die altijd wijst naar de actuele instructie .
  * **ALU**: Arithmetic Logical Unit die 11 bewerkingen ondersteunt: `nop`, `or`, `and`, `xor`, `add`, `sub`, `shl`, `shr`, `ashr`, `not`, `neg` .
* **De 7 Basisinstructies** :
  1. `halt`: De processor stopt.
  2. `li r, i`: Load Immediate. Laadt een getal `i` direct in register `r`.
  3. `ALU r, s`: Voert een ALU-bewerking uit (bijv. `add r0, r1` doet `r0 = r0 + r1`).
  4. `ld r, (s)`: Load from RAM. Laadt data vanuit het Data-RAM adres in `s` naar register `r`.
  5. `st r, (s)`: Store to RAM. Schrijft data van register `r` naar het Data-RAM adres in `s`.
  6. `jp r`: Jump. Springt naar het adres in register `r` (PC = reg[r]).
  7. `jpc r`: Voorwaardelijke sprong. Springt op basis van een conditie (bijv. `jpnz` voor 'jump if not zero').

## 4. De Compiler Toolchain & Code Vertaling
* Broncode is niet direct uitvoerbaar. Compilatiestappen: **Source code -> Preprocessor -> Compiler -> Assembler -> Linker -> Executable code** .
* Elke processorfamilie (Intel, ARM, MIPS, Moncky) heeft zijn eigen instructieset. C-code voor ARM draait dus niet direct op Intel .
* **Vertalingsvoorbeeld (Variabelen & Rekenen)** :
  * `a = 4;` wordt gecompileerd naar:
    `li r0, 4` (laad 4 in `r0`)
    `li r1, 33` (laad RAM-adres 33 voor variabele `a` in `r1`)
    `st r0, (r1)` (sla de waarde 4 op in RAM-adres 33)
  * `a = a + b;` vertaalt naar het inladen van beide RAM-adressen in registers (`ld`), het optellen (`add r1, r2`), en het resultaat weer opslaan (`st`) .
* **Controle flow (If/Loops)**:
  * `if`-statements en `while`/`for`-loops worden op de Moncky vertaald via **labels** en de **voorwaardelijke sprong (`jpc`)** . Voor een `while (i < 100)` berekent de compiler `i - 100` (`sub`) en kijkt of het resultaat negatief is via `jpns` (Jump if Negative Sign) om de lus voort te zetten of te stoppen .

## 5. Interrupts & Hardware Interfacing
* Een **interrupt** is een hardware-verzoek (bijv. een drukknop) dat de processor dwingt zijn huidige programma te pauzeren, een specifieke routine uit te voeren en daarna te hervatten .
* **Voordelen**: Hoge responsiviteit, efficiëntie (geen continue *polling* nodig), en energiebesparing .
* Wanneer geactiveerd, zoekt de processor in de *Interrupt Vector Table* naar de bijbehorende **Interrupt Service Routine (ISR)**, voert deze uit, en hervat daarna het hoofdprogramma .
* **Configuratie op de ATmega328P (Pin Change Interrupts)** :
  1. **PCICR**: Activeer de interrupt voor een specifieke poort (bijv. `PCICR |= _BV(PCIE1);` voor poort C).
  2. **PCMSKx**: Bepaal welke pin(nen) op die poort de interrupt mogen triggeren (bijv. `PCMSK1 |= _BV(BUTTON1);`).
  3. **ISR schrijven**: Gebruik de macro `ISR(PCINTx_vect) { ... }` om de logica uit te voeren.
  4. **sei() / cli()**: Zet het globale interruptsysteem aan (`sei()`) of uit (`cli()`).

## 6. Pointers & Geheugenbeheer in C
* **Geheugenadressen en Pointers**: De `&`-operator geeft het fysieke geheugenadres van een variabele in de RAM (bijv. `&a`). Een pointer is een variabele die dit adres bewaart (bijv. `int* b = &a;`). De `*`-operator (dereferencing) wordt gebruikt om de actuele waarde op dat adres aan te passen of uit te lezen (bijv. `(*a)++`) .
* **Functieparameters (By-value vs. By-reference)** : 
  * Standaard werkt C 'by-value': je geeft een variabele mee aan een functie en de functie maakt daar intern een kopie van. Aanpassingen worden niet bewaard.
  * Wil je de *originele* variabele aanpassen? Geef dan een pointer mee via 'by-reference' (bijv. `void increment_byref(int* a)`).
* **Arrays & Pointers**: De naam van een array fungeert onder water als een pointer naar het eerste element (dus `c` is hetzelfde als `&c`) . 
  * Let op: als je een array als parameter meegeeft aan een functie (zoals `void array_as_parameter(int* p)`), wordt dit gezien als een pure pointer. Gebruik je daar `sizeof(p)`, dan krijg je de grootte van de pointer en *niet* de originele lengte van de array .
  * Bij het itereren door een dynamische array kan je de blokhaken notatie gebruiken (`tabc[i]`), óf pointer-rekenen (`*(tabm + i)`) .
* **Dynamisch Geheugen (Heap)** : Voor arrays waarvan je de grootte pas tijdens de runtime weet, gebruik je dynamische allocatie met de `<stdlib.h>` bibliotheek.
  * `malloc(size)`: Reserveert een geheugenblok, maar behoudt de willekeurige oude 'garbage' data in die blokken.
  * `calloc(aantal, size)`: Reserveert het geheugen en vult dit direct veilig met nullen op.
  * **Belangrijk**: Gebruik altijd `free(pointer);` om het geheugen nadien expliciet terug vrij te geven om 'memory leaks' te voorkomen.
* **Complexe Pointers** : Arrays met tekst (strings) van ongelijke lengtes kunnen geheugenefficiënt worden opgeslagen door middel van een array van pointers (`char* pnamen[AANTAL]`) of zelfs een dubbele pointer (`char** ppnamen`) waarbij je met `malloc(strlen(...) + 1)` per woord exact de juiste ruimte reserveert.