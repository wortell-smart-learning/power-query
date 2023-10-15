# Lab 4 - Combineren van afwijkende tabellen

*Vereisten*

Om het lab te kunnen starten is het van belang dat je toegang hebt tot Power BI desktop.

*Doel*

In dit vierde lab leer je Power Query in te zetten om data samen te voegen uit tabellen waarvan de opmaak verschilt.

## Opdracht 1 - Combineren van afwijkende tabellen, de reactieve aanpak

In het vorige lab heb je data samengevoegd uit meerdere bronnen. 
Een onuitgesproken aanname was echter dat al die bronnen dezelfde structuur hadden.
Bij het samenvoegen van data uit verschillende tabellen loop je soms tegen verschillen aan in de structuur. 
Zowel de kolomnamen als de volgorde kunnen afwijken.
Ook kan door handmatig ingrijpen of falen de structuur in de loop van de tijd veranderen.
In zo'n geval worden afwijkende kolommen in een samengevoegde query alleen gevuld vanuit één databron.
De rijen vanuit andere databronnen zullen leeg gelaten worden.
Het kan ook voorkomen dat kolommen uit de tweede databron worden genegeerd, waardoor data ontbreekt.
In dit lab leer je de oplossing voor deze issues.


1. Start een nieuw Power BI rapport en lees workbook **L4O1 - Bikes.xlsx** uit **Lab 4** in als Excel workbook (selecteer **Load**).

2. Lees **L4O1 - Accessories.xlsx** uit **Lab 4** in als Excel workbook en start Power Query Editor (Selecteer **Transform**).

3. Creër een nieuwe query waarin beide queries worden samengevoegd (**Append Queries as New**).

> Als je de preview bekijkt van de nieuwe query zie je zowel de kolommen **StandardCost** uit **Accessories** als **Cost** uit **Bikes** met de resulterende lege waarden.
> Het is je misschien opgevallen dat je de categorie kwijt bent na de samenvoeging. 
> In een later lab bekijk je hoe je die context kunt behouden.

4. Selecteer de **Accessories** query en hernoem de kolom **StandardCost** tot "Cost". Controleer het gevolg in query **Append1**.

> In dit geval is handmatig bijwerken een snelle oplossing. 
> Some is dit echter niet haalbaar, bijvoorbeeld bij een groot aantal kolommen, of als je de opmaak van de aanlevering niet in de hand hebt. 
> En als je een folder als input gebruikt, dan werkt handmatig hernoemen van kolommen niet meer, zoals je straks ziet.

## Opdracht 2 - Demonstratie van het symptoom van ontbrekende waarden

1. Pak de bestanden uit de zip **L4O2 - Products.zip** uit in de folder "C:\Data\L4\L4O2 - Products\". Bekijk de bestanden en merk de verschillende kolomkoppen op.

2. Start een nieuw Power BI rapport en selecteer op de **Home** tab **Get Data** en selecteer onder de categorie **File** de bron **Folder**.

3. Navigeer naar de juiste folder met de bronbestanden voor **Lab 4**, klik op **Combine** en kies voor **Combine & transform Data**.

4. Selecteer in de **Combine File** dialoog die opent één van de opties in het dropdown menu **Sheet1** en klik op OK.

> De keuze die je maakt bepaalt de kolomnamen voor de gecombineerde query.

5. Scroll in het *Preview Query* paneel naar beneden tot de **Accessories** overgaan in de **Bikes**. Merk op dat de kolommen **Product**, **StandardCost** en **ListPrice** lege waarden bevatten.

> Om dit issue te verhelpen moet je aan de slag met de sample query. 

6. Selecteer in het *Queries* paneel de **Transform Sample File**. Deze bevat de file die je bij het inlezen van de folder als voorbeeld hebt geselecteerd en laat diens data correct zien.

> Bij het combineren van files uit een folder maakt Power Query verschillende artefacten aan: een query function, een sample query, een file query en een parameter.
> De transformatie voor elke file staat in de functie. Om deze transformatie te wijzigen kun je de sample file aanpassen. 
> Deze aanpassingen worden dan doorgevoerd in de functie en toegepast op alle files. 
> Als je files uit een folder combineert, zoek dan de **Transform Sample File** om aanpassingen op elke file te doen, voordat ze worden samengevoegd.

## Opdracht 3 - Aanname van gelijke volgorde en het generaliseren van de kolomkoppen

Om het issue van de ontbrekende waarden op te lossen mag je aannemen dat de kolomvolgorde in de files hetzelfde is.
Door deze aanname kun je generieke kolomkoppen gebruiken, zoals Column1, Column2 enz. en de kolomvolgorde gebruiken om de tabellen correct samen te voegen.

1. Selecteer in het *Queries* paneel de **Transform Sample File** en hernoem het tot "Products Sample".

2. Verwijder de laatste stap **Promoted Headers**.

> Door de generieke kolomnamen kun je de correcte data in de samengevoegde tabel zien.

3. Selecteer de query **L4O2 - Products** en merk de volgende foutmelding op: `Expression.Error: The column 'Product' of the table wasn't found.`

4. Verwijder de laatste stap: **Changed Type**. Nu heeft de samengevoegde tabel geen ontbrekende waarden meer.

5. Je kunt nu de eerste rij als kolomkoppen gebruiken (**Use First Row as Headers**).

> De kolomkoppen van de andere tabellen staan nog steeds als rijen in de data. Eerder heb je die eruit gefilterd, maar hadden ze dezelfde naam.
> Nu is dat niet het geval. Je kunt de rij met kolomkoppen eenvoudiger herkennen door voor het samenvoegen een index aan de data toe te voegen.

6. Selecteer de query **Products Sample**. Selecteer op de **Add Column** tab de transformatie **Index Column**. Voor elke file zal de rij met kolomkoppen de waarde 0 hebben in deze index.

7. Ga terug naar de query **L4O2 - Products** en filter de rijen met kolomkoppen uit de dataset.

8. Verwijder de eerste en laatste kolom. Maak de query robuuster door in de formule van deze **Removed Columns** stap de harde verwijzing naar `"L4O2 - Accessories.xlsx"` te vervangen door `Table.ColumnNames(#"Filtered Rows"){0}`.

> Je kunt nu de query laden naar het rapport om de analyse te starten.

## Opdracht 4 - Eenvoudige normalisatie d.m.v. Table.TransformColumnNames

Als je niet kunt aannemen dat de kolomvolgorde hetzelfde is voor al je bestanden, dan is normalisatie van kolomnamen een krachtige tool.
Het is in principe niet meer dan tekstmanipulatie, maar in veel gevallen is dat voldoende om formats van kolomnamen consistent te maken.
Omdat Power Query case sensitive is, kan het toepassen van lowercase, uppercase of capitalizatie een effectieve stap zijn.
Als je tabellen vaak veranderen en de kolomnamen van lowercase naar uppercase veranderen en vice versa, dan zal het uniformeren van de case afwijkingen beperken.

Om kolomnamen te bewerken heb je de M functie Table.TransformColumnNames tot je beschikking. 
Als de laatste stap in de Applied Steps bijvoorbeeld **Vorige stap** heet, dan kun je capitalisatie toepassen met de volgende formule:
`= Table.TransformColumnNames(#"Vorige stap", Text.Proper)`
En je kunt underscores door spaties vervangen:
`= Table.TransformColumnNames(#"Vorige stap", each Replacer.ReplaceText(_,"_"," "))`

In deze opdracht zul je beide formules gaan toepassen bij het samenvoegen van AdventureWorks Producttabellen.

1. Pak de bestanden uit de zip **L4O4 - Products.zip** uit in de folder "C:\Data\L4\L4O4 - Products\". 

> Deze bestanden lijken op de bestanden uit opdracht 2, met kleine verschillen. De kolomkoppen kunnen geuniformeerd worden door te capitaliseren en underscores te vervangen. Daarnaast zijn in **Bikes** de eerste twee kolommen omgewisseld.

2. Start een nieuw Power BI rapport en selecteer op de **Home** tab **Get Data** en selecteer onder de categorie **File** de bron **Folder**.

3. Navigeer naar de juiste folder met de bronbestanden voor **Lab 4**, klik op **Combine** en kies voor **Combine & transform Data**.

4. Selecteer in de **Combine File** dialoog die opent één van de opties in het dropdown menu **Sheet1** en klik op OK.

> Check dat de resulterende query inderdaad leidt onder het symptoom van ontbrekende waarden.

5. Selecteer de **Transform Sample File** en hernoem het tot "Products Sample". Klik dan op het Fx icoon in de *Formula bar*.

> Er wordt een nieuwe stap toegevoegd, **Custom1**, die de volgende formule laat zien: `= #"Promoted Headers"`. 
> Dit is de variabele die verwijst naar de output van de vorige stap, **Promoted Headers**.
> Omdat deze variabele de tabel met afwijkende kolomnamen teruggeeft, kun je de functie `Table.TransformColumnNames` erop toepassen met argument `Text.Lower` om kleine letters van de kolomnamen te maken.

6. Wijzig de formule in: `= Table.TransformColumnNames(#"Promoted Headers", Text.Lower)` en druk op Enter. Merk op dat de kolomnamen er nu in kleine letters staan. 

> Als kolomnamen beginnend met hoofdletters jouw voorkeur hebben, vervang `Text.Lower` dan door `Text.Proper`.
> Je kunt deze transformatie ook toepassen als de kolomnamen van jouw huidige datasets consistent zijn, om problemen in de toekomst te voorkomen.

7. Klik opnieuw op het Fx icoon in de *Formula bar* en wijzig de formule van stap **Custom2** naar `= Table.TransformColumnNames(#"Custom1", each Replacer.ReplaceText(_,"_"," "))`.

8. Klik op Enter en merk op dat de kolomnamen nu spaties bevatten in plaats van underscores. Ze zien er nu gebruiksvriendelijker uit.

9. Selecteer nu query **L4O4 - Products** en verwijder de laatste stap, **Changed Type**. De bestanden zijn nu correct samengevoegd en er zijn geen onverwachte ontbrekende waarden meer.

