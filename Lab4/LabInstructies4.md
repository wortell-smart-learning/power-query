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

4. Seleceer in de **Combine File** dialoog die opent één van de opties in het dropdown menu **Sheet1** en klik op OK.

> De keuze die je maakt bepaalt de kolomnamen voor de gecombineerde query.

5. Scroll in het *Preview Query* paneel naar beneden tot de **Accessories** overgaan in de **Bikes**. Merk op dat de kolommen **Product**, **StandardCost** en **ListPrice** lege waarden bevatten.

> Om dit issue te verhelpen moet je aan de slag met de sample query. 

6. Selecteer in het *Queries* paneel de **Transform Sample File**. Deze bevat de file die je bij het inlezen van de folder als voorbeeld hebt geselecteerd en laat diens data correct zien.

> Bij het combineren van files uit een folder maakt Power Query verschillende artefacten aan: een query function, een sample query, een file query en een parameter.
> De transformatie voor elke file staat in de functie. Om deze transformatie te wijzigen kun je de sample file aanpassen. 
> Deze aanpassingen worden dan doorgevoerd in de functie en toegepast op alle files. 
> Als je files uit een folder combineert, zoek dan de **Transform Sample File** om aanpassingen op elke file te doen, voordat ze worden samengevoegd.

