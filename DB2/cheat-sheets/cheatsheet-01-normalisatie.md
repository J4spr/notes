# Cheat Sheet 1: Database Normalisatie & Integratie (DB2)

> **Doel:** Snel en foutloos van 0NV naar 3NV decomponeren tijdens het open-boek examen, zonder dataverlies en zonder redundantie of anomalieën.

---

## 1. Kernbegrippen
* **Normalisatie:** Het stapsgewijs splitsen van gegevensgroepen volgens formele regels (zonder informatieverlies) om redundantie en update-, insert- en delete-anomalieën te elimineren.
* **Functionele Afhankelijkheid ($A \rightarrow B$):** Attribuut $B$ is functioneel afhankelijk van attribuut $A$ als één waarde van $A$ exact één unieke waarde van $B$ bepaalt ($A$ is de **determinant**).
* **Volledige Functionele Afhankelijkheid:** $B$ hangt af van de héle samengestelde sleutel $(A_1, A_2)$ en niet van slechts een deel daarvan ($A_1$ of $A_2$).
* **Transitieve Afhankelijkheid ($A \rightarrow B \rightarrow C$):** Een niet-sleutelattribuut $C$ is functioneel afhankelijk van een ander niet-sleutelattribuut $B$, waardoor $C$ indirect afhankelijk is van sleutel $A$.
* **De Gouden Regel (Bill Kent):**
  > *"Every non-key attribute must provide a fact about **the key** (1NV), **the whole key** (2NV), and **nothing but the key** (3NV), so help me Codd."*

---

## 2. De 4 Normalisatiestappen (0NV $\rightarrow$ 3NV)

### 0NV (Nulde Normaalvorm)
* **Wat te doen:**
  1. Maak een complete inventarisatie van alle gevraagde gegevensvelden.
  2. **Elimineer procesgegevens:** Berekende velden (zoals `totaalbedrag = aantal * prijs` of `leeftijd`) worden **geschrapt**; die bewaar je niet in de database.
  3. Duid een voorlopige **identifier** (sleutelkandidaat) aan.

### 1NV (Eerste Normaalvorm)
* **Criterium:** Geen herhalende groepen (repeating groups) en alle attribuutwaarden zijn **atomair** (één waarde per cel, geen komma-gescheiden lijsten).
* **Hoe toepassen:**
  1. Identificeer herhalende gegevens (attributen die meerdere keren voorkomen voor één identifier).
  2. Splits de herhalende attributen af naar een **nieuwe groep**.
  3. Neem de identifier van de oorspronkelijke groep mee naar de nieuwe groep.
  4. Vorm in de nieuwe groep een **samengestelde primaire sleutel** (bv. `(oorspronkelijke_id, herhalend_id)`).

### 2NV (Tweede Normaalvorm)
* **Criterium:** De relatie staat in 1NV én elk niet-sleutelattribuut is **volledig functioneel afhankelijk** van de hele primaire sleutel.
* **Belangrijke examenvink:** 2NV hoeft **enkel** gecontroleerd te worden bij groepen met een **samengestelde primaire sleutel**! Heeft een tabel een enkelvoudige PK, dan staat hij automatisch al in 2NV.
* **Hoe toepassen:**
  1. Zoek attributen die slechts afhangen van een **deel** van de samengestelde sleutel (partiële afhankelijkheid).
  2. Splits deze attributen af naar een nieuwe entiteit samen met dat specifieke sleuteldeel als primaire sleutel.
  3. In de oorspronkelijke tabel blijven alleen attributen staan die de **volledige combinatie** van sleutels nodig hebben.

### 3NV (Derde Normaalvorm)
* **Criterium:** De relatie staat in 2NV én bevat **geen transitieve afhankelijkheden** (geen afhankelijkheden tussen niet-sleutelattributen onderling).
* **Hoe toepassen:**
  1. Zoek patronen waarbij niet-sleutelattribuut $B$ een ander niet-sleutelattribuut $C$ bepaalt ($B \rightarrow C$).
  2. Splits $B$ en $C$ af naar een aparte lookup-tabel.
  3. In de nieuwe tabel wordt $B$ de primaire sleutel (`PK`).
  4. In de oorspronkelijke tabel blijft $B$ achter als buitenlandse sleutel (`FK`) om de relatie te bewaren.

---

## 3. Oefenmatrix & Werkwijze voor het Examen

Teken op het examen altijd deze 4 kolommen om het overzicht te bewaren:

| 0NV | 1NV | 2NV | 3NV |
| :--- | :--- | :--- | :--- |
| **<u>id1</u>** | **<u>id1</u>** | **<u>id1</u>** | **<u>id1</u>** |
| veld_a | veld_a | veld_a | veld_a |
| *herhalend:* | | | |
| id2 | **<u>id1</u>** | **<u>id1</u>** | **<u>id1</u>** |
| veld_b | **<u>id2</u>** | **<u>id2</u>** | **<u>id2</u>** |
| veld_c (hangt af van id2) | veld_b | veld_b | veld_b |
| veld_d (hangt af van veld_c)| veld_c | | |
| | veld_d | **<u>id2</u>** | **<u>id2</u>** |
| | | veld_c | veld_c (FK) |
| | | veld_d | |
| | | | **<u>veld_c</u>** |
| | | | veld_d |

---

## 4. Integratie van Normalisatieresultaten
Wanneer verschillende gebruikersbehoeften afzonderlijk genormaliseerd zijn, moeten de deelresultaten worden samengevoegd:
1. **Controleren op synoniemen:** Verschillende namen voor hetzelfde concept (bv. `klantnr` vs `klantcode`) $\rightarrow$ harmoniseer naar één eenduidige benaming.
2. **Controleren op homoniemen:** Dezelfde naam voor verschillende concepten (bv. `datum` bij bestelling vs `datum` bij factuur) $\rightarrow$ geef specifieke namen (`besteldatum`, `factuurdatum`).
3. **Samenvoegen van tabellen met gelijke primaire sleutel:** Tabellen met identieke PK's worden samengevoegd tot één entiteit.
4. **Transformeren naar relationeel model:** Tabelnamen meervoudig (`Klant` $\rightarrow$ `Klanten`), PK's onderstrepen en FK's expliciet markeren.

---

## 5. Hogere Normaalvormen (Theorie-definities)
* **BCNV (Boyce-Codd Normaalvorm):** Elke minimale determinant moet een kandidaat-sleutel zijn. (Strenger dan 3NV als er meerdere overlappende kandidaat-sleutels zijn).
* **4NV:** Verwijdert meervoudige (multivalued) afhankelijkheden uit groepen met enkel sleutelattributen.
* **5NV (Projectie-Join Normaalvorm):** Een relatie kan niet worden opgedeeld in kleinere projecties zonder informatieverlies bij de hereniging via JOIN.
