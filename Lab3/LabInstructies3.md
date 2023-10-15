# Lab 3 - Data samenbrengen uit meerdere bronnen

*Vereisten*

Om het lab te kunnen starten is het van belang dat je toegang hebt tot Power BI desktop.

*Doel*

In dit derde lab leer je Power Query in te zetten om data samen te voegen.

## Opdracht 1 - Samenvoegen van meerdere queries

1. Start een nieuw Power BI rapport en lees workbook **L3O1 - Bikes.xlsx** uit **Lab 3** in als Excel workbook (selecteer **Load**).

2. Lees **L3O1 - Accessories.xlsx** uit **Lab 3** in als Excel workbook en start Power Query Editor (Selecteer **Transform**).

3. Creëer een nieuwe query **Products** als reference van **Accessories**. 

4. Check dat de nieuwe **Products** query geselecteerd is, open in de **Home** tab het dropdown menu **Append Queries** en kies de transformatie **Append Queries**.

> Laten we de M code bekijken die voor de Reference en Append stappen is gegenereerd. 
> Als je de stap **Source** in het *Applied Steps* paneel bekijkt zie je daar de code `= Accessories`.
> Deze code staat voor de output van de query **Accessories**, het gevolg van de Reference transformatie.
> Als je in de **home** tab de **Advanced Editor** selecteert zie je daar de volgende code:
```
let
    Source = Accessories,
    #"Appended Query" = Table.Combine({Source, Bikes})
in
    #"Appended Query"
```
> Je ziet de twee stappen terug die we hebben toegevoegd, de Reference en de Append. 
> Voor de Append transformatie heeft Power Query de MM functie Table.Combine gebruikt, die de twee andere queries samenvoegt.
> Deze functie accepteert een lijst van queries (te zien aan de accolades) als input.
> Hetzelfde kun je voor elkaar krijgen door in het dropdown menu **Append Queries** te kiezen voor **Append Queries as New**.

5. Klik op **Close & Apply**, importeer **L3O1 - Clothing.xlsx** en **L3O1 - Components.xlsx** als nieuwe queries en start de Power Query Editor.

6. Selecteer query **Products**, open de **Advanced Editor** en breidt de lijst van tabellen in de functie `Table.Combine` uit met de nieuwe queries. De nieuwe code ziet er dan als volgt uit: `Table.Combine({Source, Bikes, Clothing, Components})`.

7. Sluit de Advanced Editor en check het resultaat van de querystap door te kijken of de vier categorieën beschikbara zijn in de filter control in de kolomkop van de kolom **ParentProductCategoryName**.

## Opdracht 2 - Samenvoegen van files uit een folder

Voor een beperkt aantal queries met dezelfde structuur zijn deze handmatige stappen goed uit te voeren. 
Dit wordt vervelend als je maandelijks een nieuwe file krijgt aangeleverd met bijvoorbeeld bijgewerkte budgetten.
Je wil hiervoor niet handmatig de query toevoegen en de lijst met gecombineerde queries bijwerken in Advanced Editor.
Gelukkig heeft Power Query daar een oplossing voor.

1. Pak de bestanden uit de zip **L3O3 - Products.zip** uit in de folder "C:\Data\L3\L3O2 - Products\".

2. Start een nieuw Power BI rapport en selecteer op de **Home** tab **Get Data** en selecteer onder de categorie **File** de bron **Folder**.

3. Navigeer naar de juiste folder met de bronbestanden voor **Lab 3**, klik op **Combine** en kies voor **Combine & transform Data**.

4. Seleceer in de **Combine File** dialoog die opent **Sheet1** en klik op OK.

> In het *Query Preview* paneel zie je in de eerste kolom **Source.Name** de filenaam staan. 
> Klik op de filter control van de kolom om te verifiëren dat alle files uit de folder zijn opgenomen.
> De filenaam kan interessant zijn om eventueel elementen uit af te leiden, zoals in dit geval de **Release Year**.
> Negeer voor nu de extra elementen die zijn toegevoegd in het *Queries* paneel, zoals de objecten in de folder **Helper Queries**.

5. Extraheer het jaartal uit **Source.Name** en hernoem het naar **Release Year**. Dit kan op verschillende manieren, bijvoorbeeld met **Replace Values** of **Split Column**. Als alternatief kun je ook **Column from Example** gebruiken op basis van **Source.Name**, de voorgestelde formule beoordelen en vervolgens **Source.Name** verwijderen.

> Wordt er een nieuwe file toegevoegd in de onderliggende folder, dan zal deze query die automatisch oppakken en hoeven er geen handmatige handelingen meer te worden uitgevoerd.
> Dit kun je simuleren door een van de files in de folder te kopiëren en te hernoemen tot **L3O2 - 2018.xlsx**.
> Ververs nu de preview door in de **Home** tab **Refresh Preview** te selecteren en bekijk het resultaat. Mooi toch?
