# Groepsopdracht periode 1

### **Opties voor businesscases (met beschrijvingen):**

1. **(Mag niet) Bibliotheekbeheersysteem (voorbeeld ter inspiratie)**:
    - **Beschrijving**: Dit systeem beheert boeken, studenten (leden), bibliothecarissen en uitleenactiviteiten in een universiteitsbibliotheek. Studenten kunnen zoeken naar beschikbare boeken, deze lenen en terugbrengen. Bibliothecarissen kunnen de boekenvoorraad beheren en uitleenverzoeken afhandelen.
    - **Voorbeelden van begrippen**: boek, student, bibliothecaris, lenen, reserveren.
    - **Gebruiksscenario's**: Boek lenen, boek terugbrengen, catalogus doorzoeken, boek reserveren.
    - **Domeinobjecten**: boek, student, bibliothecaris, uitleentransactie.
2. **Online bestelsysteem voor eten**:
    - **Beschrijving**: Met dit systeem kunnen klanten menu's van verschillende restaurants bekijken, bestellingen plaatsen en leveringen volgen. Restauranthouders kunnen hun menu's beheren en bezorgers kunnen de status van leveringen bijwerken.
3. **Studentenregistratiesysteem**:
    - **Beschrijving**: Met dit systeem kunnen studenten zich inschrijven voor cursussen, lesroosters bekijken en studieplannen beheren. Docenten kunnen het cursusaanbod beheren en inschrijvingslijsten bekijken.
4. **Parkeerbeheersysteem**:
    - **Beschrijving**: Dit systeem beheert parkeerplaatsen voor een kantorencomplex. Medewerkers kunnen parkeerplaatsen reserveren, de beschikbaarheid controleren en hun reserveringen beheren. Beheerders kunnen parkeerplaatsen toewijzen en zorgen voor een efficiënt gebruik van de parkeerplaatsen.
5. **Online ticketverkoopsysteem voor evenementen**:
    - **Beschrijving**: Op dit platform kunnen gebruikers tickets kopen voor evenementen zoals concerten, sportwedstrijden en theatervoorstellingen. Organisatoren van evenementen kunnen evenementen plaatsen en gebruikers kunnen evenementdetails bekijken en tickets reserveren.

### **Deel 1: Groepsopdracht – Woordenlijst, objectgeoriënteerde analyse, use case-diagram en use case-beschrijvingen**

### **Opdracht**

Kies in je groep (4-6 personen) een van de gegeven businesscases (**niet uit de bibliotheek**). Maak eerst een **woordenlijst** met de belangrijkste termen, voer vervolgens **een objectgeoriënteerde analyse (OOA)** uit, maak een **use case-diagram** en schrijf **use case-beschrijvingen** om de businesscase weer te geven.

---

### **Stappen**

1. **Maak een woordenlijst**:
    - Definieer de belangrijkste termen die betrekking hebben op uw systeem.
    - **Voorbeeld (bibliotheeksysteem)**:
        - **Boek**: een fysiek of digitaal item dat kan worden geleend.
        - **Lenen**: Het proces waarbij een boek voor een bepaalde periode wordt meegenomen.
        - **Bibliothecaris**: Een persoon die verantwoordelijk is voor het beheer van de bibliotheekcollectie en die studenten helpt bij hun bibliotheekbehoeften.
        - **Student**: Een lid van de bibliotheek dat boeken kan lenen.
        - **Reservering**: Een handeling waarbij een boek dat momenteel niet beschikbaar is, wordt aangevraagd voor toekomstig gebruik.
2. **Objectgeoriënteerde analyse (OOA)**:
    - Identificeer de kernobjecten en beschrijf hun verantwoordelijkheden.
    - Voorbeeld (bibliotheekbeheersysteem):

Objecten kunnen zijn: Boek, Student, Bibliotheekmedewerker, Uitlening, Reservering

- Boek heeft eigenschappen zoals titel, auteur, beschikbaarheid.
- Student kan boeken lenen en reserveren.
- Uitlening registreert welke student welk boek op welk moment heeft.
1. **Functionele &amp; Niet-functionele Requirements (FURPS)**:
    - Stel de vereisten van jullie systeem op volgens het FURPS-model. Formuleer daarbij de functionele vereisten via de twee methoden die we in de les hebben gezien: in de vorm van user stories én in de vorm van use case descriptions.
    - Voorbeeld (Bibliotheekbeheersysteem):
        - Functionele vereisten – User Story

Als student wil ik boeken kunnen opzoeken op titel of auteur, zodat ik snel vind wat ik nodig heb.

- Functionele vereisten – Use Case Description

**Titel**: Boek lenen.

**Actoren**: Student, Bibliothecaris.

**Voorwaarden**: De student moet een geldige bibliotheekkaart hebben en het boek moet beschikbaar zijn.

**Normale stroom**: De student vraagt een boek te lenen, de bibliothecaris controleert of het boek beschikbaar is en de bibliothecaris verwerkt de uitleentransactie.

**Alternatieve stroom**: Als het boek niet beschikbaar is, wordt de student hiervan op de hoogte gesteld en kan hij het boek reserveren voor een later tijdstip.

**Na-voorwaarden**: Het boek wordt aan de student uitgeleend en de uitleengegevens worden bijgewerkt.

- Niet-functionele vereisten (URPS):

Gebruiksvriendelijkheid: De zoekfunctie moet intuïtief zijn en werken via een eenvoudige zoekbalk.

Betrouwbaarheid: Het systeem moet beschikbaar zijn met een uptime van minstens 99,5%.

Prestaties: Zoekresultaten moeten binnen 2 seconden worden weergegeven.

Ondersteuning: Het systeem moet logbestanden bijhouden van zoekopdrachten voor foutanalyse.

### **Te leveren resultaten:**

1. **Groepsopdracht**: Werk de onderstaande onderdelen uit op basis van de gekozen businesscase:
    1. **Glossary:** Een document met definities van de belangrijkste termen binnen het gekozen systeem.
    2. **Objectgeoriënteerde analyse (OOA):** Identificatie en beschrijving van de kernobjecten en hun verantwoordelijkheden binnen het systeem.
    3. **Requirements (FURPS-model):**
        1. Formuleer niet-functionele vereisten voor: **Bruikbaarheid, Betrouwbaarheid, Prestaties en Ondersteuning.**
        2. Formuleer de functionele vereisten op **twee manieren:**
            1. **Gebruikersverhalen**
            2. **Use case-beschrijvingen** (volg de [template](https://docs.google.com/document/d/1Rom4z8JSRlbvuR4MU-ZkgrXEXRAuaWkO/edit?usp=drive_link&ouid=105061193310403490033&rtpof=true&sd=true))

### 

### **Deel 2: Individuele onderzoekstaak – Use case diagram**

### **Opdracht (voor volgende les):**

Als voorbereiding doet elke student individueel onderzoek naar **Use Case Diagrams**.

Beantwoord in een korte samenvatting:

- Wat is een Use Case Diagram?
- Welke onderdelen bevat het (actoren, use cases, relaties)?
- Wat is het doel ervan in softwareontwikkeling?

**Toepassing:**

Teken een eigen **Use Case Diagram** op basis van de case die je groep gekozen heeft.

**Gebruik bij het opstellen je onderzoek als onderbouwing.**

### **Individueel in te leveren:**

- Een korte samenvatting van je bevindingen (±200 woorden).
- Een getekend Use Case Diagram (digitaal).

### **Beoordelingscriteria:**

- **Groepswerk:**
    - **Woordenlijst: Zijn de sleutelbegrippen correct en volledig gedefinieerd?**
    - **OOA: Zijn kernobjecten logisch gekozen en goed uitgewerkt?**
    - **Requirements: Zijn functionele en niet-functionele eisen helder en toepasbaar?**
    - **Use Case Descriptions: Zijn de beschrijvingen compleet, duidelijk en realistisch?**
- **Individueel werk:**
    - **Onderzoek Use Case Diagram: Begrijpt de student de structuur en functie van het diagram?**
    - **Tekenwerk: Bevat het diagram correcte onderdelen en is het toepasbaar op de gekozen case?**

[Parkeersysteem](https://www.notion.so/Parkeersysteem-27619744e6d380028c15d40ddd3a9dd4?pvs=21)