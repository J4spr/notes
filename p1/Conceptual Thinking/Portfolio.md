# groepsopdracht week 2

1. **Woordenlijst:**
    - **Beschikbaarheid:** aantal plekken die vrij zijn en nog niet gereserveerd zijn.
    - **Reservaties:** Parkeerplaatsen die gereserveerd zijn door anderen of die je zelf gereserveerd hebt.
    - **Parkeerbeheerder:** Persoon die verantwoordelijk is voor het beheer van reservaties.
    - **Medewerkers:** Personen die plekken kunnen reserveren en hun eigen reservaties beheren.
2. **Objectgeoriënteerde analyse (OOA):**
    - Parkeerplaats heeft als objecten nummer, status, verdieping, type en een boolean om na te kijken of hij is gereserveerd of niet.
    - Reservaties heeft de objecten datum en parkeertijd.
    - Parkeerbeheerder heeft dezelfde objecten als medewerker maar kan reservaties en de geschiedenis beheren door de boolean IsBeheerder die true is.
    - Medewerkers heeft de objecten naam en email, deze persoon zijn/haar voertuig wordt ook meegegeven bij het reserveren.
3. **Functionele & niet-functionele vereisten (FURPS)**:
    - **Functionele vereisten – User Story:**
        
        Als gebruiker wil ik kunnen zien welke parkeerplaatsen er vrij zijn en die kunnen reserveren.
        
        Als beheerder wil ik reservaties kunnen zien en wijzigen.
        
        Als gebruiker wil ik mijn eigen reservaties makkelijk terugvinden en eventueel wijzigen.
        
    - **Functionele vereisten – Use Case Description:**
        
        **Titel**: Vrije plaatsen
        
        **Actoren**: Beheerder, medewerkers
        
        **Voorwaarden**: Medewerker bij het bedrijf
        
        **Normale stroom**: De app checkt welke parkeerplekken vrij zijn en welke niet en toont deze anders.
        
        **Alternatieve stroom**: Als de parkeerplek bezet is kan je deze niet selecteren.
        
        **Na-voorwaarden:** De parkeerplek wordt als bezet weergegeven aan andere gebruikers en laat zien door wie het bezet is
        
    - **Niet-functionele vereisten (URPS):**
        
        - Bruikbaarheid:
            - De gebruikers moeten makkelijk gebruik kunnen maken van de app, oudere mensen moeten ook aan de app uitkunnen.
            - Er moeten ook extra toegankelijkheidsopties zijn voor kleurenblinde mensen zodat de kleur van een genomen parkeerplek en een vrije goed contrasteren.
        - Betrouwbaarheid:
            - De app mag niet crashen tijdens de openingsuren van het bedrijf aangezien de parkingsituatie dan uit de hand kan lopen.
        - Prestaties:
            - Het systeem moet snel reageren zodat medewerkers snel kunnen zien welke plekken vrij zijn en welke plekken al genomen zijn.
            - Het systeem moet het aantal medewerkers van het bedrijf aankunnen en in principe ook iets meer anders crasht het misschien vaak.
        - Ondersteuning:
            - De updates van de app moeten gebeuren wanneer het bedrijf gesloten is om zo zoveel mogelijk hinder te voorkomen.

### **Use Case-Beschrijvingen:**

|Use Case naam|Parkeren|
|---|---|
|Doel|De bestuurder wilt zijn voertuig achterlaten.|
|Actoren|Medewerker en beheerder|
|Precondities|De bestuurder is geregistreerd in het parkeersysteem.|
|Postcondities|Het voertuig is succesvol geparkeerd.|
|Trigger event/||
|Startgebeurtenis|De bestuurder wilt parkeren.|
|Hoofdsucces scenario (HSS)|1. De bestuurder komt aan de ingang aan.|

2. De nummerplaatherkenning scant de auto.
3. Slagboom opent.
4. Bestuurder rijdt garage binnen.
5. De bestuurder parkeert de auto.
6. Bareel gaat open.
7. Bestuurder rijdt weg. | | Alternatieve scenario’s | - Fout bij nummerplaatdetectie
8. Wanneer je aankomt is er een probleem met het systeem dat je nummerplaat controleert.
9. De parkeerbeheerder kan opnieuw gecontacteerd worden via de app en op die manier kan deze jou toch binnenlaten. |

|Use Case naam|Reserveren|
|---|---|
|Doel|Medewerker reserveert een parkeerplaats.|
|Actoren|Medewerker en beheerder|
|Precondities|Bestuurder moet 1 of meerdere tijdsloten selecteren.|
|Postcondities|Bestuurder heeft een parkeerplaats gereserveerd.|
|Trigger event/ Startgebeurtenis|Bestuurder wil een parkeerplaats hebben.|
|Hoofdsucces scenario (HSS)|1. Bestuurder opent de app.|

2. Bestuurder selecteert een plaats.
3. Systeem controleert of de parkeerplaats vrij is.
4. Bestuurder voert de begintijd in.
5. Systeem controleert of de parkeerplaats vrij is op dat uur.
6. Bestuurder voert eindtijd in.
7. Bestuurder vult voertuig gegevens in.
8. Systeem reserveert de parkeerplaats. | | Alternatieve scenario’s | - Tijdslot is niet vrij:
9. Bestuurder selecteert een andere parkeerplaats of een andere tijdslot.
10. Normale controles gaan verder.

- Voertuiggegevens komen niet overeen met de reservatie.

1. Bestuurder kan een beheerder contacteren.
2. Beheerder kan gegevens van de bestuurder controleren.
3. Beheerder kan nummerplaat aanpassen als gegevens overeenkomen.
4. Bestuurder kan parkeren. |

|Use Case naam|Over tijd|
|---|---|
|Doel|Bestuurders respecteren de gereserveerde tijdsloten.|
|Actoren|Medewerker|
|Precondities|Bestuurder moet geregistreerd zijn in het systeem met een geldig tijdslot.|
|Postcondities|Systeem stuurt een melding uit.|
|Trigger event/||
|Startgebeurtenis|De geregistreerde tijd is verstreken.|
|Hoofdsucces scenario (HSS)|1. Systeem controleert de tijd van de geparkeerde auto.|

2. Systeem detecteert dat de gereserveerde tijd is verstreken.
3. Bestuurder ontvangt een melding in de app. | | Alternatieve scenario’s | - Bestuurder heeft de parkeerplaats verlengd via de app:
4. Systeem herkent de verlenging.
5. Er word geen melding gestuurd. |

|Use case naam|Geschiedenis|
|---|---|
|Doel|Beheerder wilt kijken naar de geschiedenis van alle reservaties en parkeerplekken.|
|Actoren|Beheerder|
|Precondities|De beheerder wil de geschiedenis reserveringen bekijken.|
|Postcondities|Toon de hele geschiedenis|
|Trigger event/ Startgebeurtenis|Beheerder opent zijn dashboard in de app.|
|Hoofdsucces scenario (HSS)|1. Beheerder navigeert naar de parkeergeschiedenis pagina.|

2. Het parkeersysteem laat de geschiedenis zien.
3. Beheerder kan filteren op alle tabellen. | | Alternatieve scenario’s | De medewerker is geen beheerder waardoor hij de geschiedenis niet kan zien. |

|Use Case naam|**Medewerker annuleert reservering**|
|---|---|
|Doel|Medewerker wilt een reservering annuleren|
|Actoren|Medewerker|
|Precondities|Reservering bestaat al voor deze medewerker en medewerker is ingelogd|
|Postcondities|Reservering wordt verwijderd en de parkeerplaats is opnieuw beschikbaar|
|Trigger event/||
|Startgebeurtenis|Medewerker annuleert de reservering via de app|
|Hoofdsucces scenario (HSS)|1. Medewerker opent het parkeersysteem app.|

2. Medewerker selecteer de reservering dat hij wilt annuleren.
3. Medewerker kiest de optie om te annuleren.
4. Het systeem vraagt als de Medewerker zeker is.
5. Medewerker bevestigt de actie.
6. Het systeem annuleert de reservering en markeerd parkeerplaats opnieuw als beschikbaar. | | Alternatieve scenario’s | - Annuleren is mislukt door systeemfout:
7. Het systeem toont een foutmelding. **2. Medewerker kan later opnieuw proberen of een beheerder contacteren. 


# Week 3

## User stories:

### Medewerker:

- Als medewerker wil ik kunnen inloggen om toegang te krijgen tot deze software.
- Als medewerker wil ik kunnen zien welke plaatsen er vrij zijn.
- Als medewerker wil ik een parking kunnen reserveren.
- Als medewerker wil ik mijn eigen reservaties kunnen beheren.
- Als medewerker wil ik een probleem in de software kunnen melden.

### Parkeerbeheerder:

- Als parkeerbeheerder wil ik reservaties kunnen beheren.
- Als parkeerbeheerder wil ik problemen kunnen oplossen.

## Map

![map](assets/map.png)

## **Use case diagram:**

![use case](assets/use_case.png)

## **Activity diagram:**

![activity diagram](assets/activity.png)

## **WireFrames:**

![Wireframes](assets/wireframes.png)

# Week 4

## Bedrijfsregels:

### **Beheer en onderhoudsregels:**

- Als er incidenten zijn gebeurd of een medewerker is iets kwijt, moet dit meteen gemeld worden aan de parkeerbeheerder.
- Wanneer een medewerker dit bedrijf verlaat, worden zijn/haar rechten om parkeerplaatsen te reserveren ingetrokken.
- Beheerders kunnen reservaties wijzigen en verwijderen. Ze kunnen ook parkeerplaatsen tijdelijk op “Niet beschikbaar” zetten indien hier werken aan zijn.

### Beveiliging en toegangsregels:

- De toegang tot de parking gebeurt via personeelsbadge of kentekenherkenning.
- Medewerkers kunnen hun reservatie ten laatste 1 uur voor de gereserveerde tijd hun reservatie wijzigen of annuleren.
- Medewerkers met een handicap statuut kunnen speciale handicap parkeerplaatsen reserveren.
- Parkeerplaatsen voor elektrische auto’s kunnen gebruikt door mensen met elektrische wagens.
- De parking is voorzien van camera’s zowel in de parking als bij de ingang van de parking.
- Als er bezoekers langs komen moet dit worden gemeld aan de parkeerbeheerder die hen dan een parkeerplek kan toewijzen. Ze kunnen dan gedurende een bepaalde tijd mee op de parking staan.
- Medewerkers mogen alleen op de parking staan indien ze aan het werken zijn. Het is niet toegestaan om hier geparkeerd te staan voor privé voordelen.
- LPG auto’s mogen niet ondergronds parkeren, deze zijn verplicht om bovengronds te parkeren.

## Interpretaties:

Wij zijn er van uitgegaan dat de parking een ondergronds en bovengronds deel heeft , op basis daarvan maken we onderscheid tussen de brandstoftypes van de wagens. Een LPG wagen mag op de meeste ondergrondse parkeergarages niet binnen. Elektrische auto’s hebben ook hun eigen plekken zodat ze kunnen opladen. We zijn er ook van uit gegaan dat medewerkers niet moeten betalen voor de parking aangezien ze werken voor het bedrijf en daar moeten zijn. Medewerkers kunnen ook parkeren zonder reservatie wanneer de status van de parkeerplek “vrij” is, ze kunnen dan binnen zolang er plek is en met hun badge.



![busness case](assets/business_case.png)

# Week 5

## oud conceptueel class diagram

![class diagram](assets/oud_class_diagram.png)
## nieuw conceptueel class diagram

![class diagram](assets/nieuw_class_diagram.png)
## Wat en waarom gewijzigd

We hebben enumeratieklassen toegevoegd om op voorhand een aantal attributen vaste opties te geven. We hebben Beheerder ook een subklasse gemaakt van medewerkers zodat deze dezelfde attributen heeft als medewerkers maar wel extra opties. We hebben ook een klasse voortuig toegevoegd zodat je de voortuig informatie al hebt en deze niet meer moet ingeven bij het maken van de reservatie. We hebben een veel op veel relatie tussen medewerkers en voertuig zodat meerdere medewerkers hetzelfde voertuig kunnen gebruiken , denk dan bv. aan een koppel dat afwisselend de wagen gebruikt. We hebben ook een extra attribuut “brandstoftype” toegevoegd om zo te kunnen filteren op waar de auto mag staan. LPG wagens mogen bv niet in een ondergrondse parking. we hebben ook een klasse geschiedenis toegevoegd zodat de parkeerbeheerder kan zien wie welke parkeerplek heeft gebruikt op welke datum en tijdstip indien er een probleem is.

## Welke en waarom bedrijfsregels en modelering inzichten toegepast

- Bedrijfsregels:
    - LPG- wagens mogen niet ondergronds parkeren vastgelegd via notitie → Om veiligheidsregel duidelijk te maken.
    - Parkeerplaats enkel gebruiken door voertuigen met de overeenkomstige brandstof → Om ervoor te zorgen dat alleen elektrische auto’s op de plaatsen met laadpalen mogen staan.
    - Enkel medewerkers en de beheerder kunnen reservaties maken → Om ervoor te zorgen dat mensen buiten het bedrijf geen reservaties kunnen maken.
    - Beheerder kan de reservaties beheren en de geschiedenis bekijken → Om verschil te laten zien tussen een normale medewerker en de beheerder.
- Modelering inzichten:
    - Enumeraties voor brandstofType, type, reserveringsstatus en tijdslot → Zodat de medewerker alleen keuze heeft tussen bepaalde opties.
    - Generalisatie voor beheerder door gebruik te maken van medewerker → Om herhaling te beperken.
    - Cardinaliteiten zoals “Reservering 1 - 0..* Geschiedenis” → Om aan te geven hoeveel relaties tussen de klassen zijn.
    - Boolean's voor beheerder en parkeerplaats → Om aan te geven of iets is of niet
    - Notitie “LPG mag niet in een ondergrondse parking” → Om een regel te laten zien

