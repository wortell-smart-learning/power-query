# Lab 2 - Datapreparatie uitdagingen

*Vereisten*

Om het lab te kunnen starten is het van belang dat je toegang hebt tot Power BI desktop.

*Doel*

In dit tweede lab leer je Power Query in te zetten om basale uitdagingen in datapreparatie op te lossen.

## Opdracht 1 - Betekenis halen uit gecodeerde kolommen

1. Start een nieuw Power BI rapport en lees workbook **L2O1.xlsx** uit **Lab 2** in als Excel workbook.

2. Selecteer in het **Navigator** scherm dat opent de tabellen **Categories**, **Colors** en **Products** en selecteer **Transform Data**. Check dat je in het *Queries* paneel dat opent de drie queries kan zien en bekijk de preview.

3. Selecteer de **Categories** query en merk op dat de eerste rij de kolomkoppen bevat. Selecteer in de tab **Transform** de transformatie **Use First Row as Headers** om dit op te lossen. Werk je liever met shortcuts dan kun je ook in het *Preview* paneel in de linkerbovenhoek op het tabelicoontje klikken en vervolgens **Use First Row as Headers** selecteren.

4. Herhaal stap 3 voor de **Colors** query.

5. Selecteer in de **Products** query de **Product Code** kolom door op de kolomkop te klikken of door onder de **Home** tab onder het dropdown menu **Choose columns** de optie **Go to Column** te selecteren en de kolom **Product Code** te kiezen.

6. Selecteer onder de **Transform** tab het dropdown menu **Split Column** en selecteer **By Delimiter**. Hetzelfde kun je doen door te rechtsklikken op de kolomkop **Product Number** en vervolgens **Split Column** en **By Delimiter** te kiezen.

7. De default settings zijn correct voor het splitsen van deze kolom, maar check voor je **OK** drukt nog even de instellingen. 
	- De Custom optie is geselecteerd en het streepje als scheidingsteken. Power Query heeft dit goed beoordeeld op basis van de waarden in de kolom.
	- **Each occurence of this delimiter** is geselecteerd omdat er meerdere scheidingstekens zijn gevonden per waarde.
	- Als je de Advanced options openklikt, zie je dat Power Query heeft gedetecteerd dat de waarde van **Product Number** in vier kolommen kan worden gesplitst.
	- Het **Quote Character** is ook ingesteld. Scheidingstekens (in dit geval streepje) die deel zijn van een tekst en niet als scheidingstekens moeten worden behandeld kunnen met de **Quote Character** correct worden geïnterpreteerd.
	
8. Na het sluiten van de dialoog zie je de vier nieuwe kolommen (Product Number.1 t/m 4)in het *Preview* paneel. Hernoem ze tot **Category Code**, **Short Product Number**, **Size** en **Color**. 

## Opdracht 2 - Samenvoegen van tabellen

In Opdracht 1 hebben we de codes voor Category en Color geëxtraheerd uit een samengestelde kolom. In deze opdracht geven we hier vervolg aan door de codes te vervangen door de omschrijvingen.

1. Selecteer de **Products** query en kies onder de **Home** tab voor **Merge Queries**. 

> In de **Merge** dialoog die opent kun je twee tabellen samenvoegen op basis van overeenkomende waarden in gespecificeerde kolommen. We gaan de **Product Category Name** uit de **Categories** query opnemen in de **Products** query, aan de hand van de overeenkomende **Category Code**.

2. Selecteer de **Category Code** in de **Products** tabel en selecteer in het dropdown menu **Categories**. Selecteer daarin ook **Category Code**. Check dat in de **Join Kind** gekozen is voor **Left Outer (All from first, matching from second)** en klik op OK.

> In het *Preview* paneel is een nieuwe **Categories** kolom toegevoegd met tabelobjecten als waarden.

3. Open de kolom door in de kolomop op de twee pijltjes te klikken. Verwijder in de **Expand** dialoog de vinkjes voor **Category Code** en **Use original column name as prefix** en klik op OK. De **Categories** kolom is vervangen door een nieuwe kolom **Product Category Name** met de overeenkomende waarden in elke rij.

4. Nu je de **Product Category Name** ter beschikking hebt, kun je de **Category Code** verwijderen door de kolom te selecteren en op de Delete toets te drukken.

> Hoewel de **Category Code** kolom nodig was om de Product en Categories queries samen te voegen, kan het resultaat van die stap gezien worden als een tijdelijke tabel, waarin de kolom overbodig is geworden.

5. Herhaal stap 1 t/m 4 voor het opnemen van kolom **Color** uit de **Colors** query in de **Products** query.

> Nu we de inhoud van de **Categories** en **Colors** queries hebben overgenomen zijn de queries overbodig geworden en hoeven ze niet meer te worden geladen.

6. Rechtsklik in het *Queries* paneel op de **Categories** query en verwijder het vinkje **Enable Load**. Herhaal dit voor de **Colors** query.

> Stap 6 stelt je in staat queries als opstapjes te gebruiken voor andere queries en zorgt ervoor dat ze niet in het Power BI rapport worden geladen.

7. Op het **Home** tab, klik op **Close & Apply**. Maak ter verificatie een column chart met **Color** op de X-as en een count van **Product** op de Y-as.

## Opdracht 3 - Kolommen uit voorbeelden

Het belang van een functie is vaak af te lezen uit de positie in het lint. In de **Add Column** tab staat **Column from Examples** helemaal links. Het is dan ook een krachtige feature die je in staat stelt betekenis te ontlenen aan bestaande kolommen zonder voorkennis te hoeven hebben van de beschikbare transformaties. 
Je kunt hierdoor nieuwe kolommen aan jouw queries toevoegen door simpelweg één of meerdere voorbeelden in te voeren. Power Query probeert vervolgens af te leiden welke calculatie benodigd is om tot die waarde te komen en past het toe op alle rijen.

In opdracht 1 heb je het Product Number gesplitst in vier elementen. Stel nu dat je alleen de Product Size uit de samengestelde code wil halen. 

1. Start een nieuw Power BI rapport en lees workbook **L2O1.xlsx** uit **Lab 2** in als Excel workbook.

> In het *Preview* paneel zien we dat de kolom **Product Number** bestaat uit 4 door streepjes gescheiden codes. De uitdaging is om de derde code, die staat voor **Product Size** eruit te halen.

2. Selecteer de kolom **Product Number**, open op de tab **Add Column** het dropdown menu voor **Column from Examples** en selecteer **From Selection**.

> In veel gevallen weet je van tevoren op basis van welke kolommen je de nieuwe kolom wil afleiden. Het selecteren van die selectie verhoogt de kans dat Power Query een nuttige aanbeveling doet aan de hand van jouw voorbeeld. 

3. In de **Add Column from Examples** dialoog wordt je gevraagd de voorbeeldwaarden aan te leveren. De af te leiden kolom staat rechts in beeld. Hernoem deze kolom naar **Size**.

4. Dubbelklik de eerste lege cel in de kolom **Size** (een dropdown menu geeft wat suggesties voor de vulling). Vul de cel met de waarde "S" (zonder quotes), de derde waarde in "VE-C304-S-BE". Druk nu op Enter en Power Query vult de kolom met alle afgeleidde waarden. In het blok boven de kolomkoppen staat de formule die hiervoor is gebruikt.

5. Klik op Ctrl+Enter of OK om de kolom aan te maken. Het *Preview* paneel laat de nieuwe kolom zien, gevuld zoals verwacht. 

> In het **Applied Steps** paneel staat de stap die de kolom toevoegt: **Inserted Text Between Delimiters**. Zonder kennis van deze transformatie heb je het kunnen gebruiken. Nu je het hier ziet kun je het ook in het lint opzoeken (staat onder de **Transform** tab) en onderzoeken hoe het werkt.

## Opdracht 4 - Afleiden van buckets/bereik

In deze opdracht gebruiken we **Column from Examples** om numerieke waarden te groeperen in buckets.
De kolom Size bevat een combinatie van tekstuele en numerieke maten. 
In de volgende stappen leer je de tekstuele waarden te negeren en een nieuwe kolom te definiëren afgeleid van de numerieke waarden. E
r zijn verschillende manieren om dit voor elkaar te krijgen. 
In stap 1 t/m 4 gebruik je de features voor foutafhandeling in Power Query. Vanaf stap 5 maak je gebruik van **Column from Examples**.

1. Selecteer de kolom **Size**. Selecteer op de tab **Add Column** de transformatie **Duplicate Column**.

2. Hernoem de kolom **Size - Numbers** en verander het datatype door aan de linkerkant van de kolomkop op ABC te klikken en in het dropdown menu **Whole Number** te selecteren.

> Je ziet nu Errorwaarden staan in alle rijen met tekstuele waarden voor **Size**, maar je wil alleen met numerieke waarden werken, dus ga je de Errorwaarden vervangen met nulls.

3. Selecteer de kolom **Size - Numbers**, klik in de **Transform** tab op het dropdown menu van **Replace Values** en kies **Replace Errors**. Een snellere manier om dit te kiezen is te rechtsklikken op de kolomkop en **Replace Errors** te selecteren.

4. Kies in de **Replace Errors** dialoog die opent als vervangende waarde "null" (zonder quotes) en klik OK.

5. Verwijder nu de laatste vier stappen die in het *Applied Steps* paneel zijn toegevoegd. De laatste stap die overblijft is **Inserted Text Between Delimiter**.

6. Selecteer de kolom **Size**. Selecteer in de tab **Add Column** het dropdown menu **Column from Examples** en kies **From Selection**.

7. Hernoem de nieuwe kolom naar **Size - Numbers**.

8. Dubbelklik op de eerste lege cel in **Size - Numbers**. De waarde in kolom **Size** is "S". Omdat je tekstuele waarden wilt negeren, vul je hier "null" (zonder quotes) in en druk op Enter.

9. Herhaal dit voor rij 2, 3, 7 en 21 (Size M, L, NA en X).

10. Vul rij 22 met waarde 60 (Size 60). Power Query vult de nieuwe **Size - Numbers** kolom met de voorgestelde waarden. Met Ctrl+Enter of OK maak je de kolom aan.

> In het *Applied Steps* paneel zie je nu de stap **Added Conditional Column** staan. Dubbelklik op deze stap om de afleiding te zien die is gebaseerd op jouw voorbeelden. Je had dit ook kunnen aanmaken door te kiezen voor **Conditional Column** in plaats van **Column from Examples**.

11. Verander het datatype van **Size - Numbers** naar "Whole Number". 

> In het vervolg van deze opdracht maken we een aparte tabel voor producten met numerieke maten en classificeren we ze in 4 buckets door gebruik te maken van **Column from Examples**.

12. Rechtsklik in het *Queries* paneel op **Products** en selecteer **Reference**. Hernoem de nieuw toegevoegde query tot "Numeric-Size Products". Dit kan door te dubbelklikken op de query, rechtsklikken en **Rename** te selecteren of door de Name aan te passen in het *Query Settings* paneel onder **Properties**.

> Het gebruik van Reference is een handige techniek voor het aanmaken van vertakkingen van een brontabel en maakt een nieuwe tabel aan die start vanaf de laatste stap van de query waaraan wordt gerefereerd. 

13. Verwijder in de nieuwe query alle products waarvoor de waarde "null" is in de kolom **Size - Numbers**. Klik hiervoor in de kolomkop op de filter control en selecteer **Remove Empty**.

14. Maak een nieuwe **Column from Example** aan die **Size Bucket** heet en die voldoet aan de volgende afleiding: X bij 70 of groter, L bij 60 of groter, M bij 50 of groter, S bij kleiner dan 50. Check de formule die voorgesteld wordt ter verificatie. 

15. Dubbelklik op de stap **Column from Examples** in het *Applied Steps* paneel om de afleidingscondities te reviewen. Sluit dan de dialoog.

16. Bekijk de *formula bar* voor de gegenereerde M code. 

## Table of Contents

1. [Een eerste blik op Power Query](../Lab1/LabInstructies1.md)
2. [Datapreparatie uitdagingen](../Lab2/LabInstructies2.md)
3. [](../Lab3/LabInstructies3.md)
4. [](../Lab4/LabInstructies4.md)
5. [](../Lab5/LabInstructies5.md)
6. [](../Lab6/LabInstructies6.md)
7. [](../Lab7/LabInstructies7.md)
8. [](../Lab8/LabInstructies8.md)
9. [](../Lab9/LabInstructies9.md)
