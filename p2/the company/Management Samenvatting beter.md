> [!SUMMARY] Examenoverzicht Management Accounting
> Deze samenvatting bevat de theorie en de methodes voor de oefeningen die je moet kennen, gebaseerd op de opgegeven leerstof en jouw specifieke cheat-sheet voor financiële formules.

---

# THEORIE (5 Punten)

## 1. Vaste en Variabele kosten
- **Vaste kosten (FK):** Kosten die niet direct veranderen naarmate het productie- of verkoopvolume stijgt of daalt. 
  *Belangrijk theorie-inzicht:* Vaste kosten blijven in de praktijk niet *eeuwig* constant. Als de productie zo sterk toeneemt dat de capaciteit moet worden uitgebreid, dan zullen de vaste kosten stapsgewijs toenemen.
- **Variabele kosten (VK):** Kosten die rechtstreeks veranderen met het productie- of verkoopvolume. 
  *Belangrijk theorie-inzicht:* Variabele kosten hebben niet altijd een lineair verloop. 
  - **Degressief:** Bij bedrijfsgroei kan de kost per eenheid dalen door schaalvoordelen of specialisatie.
  - **Progressief:** Als het bedrijf nóg groter wordt, kan de productie minder efficiënt worden, waardoor de variabele kosten sneller oplopen.

## 2. ERP Systeem
> [!INFO] Wat is een ERP?
> **Enterprise Resource Planning (ERP)** is een geïntegreerd softwareprogramma dat binnen organisaties wordt gebruikt ter ondersteuning van bedrijfsprocessen.
> - **Ondersteunde processen:** Een ERP helpt bij het stroomlijnen van logistiek, voorraadbeheer, financiën, HR en sales.
> - **Opbouw:** Een ERP-programma is opgebouwd uit verschillende kleinere deelprogramma’s of "modules" die met elkaar verbonden zijn.

---

# OEFENINGEN (15 Punten)

## 1. Break-evenanalyse
Het break-even (BE) punt is het volume waarbij de totale inkomsten exact gelijk zijn aan de totale kosten. De winst is dan 0.

> [!FORMULA] Belangrijkste formules Break-even
> **Contributiemarge per eenheid**
> $$ \text{Contributie per E} = VP - VK\text{ per E} $$
>
> **Break-even Afzet (in eenheden)**
> $$ E_{BE} = \frac{\text{Vaste Kosten (FK)}}{VP - VK\text{ per E}} $$
>
> **Break-even Omzet (in Euro)**
> $$ \text{BE Omzet} = E_{BE} \times VP $$

**Winstobjectief (Target Profit):**
Als je een bepaalde winst wil bereiken, tel je dit op bij de vaste kosten.
$$ \text{Afzet} = \frac{FK + \text{Winst vóór belasting}}{VP - VK\text{ per E}} $$
*Let op belastingen:* Als je een winst *na* belasting (netto) krijgt, moet je deze eerst omzetten naar winst vóór belasting (bruto): $\text{Winst vóór belasting} = \frac{\text{Winst na belasting}}{1 - \text{belastingvoet}}$.

## 2. Special Order
Je krijgt de kans om een eenmalig order te accepteren tegen een **lagere verkoopprijs**. 

> [!WARNING] Beslissingsregel
> Aanvaard het order als: **Variabele kost < Speciale Verkoopprijs**. De contributiemarge van het speciale order moet positief zijn.

- **Vaste kosten negeren:** De vaste kosten worden al gedekt door de reguliere verkoop en wijzigen niet door het extra order, neem deze dus *niet* mee in je berekening.
- **Voorwaarden om te aanvaarden:** 
  1. Je hebt overcapaciteit.
  2. Het is een eenmalig order.
  3. Er is sprake van gescheiden markten (zodat je reguliere klanten niet ook de lagere prijs eisen).

## 3. Make or Buy
Kies je ervoor om een product zelf te maken (Make) of aan te kopen bij een leverancier (Buy)? Je kijkt hierbij **enkel naar differentiële kosten en opbrengsten**. 

*   Kosten die toch blijven bestaan (zoals algemene afschrijvingen of huur) laat je buiten beschouwing.

**Twee situaties:**
1. **Vrijgekomen capaciteit wordt NIET benut:** 
   Vergelijk de wegvallende productiekosten met de nieuwe aankoopkosten. Is de aankoop goedkoper dan de wegvallende (variabele) productiekosten? Dan "Buy". Anders "Make".
2. **Vrijgekomen capaciteit wordt WEL benut (Opportuniteitskost):**
   Tel de *extra winst/omzet* die je kan maken met de vrijgekomen capaciteit op bij het voordeel van het aankopen.

## 4. Cash Flow
Kasstromen (cash flows) zijn niet hetzelfde als boekhoudkundige stromen (resultatenrekening). Het grote verschil zit in de **timing**.

> [!CHECK] Kasstroom vs. Resultatenrekening
> - **Investeringen:** De volledige aankoop (uitgave) valt direct in het jaar van aankoop bij de kasstroom.
> - **Afschrijvingen & Waardeverminderingen:** Dit zijn boekhoudkundige kosten (voor de resultatenrekening), maar **GEEN kaskosten**. Deze mag je in een kasstroomplanning nooit als uitgave aftrekken!
> - **Leningen:** De kapitaalaflossing en intresten zijn beiden een *uitgave* in de kasstroom. In de resultatenrekening is enkel de intrest een kost.

## 5. Tijdswaarde van Geld (Sparen & Biedingen)
Hieronder vind je het exacte formularium voor de tijdswaarde van geld (inclusief het omzetten van rentes en het actualiseren van kasstromen), zoals voorgeschreven op jouw cheat-sheet.

> [!FORMULA] Tijdswaarde formules (Cheat-Sheet)
> **Enkelvoudige bedragen:**
> $$ K_{t \text{ met } t=1} = K_0 \times (1+r) $$
> $$ K_0 = \frac{K_{t \text{ met } t=1}}{(1+r)} $$
> $$ K_n = K_0 \times (1+r)^n $$
> $$ K_0 = \frac{K_{t \text{ met } t=n}}{(1+r)^n} $$
>
> **Omzetten van rentevoeten (jaarrente $r_j$ naar kwartaal $r_k$, maand $r_m$ of dag $r_d$):**
> $$ \sqrt{(1+r_j)} - 1 = r_k $$
> $$ \sqrt{(1+r_j)} - 1 = r_m $$
> $$ \sqrt{(1+r_j)} - 1 = r_d $$
>
> **Verband tussen Present Value (PV) en Future Value (FV):**
> $$ PV_{k,n,r} = \frac{FV_{k,n,r}}{(1+r)^n} $$
> $$ FV_{k,n,r} = PV_{k,n,r} \times (1+r)^n $$
> 
> **Annuïteiten (Reeksen - extra varianten):**
> $$ FV_{(k,n,r)} = k \times \frac{(1+r)^n}{r} - k \times \frac{1}{r} $$
> $$ k = PV \times \frac{r}{[1 - (1+r)^{-n}]} $$
>
> **Formules die je standaard krijgt bij het examen (Annuïteiten):**
> $$ FV_{(k,n,r)} = k \times \frac{(1+r)^n - 1}{r} $$
> $$ PV_{(k,n,r)} = k \times \left[ \frac{1 - (1+r)^{-n}}{r} \right] $$
> $$ PV_{(k,n,r)} = k \times \left[ \frac{1}{r} - \frac{1}{r \times (1+r)^n} \right] $$

**Biedingen vergelijken:** 
Als je moet kiezen tussen biedingen met betalingen verspreid over de tijd, moet je alles "actualiseren" naar de waarde van vandaag (Jaar 0) met de *Present Value* ($K_0$ of $PV$) formules. Degene met de hoogste waarde in Jaar 0 is het beste bod.

## 6. Evaluatietechnieken voor Investeringen
Er zijn verschillende manieren om te bepalen of een project (investering) de moeite waard is. 

**Gebaseerd op Kasstromen (Cash flows):**
- **Net Present Value (NPV):** De actuele (geactualiseerde) waarde van alle toekomstige inkomsten en uitgaven minus de initiële investering. NPV > 0 = goed project.
- **Internal Rate of Return (IRR):** De intrestvoet (r) waarbij de NPV exact nul is.
- **Payback Period (PB) / Discounted Payback Period (DPB):** De terugverdientijd in jaren. DPB houdt daarbij ook rekening met de tijdswaarde van het geld (verdisconteerde kasstromen).

**Gebaseerd op Boekhoudkundige stromen (Resultatenrekening):**
- **Return on Investment (ROI) & Accounting Rate of Return (ARR):** Hierbij moet je wél de afschrijvingen als kosten in rekening brengen (in tegenstelling tot bij NPV/IRR).

**Kwalitatieve beoordeling:**
- **Score matrix model:** Beoordeelt investeringen niet alleen op financiële return (ROI), maar gebruikt wegingsfactoren om ook te scoren op niet-financiële factoren zoals: *Strategische fit*, *Concurrentievoordeel*, *Organisatierisico* en *Management informatie*.