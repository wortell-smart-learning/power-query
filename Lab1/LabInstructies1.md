# Lab 1 - Een eerste blik op Power Query

*Vereisten*

Om het lab te kunnen starten is het van belang dat je toegang hebt tot Power BI desktop.

*Doel*

In dit eerste lab importeer je de eerste data als query en passen we eenvoudige transformaties toe om het te visualiseren.

## Opdracht 1 - De eerste query

1. Start een nieuw Power BI rapport.

2. Selecteer onder de tab **Home** het dropdown menu **Get Data** en selecteer **Excel**. Als alternatief kun je op **Get Data** klikken. De **Get Data** dialoog opent, waarna je alle beschikbare brontypen (of connectoren) kunt bekijken. Je kunt de zoekbalk gebruiken om gericht te zoeken. Als je klaar bent, selecteer dan Excel.

3. In de **Import Data** dialoog die opent, navigeer naar **Lab1** en selecteer workbook **L1O1.xlsx**. Druk op Enter of selecteer **Open** om de dialoog te sluiten.

4. Selecteer in het **Navigator** scherm dat opent de tabel die je wil importeren. Deze dialoog opent altijd als je verbinding maakt met een databron die meerdere tabellen bevat. Als je verbinding maakt met relationele databases, zoals Azure SQL database, bevat het linkerpaneel meer opties. Het grootste deel van de user interface ziet er echter hetzelfde uit. 

> Je ziet dat **Load** de default keuze is in deze dialoog en niet **Transform Data**. Gebruikers die de default flow volgen zijn wellicht niet op de hoogte van Power Query. Door **Load** te selecteren sla je de datapreparatie over en laad je de tabel zoals die is.   
> Zelfs als jouw data er goed uitziet is het aan te raden om **Transform Data** te selecteren. Dit opent de Power Query Editor, waarin je jouw data kunt bekijken, analyseren en vaststellen dat het in het verwachte formaat staat.

5. Selecteer **Sheet1** en dan **Transform Data**. De Power Query Editor opent. Dit is een goed moment om te kijken of je alle componenten van de interface kunt vinden. Als je de **Formula bar** niet ziet, kun je die activeren door naar de **View** tab te gaan en **Formula bar** te selecteren. Voortaan zal die dan zichtbaar zijn.

6. In het *Queries* paneel, hernoem de query **Sheet1** naar **Products**. Dit kan door op de query te dubbelklikken. Dit kan ook door in het *Query Settings* paneel in de properties de **Name** aan te passen.

## Opdracht 2 - De eerste transformatie

> In het *Preview* paneel zie je dat de laatste twee kolommen **Cost** en **Price** zijn. Stel dat je een nieuwe kolom wilt toevoegen voor de Profit die de Cost van de Price aftrekt. Om een nieuwe kolom toe te voegen die is gebaseerd op een berekening op twee andere kolommen, zul je eerst de twee kolommen moeten selecteren. Om een kolom te selecteren kun je de kolomkop in het *Preview* paneel selecteren. Om meerdere kolommen te selecteren kun je de Shift toets gebruiken voor aangrenzende kolommen of de Ctrl toets voor niet aangrenzende kolommen.

1. Selecteer de kolom **Price**. Selecteer dan met behulp van Shift of Ctrl de kolom **Cost**.

2. Om een nieuwe kolom toe te voegen, zoek de relevante transformatie in de **Add column** tab. Ga naar **Add Column**, bekijk de verschillende opties en selecteer dan **Standard**. Je ziet nu de verschillende rekenkundige transformaties waarop je de nieuwe kolom kunt baseren. Selecteer **Subtract** in het drop-down menu.

3. Als de kolom is toegevoegd in het *Preview* paneel, hernoem het dan naar **Profit**. Om een kolom te hernoemen kun je op de kolomkop dubbelklikken. Je kunt **Rename** ook terugvinden als een van de verschillende transformatieopties als je rechtsklikt op de kolomkop.

4. Bekijk de waarden in de kolom **Profit**. Die zouden positief moeten zijn. Zijn ze negatief, dan ligt dat aan de volgorde waarin je de kolommen hebt geselecteerd in stap 2. Om dat aan te passen moeten we de volgende stappen doorlopen:
  - Kijk naar het *Applied Steps* paneel aan de rechterkant van de Power Query Editor. Hier staan alle stappen die zijn gegenereerd. Je kunt elke stap selecteren en de output zien in het *Preview* paneel. Die data is niet opgeslagen, maar een cache preview van de werkelijke data.
  - Selecteer de stap **Inserted Subtraction** in **Applied Steps**.
  - Zoek in de formule in de **Formula bar** naar de volgende code: [Cost] - [Price] en vervang het door [Price] - [Cost]. De volledige formule ziet er nu als volgt uit: \
    = Table.AddColumn(#"Changed Type", "Subtraction", each [Price] - [Cost], Int64.Type)

> Nu we net beginnen met Power Query is het nog niet nodig de syntax in de formula bar te begrijpen. Deze formule is deel van de M taal. In de loop van de training gaan we leren wanneer en hoe deze formules aan te passen, zonder een expert te zijn in de M syntax.

5. Verwijder de **Product Number** kolom door de kolom te selecteren en op de **Delete** toets te drukken. Je kunt ook in de **Home** tab **Remove Columns** selecteren.

6. Probeer de data te filteren. Stel dat je alleen de rijen over wilt houden die de tekst **Mountain** bevatten. Om dit te doen, selecteer je de filter control in de kolomkop van de kolom **Product**. In het filterpaneel dat opent staan de verschillende producten. Selecteer **Text Filters** en dan **Contains...**. Vul in de **Filter Rows** dialoog die opent "Mountain" in en klik op OK.

> Standaard behandelt Power Query tekst op een case-sensitive manier. Als je "mountain" invult bij stap 6 is de resultaatset leeg. Om een case-insensitive filter toe te passen kun je de M formule aanpassen. De originele formule ziet er als volgt uit:
> = Table.SelectRows(#"Removed Columns", each Text.Contains([Product], "Mountain"))
> Door Comparer.OrdinalIgnoreCase toe te voegen als derde argument aan de Text.Contains functie kunnen we een case-insensitive filter toepassen. De M formule ziet er dan zo uit:
> = Table.SelectRows(#"Removed Columns", each Text.Contains([Product], "mountain", Comparer.OrdinalIgnoreCase))
> Misschien ben je bezorgd dat deze aanpassing op dit moment nog te geavanceerd is, maar de meeste uitdagingen in datapreparatie kun je af zonder de formules te hoeven aanpassen. In een aantal gevallen kan zo'n aanpassing handig zijn, maar je hoeft niet de complete M syntaxt te kennen.

7. Laad tenslotte de query naar het rapport. Selecteer **Close & Apply** in de **Home** tab. Bouw een eenvoudige visualisatie op de getransformeerde tabel. 

## Opdracht 3 - De data bewerken

1. Open het bronbestand **L1O1.xlsx** en doe wat aanpassingen. Ververs, nadat je de file hebt opgeslagen, jouw rapport en kijk hoe jouw query omgaat met de gewijzigde data. Om de query te verversen, selecteer **Refresh** in de **Home** tab. Dit is de kern van automatisering en een tijdsbesparend element in Power Query. Je kunt de data eenmalig prepareren en dan een refresh starten om de data automatisch te prepareren op elk moment.

> Je kunt de verversing van de data ook periodiek inplannen als je gebruik maakt van de Power BI service. Lees er meer over in de [documentatie](https://learn.microsoft.com/en-US/power-bi/connect-data/refresh-scheduled-refresh).

2. Bewerk de query aan de hand van de volgende stappen
   - Selecteer **Transform Data** in de **Home** tab.
   - Selecteer een van de bestaande stappen in **Applied Steps**, pas het aan of verwijder ze en voeg nieuwe stappen toe. Om een stap toe te voegen tussen bestaande stappen, selecteer de stap waarna de nieuwe stap moet komen en selecteer een transformatiestap uit het lint of na rechtklikken op een kolomkop.

Je hebt nu de originele brontabel geïmporteerd en getransformeerd. Het rapport met de oplossing is hier te downloaden.


## Table of Contents

1. [Lab 1 - Een eerste blik op Power Query](../Lab1/LabInstructies1.md)
2. [Lab 2 - Datapreparatie uitdagingen](../Lab2/LabInstructies2.md)
3. [Lab 3 - Data samenbrengen uit meerdere bronnen](../Lab3/LabInstructies3.md)
4. [Lab 4 - Combineren van afwijkende tabellen](../Lab4/LabInstructies4.md)
