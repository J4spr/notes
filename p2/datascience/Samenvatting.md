# Samenvatting Data Science Fundamentals

## 1. Doelstellingen van Data-analyse
* **Descriptief:** Wat gebeurt er? (Frequenties, trends, uitschieters).
* **Exploratief:** Waarom gebeurt het? (Relaties zoeken tussen variabelen).
* **Confirmatorisch:** Zijn we zeker dat het gebeurt? (Statistische toetsing).
* **Predictief:** Wat gaat er gebeuren? (Voorspellen op basis van modellen).

## 2. Soorten Data
* **Data Types:** * *Transactionele data* (Business events/transacties).
    * *Master data* (Stamgegevens van entiteiten zoals klanten).
    * *Analytische data* (Data over business performance).
* **Structuur:**
    * *Gestructureerd:* Georganiseerd in rijen/kolommen (naam, adres).
    * *Ongestructureerd:* 85% van business data (e-mail, video, tekst).
* **Big Data:** Gekenmerkt door de 3 V's: Volume, Velocity (snelheid), en Variety (variëteit).

## 3. Meetniveaus (Meetschalen)
* **Kwalitatief (Categorisch):**
    * *Nominaal:* Enkel onderscheid (v/m, automerk, bloedgroep).
    * *Ordinaal:* Onderscheid + natuurlijke ordening (tevredenheid, rangen leger, diploma).
* **Kwantitatief (Numeriek):**
    * *Interval:* Getal, vaste afstanden, GEEN absoluut nulpunt (temperatuur °C, IQ, tijd).
    * *Ratio:* Getal, absoluut nulpunt mogelijk, verhoudingen mogelijk (lengte, gewicht, inkomen).

## 4. Modelkwaliteit
* **Betrouwbaarheid:** Stabiliteit en reproduceerbaarheid van de resultaten (steeds hetzelfde meten).
* **Validiteit:** Nauwkeurigheid; meet je wat je beoogt te meten? (de juiste informatie).

## 5. Datareeksen en Variabelen
* **Datapunt:** Eén enkele observatie met waarde en context.
* **Tijdreeks:** Metingen van dezelfde gebeurtenis doorheen de tijd.
* **Cross-sectionele reeks:** Metingen op verschillende plaatsen/situaties op hetzelfde moment.
* **Variabelen:**
    * *Onafhankelijk (Rechterkant):* De context/oorzaak (bijv. tijdstip, datacenter).
    * *Afhankelijk (Linkerkant):* Wat we bestuderen/het gevolg (bijv. server responstijd).

## 6. Kansberekening Basis
* **Wet van Laplace:** P(A) = aantal gewenste uitkomsten / totaal aantal mogelijke uitkomsten.
* **Eigenschappen:** Een kans ligt altijd tussen 0 en 1. De som van alle mogelijke kansen is 1.
* **Tegengestelde gebeurtenis:** P(niet A) = 1 - P(A).
* **Voorwaardelijke kans:** P(A|B) is de kans op A, gegeven dat B al is opgetreden.
---

# Samenvatting Descriptieve Data-analyse: Centrum- en Spreidingsmaten

## 1. Centrummaten
Centrummaten beschrijven het centrale punt of de "typische" waarde van een gegevensset.
* **Gemiddelde ($\bar{x}$):** De som van alle waarden gedeeld door het totaal aantal waarnemingen ($n$). Het is gevoelig voor uitschieters.
* **Mediaan:** De middelste waarde wanneer de data van klein naar groot is gesorteerd. Het is een robuuste maatstaf die niet wordt beïnvloed door uitschieters.
* **Modus:** De waarde die het meest frequent voorkomt in de datareeks.

## 2. Spreidingsmaten
Spreidingsmaten geven aan hoe sterk de gegevens verspreid liggen rondom het centrum.
* **Variatiebreedte (Range):** Het verschil tussen de hoogste (Maximum) en laagste (Minimum) waarde in een dataset.
* **Interkwartielafstand (IQR):** De afstand tussen het eerste kwartiel ($Q_1$) en het derde kwartiel ($Q_3$); het beschrijft de spreiding van de middelste 50% van de data.
* **Variantie ($s^2$):** De gemiddelde gekwadrateerde afwijking van het gemiddelde.
* **Standaarddeviatie ($s$):** De vierkantswortel van de variantie. Het drukt de spreiding uit in dezelfde eenheid als de oorspronkelijke gegevens.



[Image of standard deviation on a normal distribution curve]


## 3. Vorm van de Verdeling
De vorm van de data geeft inzicht in de symmetrie en de aanwezigheid van uitschieters.
* **Symmetrisch:** De linker- en rechterkant van de verdeling zijn elkaars spiegelbeeld; gemiddelde en mediaan liggen dicht bij elkaar.
* **Scheefheid (Skewness):** * *Rechts-scheef:* De staart van de verdeling loopt uit naar rechts (positief).
    * *Links-scheef:* De staart van de verdeling loopt uit naar links (negatief).



[Image of normal distribution vs skewed distribution]


## 4. Visualisatie en Uitschieters
* **Boxplot:** Een grafische weergave van de vijf-getallensamenvatting (minimum, $Q_1$, mediaan, $Q_3$, maximum).
* **Uitschieters (Outliers):** Waarden die uitzonderlijk hoog of laag zijn vergeleken met de rest van de dataset. Ze kunnen duiden op fouten in de data of op bijzondere fenomenen.



## 5. Datakwaliteit
Bij het beschrijven van data is het essentieel om te controleren op:
* **Ontbrekende waarden:** Zijn er gaten in de dataset?.
* **'Vuile' data:** Bevat de dataset fouten of onverwachte waarden?.