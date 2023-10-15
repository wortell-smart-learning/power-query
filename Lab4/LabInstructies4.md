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
