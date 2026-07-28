# Management Accounting: Volledige Cursus Samenvatting & Oefengids

---

## Deel 1: Cost Accounting & Break-even

### 1. Kostprijsberekening per eenheid
De totale fabricagekostprijs ($FKP$) bestaat uit een combinatie van vaste en variabele kosten. Om dit te berekenen, doorloop je de volgende stappen:

* **Stap 1: Identificeer de vaste kosten.** Dit zijn kosten die onafhankelijk zijn van het productievolume binnen een bepaalde capaciteit (bijv. afschrijvingen, basissalarissen directie).
* **Stap 2: Identificeer de variabele kosten.** Dit zijn kosten die rechtstreeks meestijgen met het aantal geproduceerde eenheden (bijv. grondstoffen, energieverbruik per machine-uur).
* **Stap 3: Pas de formules toe:**
  $$Totale FKP = Vaste Fabricagekosten + (Variabele Fabricagekosten per eenheid * E)$$
  $$Fabricagekostprijs / eenheid = \frac{Vaste Fabricagekosten}{E} + Variabele Fabricagekosten per eenheid$$
  *(waarbij $E$ het aantal geproduceerde eenheden is)*

> [!TIP]
> **Oefening om zelf te proberen (Slide 24):**
> Vul de tabel aan voor een productie van 32.000, 38.000 en 100.000 eenheden op basis van de gegevens van ComputerHouse (Slide 6). Let goed op de capaciteit van de assemblagelijn (8.500 uur/jaar) en hoe de beheerskosten verdeeld worden!

---

### 2. Break-even Analyse
Het kritisch of break-even punt ($E_{BE}$) is het productie- en verkoopvolume waarbij de totale omzet exact gelijk is aan de totale kosten (de winst is dan 0).

* **Stap 1:** Bepaal de verkoopprijs ($VP$) per eenheid.
* **Stap 2:** Bepaal de variabele kosten ($VK$) per eenheid.
* **Stap 3:** Bereken de contributiemarge per eenheid:
  $$Contributie per E = VP - VK per E$$
* **Stap 4:** Bereken het break-even punt in eenheden:
  $$E_{BE} = \frac{Vaste Kosten (FK)}{VP - VK per E}$$

> [!NOTE]
> **Voorbeeldoefening opgelost (Slide 40-42):**
> N.V. De Hoeve: $FK = € 375.000$; $VK = € 5.000$; $VP = € 12.500$.
> - $Contributie per E = € 12.500 - € 5.000 = € 7.500$
> - $E_{BE} = € 375.000 / € 7.500 =$ **50 bungalows**
> - $Break-even omzet = 50 * € 12.500 = € 625.000$

---

### 3. Speciale orders (Beslissingsmodel)
Moet je een eenmalig order tegen een lagere verkoopprijs aanvaarden? 

* **Stap 1:** Controleer of er voldoende vrije productiecapaciteit is.
* **Stap 2:** Bereken de contributiemarge van het speciale order ($VP_{speciaal} - VK_{per E}$).
* **Stap 3:** Pas de beslissingsregel toe:
  - $VP > Integrale kostprijs \rightarrow$ **Aanvaarden**.
  - $VP < VK_{per E} \rightarrow$ **Niet aanvaarden** (je maakt puur verlies op de grondstoffen/arbeid).
  - $VK_{per E} < VP < Integrale kostprijs \rightarrow$ **Verder onderzoeken**. Als er vrije capaciteit is en de vaste kosten al gedekt zijn door de normale productie, levert elke positieve contributiemarge extra winst op!

---

### 4. Make or Buy Beslissingen (Zelf maken of Uitbesteden)
Bij deze oefeningen (zoals *4.9 Kitchenapp*, *4.12 Meubellux* en *4.13 Peluche*) moet je beslissen of je een onderdeel zelf blijft produceren of het aankoopt bij een externe leverancier.

* **Stap 1: Bereken de relevante kosten van ZELF MAKEN.**
  - **Wel meenemen:** Variabele productiekosten (grondstoffen, directe uren) and vermijdbare vaste kosten (bijv. een machine die je specifiek voor dit onderdeel huurt en kunt opzeggen).
  - **Niet meenemen:** Onvermijdbare vaste kosten (zoals algemene fabrieksoverhead of afschrijvingen van machines die sowieso blijven staan). Deze kosten lopen immers gewoon door.
* **Stap 2: Bepaal de kosten van KOPEN.**
  - Dit is simpelweg: $Aankoopprijs per eenheid \times het benodigde aantal eenheden$ (+ eventuele extra transport- of bestelkosten).
* **Stap 3: Controleer de opportuniteitskosten (Vrije capaciteit).**
  - Als je door te 'buyen' capaciteit vrijmaakt waarmee je een ander product kunt maken dat winst oplevert, tel je die misgelopen winst op als extra kosten bij de optie 'Zelf maken'.
* **Stap 4: Vergelijk en Beslis.** Kies de optie met de laagste totale relevante kosten.

> [!TIP]
> **Oefening om zelf te proberen (Oefening 4.9 Kitchenapp / 4.12 Meubellux):**
> Loop door de gegevens van de oefeningenbundel. Identificeer welke vaste kosten gemarkeerd staan als "blijven bestaan, ook bij uitbesteding" en elimineer deze uit je berekening voor de beslissing.

---

### 5. Multi-product Break-even (Assortimentsanalyse)
In de realiteit verkoopt een bedrijf vaak meerdere producten met verschillende marges (zoals in *4.4 Souperbike* of *4.5 Waese raapjes*).

* **Stap 1:** Bepaal de verkoopmix (omzet- of afzetverhouding). Bijvoorbeeld: voor elk product A verkoop je twee stuks van product B (verhouding 1:2).
* **Stap 2:** Bereken de gewogen gemiddelde contributiemarge ($GGCM$):
  $$GGCM = (Marge A \times \% Mix A) + (Marge B \times \% Mix B)$$
* **Stap 3:** Bereken het totale break-even punt in 'pakketjes':
  $$Totale Pakketten_{BE} = \frac{Totale Vaste Kosten}{GGCM}$$
* **Stap 4:** Splits het aantal eenheden terug uit naar de individuele producten op basis van de initiële verkoopmix.

---

## Deel 2: Investeringsanalyse & Financieel Plan

### 1. Investeringskasstromen (Cash Flows)
Bij projectbeoordeling kijken we naar de timing van binnenkomende en uitgaande geldstromen.

* **Stap 1:** Noteer de initiële investering in **Jaar 0** (dit is een negatieve kasstroom).
* **Stap 2:** Identificeer de **differentiële (incrementele) stromen** in de opvolgende jaren. Kosten die voor beide opties hetzelfde zijn (zoals papierkosten in het printervoorbeeld), laat je weg.
* **Stap 3:** Bereken de netto impact per jaar. Minder uitgaven (besparingen) tellen mee als een positieve kasstroom ($+$).

---

### 2. Tijdswaarde van Geld (Annuïteiten)
Geld vandaag is meer waard dan geld in de toekomst. Een annuïteit is een reeks van opeenvolgende, gelijke betalingen of ontvangsten.

* **Formule Beginwaarde (Present Value) van een gewone annuïteit:**
  $$PV_{(k,n,r)} = k \times \frac{1 - (1+r)^{-n}}{r}$$
  *(waarbij $k$ = termijnbedrag, $r$ = rentevoet, $n$ = aantal perioden)*
* **Bijzonder geval: Perpetuïteit** (een oneindige reeks betalingen):
  $$PV = \frac{k}{r}$$

---

### 3. Het Financieel Plan (Balans & Cash Flow Statement)
Om te controleren of je project financieel gezond blijft, koppel je de resultatenrekening aan de balans en de kasstroomstaat.

* **De Balans-formule:** $$Activa (Bezittingen) = Passiva (Eigen Vermogen + Schulden)$$
* **Berekening Operationele Kasstroom (Slide 52):**
  $$Operationele Kasstroom = Bedrijfswinst (EBIT) + Afschrijvingen - \Delta Behoefte aan Bedrijfskapitaal$$

> [!TIP]
> **Oefening om zelf te proberen (Slide 51-54):**
> Bestudeer het balansvoorbeeld. Probeer zelf te berekenen hoe de vorderingen in Jaar 2 veranderen als de omzet stijgt, gebruikmakend van de formule op Slide 51: $(Omzet / 365) \times 30  dagen krediet$.

---

### 4. Directe versus Indirecte Methode van Kasstroomplanning
Bij het opstellen van een financieel ondernemingsplan (zoals in deel VI en VII) kun je de operationele kasstroom op twee manieren benaderen.

#### A. De Directe Methode (Ontvangsten en Uitgaven)
Je kijkt puur naar de mutaties op de bankrekening:
* **Stap 1:** Bereken de $Klantontvangsten = Omzet inclusief BTW - Toename Handelsvorderingen$.
* **Stap 2:** Bereken de $Leveranciersbetalingen = Aankopen inclusief BTW - Toename Leveranciersschulden$.
* **Stap 3:** Trek alle operationele uitgaven (lonen, huur, interesten, btw-saldi) af van de ontvangsten.

#### B. De Indirecte Methode (Vertrekkend vanuit de winst)
Je corrigeert de papieren winst naar werkelijk geld (gebruikt in *Oefening 6.4 Pure Sound*):
* **Stap 1:** Neem de Bedrijfswinst ($EBIT$) uit de resultatenrekening.
* **Stap 2:** **Tel niet-kaskosten op ($+$):** Afschrijvingen en waardeverminderingen hebben je winst verlaagd, maar er is geen geld de onderneming uitgestroomd.
* **Stap 3:** **Corrigeer voor de Behoefte aan Bedrijfskapitaal ($\Delta BBK$):**
  - Is je voorraad of zijn je vorderingen gestegen? Dit heeft geld gekost $\rightarrow$ **Aftrekken ($-$)**.
  - Zijn je leveranciersschulden gestegen? Je hebt betalingen uitgesteld, dus geld vastgehouden $\rightarrow$ **Optellen ($+$)**.

> [!NOTE]
> **Belangrijk controlepunt voor je Financieel Plan:**
> De operationele kasstroom onder de indirecte methode moet exact gelijk zijn aan de uitkomst van de directe methode. Daarnaast moet de eindstand van je kasplanning op de euro nauwkeurig overeenstemmen met de post 'Liquide middelen' op je Balans.

---

### 5. Investeringscriteria: Net Present Value (NPV / CW)
Om te beslissen of een langetermijnproject rendabel is, rekenen we alle toekomstige kasstromen om naar de waarde van vandaag.

* **Stap 1:** Bereken de netto differentiële kasstroom ($CF_t$) voor elk jaar $t$.
* **Stap 2:** Actualiseer elke kasstroom met de vereiste rentevoet ($r$):
  $$Present Value (PV) = \frac{CF_t}{(1+r)^t}$$
* **Stap 3:** Bereken de Net Present Value (Netto Contante Waarde):
  $$NPV = \sum_{t=1}^{n} \frac{CF_t}{(1+r)^t} - I_0$$
  *(waarbij $I_0$ = Initiële Investering in Jaar 0)*
* **Beslissingsregel:**
  - $NPV > 0 \rightarrow$ Project is rendabel en creëert waarde $
ightarrow$ **Uitvoeren**.
  - $NPV < 0 \rightarrow$ Project kost meer dan het opbrengt $
ightarrow$ **Weigeren**.

---

## Deel 3: Integratie Financieel Plan & Ondernemingsplan

### 1. De Structuur van de Openingsbalans (Jaar 0)
Bij de opstart van een onderneming of project (zoals in *Oefening 6.3 BVBA Start*) stel je eerst de openingsbalans op. Dit is het nulpunt.

* **Stap 1: Breng de Activa (Aanwendingen) in kaart.**
  - Waar gaat het geld naartoe? (bijv. Oprichtingskosten, Vaste activa zoals machines/gebouwen, initiële Voorraden en de resterende Cash op de bank).
* **Stap 2: Breng de Passiva (Bronnen) in kaart.**
  - Waar komt het geld vandaan? (bijv. Ingebracht Eigen Vermogen / Maatschappelijk kapitaal, Langlopende bankleningen).
* **Stap 3: Pas de sluitingsregel toe.** Activa moet exact gelijk zijn aan Passiva. Als je banktekening de sluitpost is, bereken je deze als:
  $$Bank (Liquide middelen) = Totale Passiva - Overige Activa$$

---

### 2. De Resultatenrekening (Winst versus Kasstroom)
De resultatenrekening kijkt naar opbrengsten en kosten over een heel jaar volgens het *toerekeningsbeginsel* (accrual accounting), **exclusief BTW** (behalve de niet-aftrekbare BTW).


> [!WARNING]
> **Onthoud voor de examens:** Afschrijvingen zijn wel een *kost* (verlagen de winst), maar geen *uitgave* (er stroomt geen geld weg). Interesten van een lening zijn een *kost*, maar de terugbetaling van de hoofdsom (kapitaalsaflossing) is **geen kost** (dit is een balansmutatie die enkel je cash en je schuld verlaagt).

---

### 3. De BTW-Berekening og het BTW-Saldo
De BTW is voor een onderneming een doorgeefluik, maar heeft een enorme impact op de maandelijkse of kwartaalgebonden kasplanning.

* **Stap 1: Bereken de Verschuldigde BTW.** Dit is de BTW die jij aanrekent op je verkopen (Omzet $	imes$ BTW-tarief). Dit is een schuld aan de staat.
* **Stap 2: Bereken de Aftrekbare BTW.** Dit is de BTW die jij betaalt op je inkopen en investeringen (Aankopen/Investeringen $	imes$ BTW-tarief). Dit is een vordering op de staat.
* **Stap 3: Bepaal de positie op de Balans / Kasplanning:**
  - $Verschuldigde BTW > Aftrekbare BTW \rightarrow$ **Te betalen BTW** (Schuld op de passivazijde van de balans).
  - $Verschuldigde BTW < Aftrekbare BTW \rightarrow$ **Te terugvorderen BTW** (Vordering op de activazijde van de balans).

---

### 4. Koppeling naar de Eindbalans (Jaar 1, 2, 3...)
Elk afgesloten jaar muteert de balansposten op een specifieke manier. Dit is de ultieme controle in oefeningen zoals *7.1 Detailplanning*:

* **Vaste Activa:** $$Nieuwe Boekwaarde = Beginwaarde + Nieuwe Investeringen - Afschrijvingen van dit jaar$$
* **Eigen Vermogen:** $$Nieuw Eigen Vermogen = Beginwaarde + Gereserveerde Netto Winst van dit jaar$$
* **Financiële Schulden:** $$Nieuwe Bankrekening Schuld = Beginwaarde - Kapitaalsaflossingen van dit jaar$$

> [!TIP]
> **Oefening om zelf te proberen (Oefening 7.1 / Project 'The Company'):**
> Als je de eindbalans van Jaar 1 opstelt, vergeet dan niet om de berekende Netto Winst over te dragen naar de passivazijde onder het Eigen Vermogen (als "Overgedragen winst"). Als je dit vergeet, zal je balans aan het einde van de rit nooit in evenwicht zijn!

---

# Master Formularium: Management Accounting

## 1. Cost Accounting & Break-even (Deel 1)

### Kostprijs & Marges
* **Totale Fabricagekostprijs ($FKP$):**
  $$Totale FKP = Totale Vaste Kosten + (Variabele Kost per eenheid \times E)$$

* **Fabricagekostprijs per eenheid ($FKP_{per E}$):**
  $$FKP_{per E} = \frac{Totale Vaste Kosten}{E} + Variabele Kost per eenheid$$

* **Contributiemarge per eenheid ($CM_{per E}$):**
  $$CM_{per E} = VP - VK_{per E}$$

* **Contributiemarge-ratio ($CM\%$):**
  $$CM\% = \frac{VP - VK_{per E}}{VP} = \frac{Totale Contributiemarge}{Totale Omzet}$$

### Break-even Analyse (Kritisch Punt)
* **Break-even Afzet ($E_{BE}$ in eenheden):**
  $$E_{BE} = \frac{Totale Vaste Kosten}{VP - VK_{per E}} = \frac{Totale Vaste Kosten}{CM_{per E}}$$

* **Break-even Omzet ($TO_{BE}$ in euro):**
  $$TO_{BE} = E_{BE} \times VP = \frac{Totale Vaste Kosten}{CM\%}$$

* **Target Profit (Gewenste Winst behalen):**
  $$Vereiste Afzet = \frac{Totale Vaste Kosten + Target Profit}{CM_{per E}}$$

* **Gewogen Gemiddelde Contributiemarge ($GGCM$):**
  $$GGCM = \sum_{i=1}^{n} (CM_{i} 	imes Mix\%_{i})$$
  $$Totale Pakketten_{BE} = \frac{Totale Vaste Kosten}{GGCM}$$

---

## 2. Investeringsanalyse & Tijdswaarde (Deel 2)

### Interest & Annuïteiten
* **Toekomstige Waarde (Compound Interest):**
  $$FV_n = PV \times (1 + r)^n$$

* **Huidige Waarde (Discounting):**
  $$PV = \frac{FV_n}{(1 + r)^n} = FV_n \times (1 + r)^{-n}$$

* **Huidige Waarde van een Gewone Annuïteit:**
  $$PV_{annuïteit} = k \times \frac{1 - (1 + r)^{-n}}{r}$$

* **Huidige Waarde van een Perpetuïteit:**
  $$PV_{perpetuïteit} = \frac{k}{r}$$

### Investeringsselectie
* **Net Present Value ($NPV$):**
  $$NPV = \sum_{t=1}^{n} \frac{CF_t}{(1 + r)^t} - I_0$$

---

## 3. Financieel Plan & Balans-mutaties

### Bedrijfskapitaal & Krediettermijnen
* **Handelsvorderingen (Balanspost Klanten):**
  $$Handelsvorderingen = \frac{Omzet incl. BTW}{365} 	imes Kredietdagen Klanten$$

* **Leveranciersschulden (Balanspost Leveranciers):**
  $$Leveranciersschulden = \frac{Aankopen incl. BTW}{365} 	imes Kredietdagen Leveranciers$$

### Kasstroomberekeningen (Indirecte Methode)
* **Operationele Kasstroom:**
  $$Operationele Kasstroom = EBIT + Afschrijvingen - \Delta BBK$$

* **Behoefte aan Bedrijfskapitaal ($\Delta BBK$):**
  $$\Delta BBK = (\Delta Voorraden + \Delta Handelsvorderingen) - \Delta Leveranciersschulden$$

### Leningen & Aflossingen
* **Jaarlijkse Intrestkost (Resultatenrekening):**
  $$Intrest_t = Openstaande Restschuld_{t-1} \times Jaarlijkse Rentevoet$$

* **Eindstand Schuld op de Balans:**
  $$Restschuld_t = Openstaande Restschuld_{t-1} - Kapitaalsaflossing_t$$

### BTW & Resultatenverwerking
* **Netto BTW-saldo:**
  $$BTW-Saldo = Verschuldigde BTW (Verkopen) - Aftrekbare BTW (Inkopen + Investeringen)$$

* **Toegevoegde Waarde (Economische definitie):**
  $$Toegevoegde Waarde = Omzet (excl. BTW) - Verbruikte Goederen en Diensten (excl. BTW)$$
