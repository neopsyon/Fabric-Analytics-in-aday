# Microsoft Fabric - Fabric Analyst in a Day - Lab 6

# ![](../media/Lab_6.1.png)
 
# Inhoud

- Introductie	

- Lakehouse

    - Taak 1: Gegevens opvragen met SQL

    - Taak 2: T-SQL-resultaat visualiseren

    - Taak 3: Visual query aanmaken

    - Taak 4: Queryresultaten visualiseren

    - Taak 5: Relaties aanmaken

    - Taak 6: Measures aanmaken

    - Taak 7: Optioneel gedeelte – Relaties aanmaken
        
    - Taak 8: Optioneel gedeelte – Measures aanmaken

- Referenties

# Introductie 

We hebben gegevens uit verschillende bronnen ingeladen in de Lakehouse. In dit lab werkt u met het datamodel. Normaliter voerden we modelleringsactiviteiten zoals het aanmaken van relaties, het toevoegen van measures enzovoort uit in Power BI Desktop. Hier leren we hoe u deze modelleringsactiviteiten in de service uitvoert.

Aan het einde van dit lab heeft u het volgende geleerd:

- Hoe u de Lakehouse verkent

- Hoe u de SQL-weergave van de Lakehouse verkent

- Hoe u datamodellering in de Lakehouse verkent

# Lakehouse

## Taak 1: Gegevens opvragen met SQL

1. Laten we teruggaan naar de Fabric-workspace, **FAIAD_<username>** die u hebt aangemaakt in Lab 2, Taak 9.

2. U ziet drie typen van lh_FAIAD – Lakehouse, Semantic model en SQL endpoint. We hebben de Lakehouse-optie in een eerder lab verkend. Selecteer de optie **lh_FAIAD SQL analytics endpoint** om de SQL-optie te verkennen. U wordt doorgestuurd naar de **SQL view** van de explorer.

    ![](../media/Lab_6.2.png)
    
Als u de gegevens wilt verkennen voordat u een datamodel aanmaakt, kunt u daarvoor SQL gebruiken. Laten we twee opties bekijken voor het gebruik van SQL: de eerste is ontwikkelaarsvriendelijk en de tweede is bedoeld voor analisten.

Stel dat u snel wilt weten hoeveel eenheden per Supplier zijn verkocht met behulp van SQL. We hebben twee opties: een SQL-statement schrijven of een visual gebruiken om het SQL-statement te genereren.

Let op het linker paneel: u kunt de Tables bekijken. Als u de tabellen uitvouwt, ziet u de Columns waaruit de tabel bestaat. Verder zijn er opties om SQL Views, Functions en Stored Procedures aan te maken. Heeft u een SQL-achtergrond, dan kunt u deze opties gerust verkennen. Laten we een eenvoudige SQL query proberen te schrijven.

3. Selecteer in het **bovenste menu** **New SQL query** of selecteer onderaan het linker paneel **Query**. U wordt doorgestuurd naar de SQL query-weergave.

    ![](../media/Lab_6.3.png)
 
4. Plak de **onderstaande SQL query** in het **queryvenster**. Deze query geeft de eenheden per Supplier Name terug. De Sales-tabel wordt samengevoegd met de Product- en Supplier-tabellen om dit te bereiken.

    ```
    SELECT su.Supplier_Name, SUM(Quantity) as Units
    FROM dbo.Sales s
    JOIN dbo.Product p on p.StockItemID = s.StockItemID
    JOIN dbo.Supplier su on su.SupplierID = p.SupplierID
    GROUP BY su.Supplier_Name
    ```

5. Klik op **Run** om de resultaten te bekijken.

6. U ziet dat er een optie is om deze query op te slaan als een View door **Save as view** te selecteren.

7. In het **linker Explorer**-paneel, onder de sectie **Queries**, ziet u dat deze query is opgeslagen onder **My queries** als **SQL query 1**. Dit biedt de mogelijkheid om de query te hernoemen en op te slaan voor toekomstig gebruik. Er is ook een optie om query's te bekijken die met u zijn gedeeld via de map **Shared queries**.

    ![](../media/Lab_6.4.png)

## Taak 2: T-SQL-resultaat visualiseren

1. We kunnen het resultaat van deze query ook visualiseren. **Markeer de query** in het queryvenster, selecteer het **Results pane** en kies vervolgens **Explore this data**.

    ![](../media/Lab_6.5.png)
   
2. Het dialoogvenster **Explore SQL query** wordt geopend. Vouw in het **Data** pane **SQL query 1** uit.

3. Selecteer de velden **Supplier_Name** en **Units**. Er wordt een gegroepeerd staafdiagram aangemaakt.

4. Wijzig in de sectie **Visualization** het visualtype door **Stacked column chart** te selecteren.

    ![](../media/Lab_6.6.png)
 
5. **Vouw Matrix uit** om de gegevens als een matrix te bekijken.

    ![](../media/Lab_6.7.png)
 
6. Selecteer rechtsboven in het scherm **Save -> Save as report**.

    ![](../media/Lab_6.8.png)
 
7. Het dialoogvenster voor het opslaan van uw rapport wordt geopend. Typ **Units by Supplier** in het tekstvak **Enter a name for your report**.

8. Zorg ervoor dat de doelworkspace uw Fabric-workspace is, **FAIAD<username>**

9. Selecteer **Save**.

    ![](../media/Lab_6.9.png)
   
    U wordt doorgestuurd naar de volledige rapportweergave. U heeft opties om de visuals op te maken. We bekijken deze opties in het volgende lab.

10. Selecteer **lh_FAIAD** in het linker paneel.

    ![](../media/Lab_6.10.png)
 
## Taak 3: Visual query aanmaken

U wordt teruggestuurd naar de **SQL analytics endpoint-weergave**. Als u niet vertrouwd bent met SQL, kunt u een vergelijkbare query uitvoeren met behulp van een visual query.

1. Selecteer in het bovenste menu **New visual query**. Er wordt een visual query-venster geopend.

2. Vouw in het **Explorer** pane **Schemas -> dbo -> Tables** uit.

3. Sleep de tabellen **Sales, Product en Supplier** naar het visual query-venster.

    ![](../media/Lab_6.11.png)
 
4. Selecteer met de tabel **Sales** geselecteerd, vanuit het menu van het visual query-venster, **Combine -> Merge queries**.

    ![](../media/Lab_6.12.png)
     
5. Het dialoogvenster Merge wordt geopend. Selecteer in de **Right table for merge dropdown** de optie **Product**.

6. Selecteer **StockItemID** uit zowel de tabel **Sales** als de tabel **Product**. Dit is om de tabellen Product en Sales samen te voegen.

7. Selecteer bij **Join kind** de optie **Left outer**.

8. Selecteer **OK**.

    ![](../media/Lab_6.13.png)
 
9. Klik in het **results** pane op de **dubbele pijl** naast de kolom **Product**.

10. Er wordt een dialoogvenster geopend. Selecteer **SupplierID** uit het dialoogvenster.

11. Selecteer **OK**. U ziet dat de stappen **Merged queries** en **Expanded Product** worden aangemaakt in de tabel **Sales**.

    ![](../media/Lab_6.14.png)
 
12. Laten we op vergelijkbare wijze de Supplier-tabel samenvoegen. Selecteer binnen de tabel **Sales** het "**+**" (dat na Expanded Product staat) om een nieuwe stap toe te voegen. Er wordt een dialoogvenster geopend.

13. Selecteer **Combine -> Merge queries**.

    ![](../media/Lab_6.15.png)
 
14. Het dialoogvenster Merge wordt geopend. Selecteer in de **Right table for merge dropdown** de optie **Supplier**.

15. Selecteer **SupplierID** uit zowel de tabel **Sales** als de tabel **Supplier**. Dit is om de tabellen Supplier en Sales samen te voegen.

16. Selecteer bij **Join kind** de optie **Left outer**.

17. Selecteer **OK**.

    ![](../media/Lab_6.16.png)
 
18. Klik in het **results** pane op de **dubbele pijl** naast de kolom **Supplier**.

19. Er wordt een dialoogvenster geopend. Selecteer **Supplier_Name** uit het dialoogvenster.

20. Selecteer **OK**. U ziet in de tabel Sales dat **Merged queries** is toegevoegd en dat de **stappen worden geregistreerd**.

    ![](../media/Lab_6.17.png)
 
21. Laten we nu groeperen op Supplier-naam om de hoeveelheid per Supplier te berekenen. Selecteer binnen de tabel **Sales** het "**+**" (dat na Expanded Supplier staat) om een nieuwe stap toe te voegen. Er wordt een dialoogvenster geopend.

22. Selecteer **Transform table -> Group by**. Het dialoogvenster Group by wordt geopend.
 
    ![](../media/Lab_6.18.png)

23. Selecteer **Supplier_Name** in de **Group by**-dropdown.

24. Voer **Units** in als naam.

25. Stel **Operation** in op **Sum**.

26. Selecteer **Quantity** in de **Column**-dropdown.

27. Selecteer **OK**.

    ![](../media/Lab_6.19.png)
 
U ziet dat alle stappen worden geregistreerd in het Sales-blok. (Raadpleeg de eerste schermafbeelding onder Taak 4.)

## Taak 4: Queryresultaten visualiseren

1. Nu de query gereed is, bekijken we het resultaat. Selecteer **Visualize results** in het results pane.

   ![](../media/Lab_6.20.png)
 
2. Het dialoogvenster Visualize results wordt geopend. Vouw in het **Data** pane aan de rechterkant **Visual query1** uit.

3. Selecteer de velden **Supplier_Name** en **Units**.

4. Het resultaat lijkt op het eerder verkregen SQL query-resultaat. Als u wilt, kunt u dit rapport opslaan. Omdat we eerder al een vergelijkbaar rapport hebben opgeslagen, kiezen we voor **Cancel**.

   ![](../media/Lab_6.21.png)
 

## Taak 5: Relaties aanmaken

Nu zijn we klaar om het model te bouwen, relaties tussen tabellen aan te maken en measures te definiëren.

1. Selecteer in het **bottom panel** **Model**. U ziet dat het middelste venster eruitziet als de Model-weergave in Power BI Desktop.

2. **Pas het formaat aan en herschik** de tabellen naar behoefte.

3. Laten we een relatie aanmaken tussen de tabellen Sales en Reseller. Selecteer **ResellerID** in de tabel **Sales** en sleep dit naar **ResellerID** in de tabel **Reseller**.

    ![](../media/Lab_6.22.png)
 
4. Het dialoogvenster voor een nieuwe relatie wordt geopend. Zorg ervoor dat **Table 1** **Sales** is en dat **Column** **ResellerID** is.

5. Zorg ervoor dat **Table 2** **Reseller** is en dat **Column** **ResellerID** is.

6. Zorg ervoor dat **Cardinality** **Many to one (*:1)** is.

7. Zorg ervoor dat **Cross filter direction** **Single** is.

8. Selecteer **Ok**.
 
    ![](../media/Lab_6.23.png)

9. Maak op vergelijkbare wijze een relatie aan tussen de tabellen Sales en Date. Selecteer **InvoiceDate** in de tabel **Sales** en sleep dit naar **Date** in de tabel **Date**.

10. Het dialoogvenster voor een nieuwe relatie wordt geopend. Zorg ervoor dat **Table 1** **Sales** is en dat **Column** **InvoiceDate** is.

11. Zorg ervoor dat **Table 2** **Date** is en dat **Column** **Date** is.

12. Zorg ervoor dat **Cardinality** **Many to one (*:1)** is.

13. Zorg ervoor dat **Cross filter direction** **Single** is.

14. Selecteer **Ok**.

    ![](../media/Lab_6.24.png)
 
15. Maak op vergelijkbare wijze een **many-to-one**-relatie aan tussen de tabellen **Sales** en **Product**. Selecteer **StockItemID** in de tabel **Sales** en **StockItemID** in de tabel **Product**.

16. Selecteer in het bovenste menu **Reporting -> Automatically update semantic model** om het model op te slaan en bij te werken.

    ![](../media/Lab_6.25.png)
 
    **Controlepunt**: Uw model moet de drie relaties bevatten tussen de tabellen Sales en Reseller, Sales en Date, en Sales en Product, zoals weergegeven in de onderstaande schermafbeelding:

    ![](../media/Lab_6.26.png)
 
    Vanwege de beschikbare tijd zullen we niet alle relaties aanmaken. Als de tijd het toelaat, kunt u het optionele gedeelte aan het einde van het lab voltooien. Het optionele gedeelte beschrijft de stappen voor het aanmaken van de overige relaties.

## Taak 6: Measures aanmaken

Laten we een aantal measures toevoegen die we nodig hebben om het Sales-dashboard te maken.

1. Selecteer de **Sales-tabel** in de modelweergave. We willen de measures toevoegen aan de Sales-tabel.

2. Selecteer in het bovenste menu **Home -> New Measure**. U ziet dat de formulebalk wordt weergegeven.

3. Voer **Sales = SUM(Sales[Sales_Amount])** in de **formulebalk** in.

4. Klik op het **vinkje** links van de formulebalk of klik op de knop **Enter**.

5. Vouw in het Properties-paneel aan de rechterkant de sectie **Formatting** uit.

6. Selecteer in de **Format**-dropdown de optie **Whole number**.

    ![](../media/Lab_6.27.png)
 
7. Selecteer met de tabel **Sales** geselecteerd in het bovenste menu **Home -> New Measure**. U ziet dat de formulebalk wordt weergegeven.

8. Voer **Units = SUM(Sales[Quantity])** in de **formulebalk** in.

9. Klik op het **vinkje** links van de formulebalk of klik op de knop **Enter**.

10. Vouw in het Properties-paneel aan de rechterkant de sectie **Formatting** uit (het kan even duren voordat het Properties-paneel is geladen).

11. Selecteer in de **Format**-dropdown de optie **Whole number**.

    ![](../media/Lab_6.28.png)
 
12. Selecteer met de tabel **Sales** geselecteerd in het bovenste menu **Home -> New Measure**. U ziet dat de formulebalk wordt weergegeven.

13. Voer **Orders = DISTINCTCOUNT(Sales[InvoiceID])** in de **formulebalk** in.

14. Klik op het **vinkje** links van de formulebalk of klik op de knop **Enter**.

15. Vouw in het Properties-paneel aan de rechterkant de sectie **Formatting** uit.

16. Selecteer in de Format-dropdown de optie **Whole number**.

    ![](../media/Lab_6.29.png)
 
    Vanwege de beschikbare tijd zullen we ook niet alle measures aanmaken. Als de tijd het toelaat, kunt u het optionele gedeelte aan het einde van het lab voltooien. Het optionele gedeelte beschrijft de stappen voor het aanmaken van de overige measures.
  
    We hebben een datamodel aangemaakt; de volgende stap is het maken van een rapport. Dit doen we in het volgende lab.

## Taak 7: Optioneel gedeelte – Relaties aanmaken

Laten we de overige relaties toevoegen.

1. Maak op vergelijkbare wijze een **many-to-one**-relatie aan tussen **Sales** en **People**. Selecteer **SalespersonPersonID** in **Sales** en **PersonID** in **People**.

    **Controlepunt**: Uw model zou er uit moeten zien zoals de onderstaande schermafbeelding.

    ![](../media/Lab_6.30.png)
 
2. Laten we nu een relatie aanmaken tussen Product en Supplier. Selecteer **SupplierID** in de tabel **Product** en sleep dit naar **SupplierID** in de tabel **Supplier**.

3. Het dialoogvenster voor een nieuwe relatie wordt geopend. Zorg ervoor dat **Table 1** **Product** is en dat **Column** **SupplierID** is.

4. Zorg ervoor dat **Table 2** **Supplier** is en dat **Column** **SupplierID** is.

5. Zorg ervoor dat **Cardinality** **Many to one (*:1)** is.

6. Zorg ervoor dat **Cross filter direction** **Both** is.

7. Selecteer **Ok**.

    ![](../media/Lab_6.31.png)

8. Maak op vergelijkbare wijze een **many to one**-relatie aan met **Cross filter direction** als **Both** tussen **Product_Details** en **Product**. Selecteer **StockItemID** in **Product_Details** en **StockItemID** in **Product**.

9. Laten we nu een relatie aanmaken tussen Reseller en Geo. Selecteer **PostalCityID** in de tabel **Reseller** en sleep dit naar **CityID** in de tabel **Geo**.

10. Het dialoogvenster voor een nieuwe relatie wordt geopend. Zorg ervoor dat **Table 1** **Reseller** is en dat **Column** **PostalCityID** is.

11. Zorg ervoor dat **Table 2** **Geo** is en dat **Column** **CityID** is.

12. Zorg ervoor dat **Cardinality** **Many to one (*:1)** is.

13. Zorg ervoor dat **Cross filter direction** **Both** is.

14. Selecteer **Ok**.

    ![](../media/Lab_6.32.png)
 
15. Laten we nu een relatie aanmaken tussen Customer en Reseller. Selecteer **ResellerID** in de tabel **Customer** en sleep dit naar **ResellerID** in de tabel **Reseller**.

16. Het dialoogvenster voor een nieuwe relatie wordt geopend. Zorg ervoor dat **Table 1** **Customer** is en dat **Column** **ResellerID** is.

17. Zorg ervoor dat **Table 2** **Reseller** is en dat **Column** **ResellerID** is.

18. Zorg ervoor dat **Cardinality** **Many to one (*:1)** is.

19. Zorg ervoor dat **Cross filter direction** **Single** is.

20. Selecteer **Ok**.

    ![](../media/Lab_6.33.png)
 	
    **Controlepunt**: Uw model zou er uit moeten zien zoals de onderstaande schermafbeelding.

    ![](../media/Lab_6.34.png)
 
21. Laten we nu een relatie aanmaken tussen PO en Date. Selecteer **Order_Date** in de tabel **PO** en sleep dit naar **Date** in de tabel **Date**.

22. Het dialoogvenster voor een nieuwe relatie wordt geopend. Zorg ervoor dat **Table 1** **PO** is en dat **Column** **Order_Date** is.

23. Zorg ervoor dat **Table 2** **Date** is en dat **Column** **Date** is.

24. Zorg ervoor dat **Cardinality** **Many to one (*:1)** is.

25. Zorg ervoor dat **Cross filter direction** **Single** is.

26. Selecteer **OK**.

    ![](../media/Lab_6.35.png)
 
27. Maak op vergelijkbare wijze een **many to one**-relatie aan tussen **PO** en **Product**. Selecteer **StockItemID** in **PO** en **StockItemID** in **Product**.

28. Maak op vergelijkbare wijze een **many to one**-relatie aan tussen **PO** en **People**. Selecteer **ContactPersonID** in **PO** en **PersonID** in **People**.

    We zijn klaar met het aanmaken van alle relaties.

    **Controlepunt**: Uw model zou er uit moeten zien zoals de onderstaande schermafbeelding.

    ![](../media/Lab_6.36.png)
 
## Taak 8: Optioneel gedeelte – Measures aanmaken

Laten we de overige measures toevoegen.

1. Selecteer de tabel **Sales** en kies in het bovenste menu **Table tools -> New Measure**.

2. Voer **Avg Order = DIVIDE([Sales], [Orders])** in de formulebalk in.

3. Klik op het **vinkje** in de formulebalk of klik op de knop Enter.

4. Zodra de measure is opgeslagen, ziet u de optie Measure tools in het bovenste menu. Klik op **Measure tools**.

5. Klik in de Format-dropdown op **Decimal Number**.

    ![](../media/Lab_6.37.png)
 
6. Voer op vergelijkbare wijze de volgende measures toe:

    a. **GM = SUM(Sales[Line_Profit])** opgemaakt als **Decimal number**.

    b. **GM% = DIVIDE([GM], [Sales])** opgemaakt als **Percentage**.

    c. **No of Customers = COUNTROWS(Customer)** opgemaakt als **Whole Number**

## Referenties
Fabric Analyst in a Day (FAIAD) introduceert u bij een aantal van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service bevat de sectie Help (?) koppelingen naar uitstekende bronnen.

   ![](../media/img18.png) 
 
Hieronder vindt u nog enkele aanvullende bronnen die u helpen bij uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [aankondiging van Microsoft Fabric GA](https://aka.ms/Fabric-Hero-Blog-Ignite23)
- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)
- Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)
- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)
- Leer nieuwe vaardigheden door de [Fabric Learning-modules](https://aka.ms/learn-fabric) te verkennen
- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)
- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om uw vragen te stellen, feedback te geven en van anderen te leren

Lees de meer gedetailleerde aankondigingsblogs over Fabric-ervaringen:

- [Blog over de Data Factory-ervaring in Fabric](https://aka.ms/Fabric-Data-Factory-Blog) 
- [Blog over de Synapse Data Engineering-ervaring in Fabric](https://aka.ms/Fabric-DE-Blog) 
- [Blog over de Synapse Data Science-ervaring in Fabric](https://aka.ms/Fabric-DS-Blog) 
- [Blog over de Synapse Data Warehousing-ervaring in Fabric](https://aka.ms/Fabric-DW-Blog) 
- [Blog over de Synapse Real-Time Analytics-ervaring in Fabric](https://aka.ms/Fabric-RTA-Blog)
- [Aankondigingsblog Power BI](https://aka.ms/Fabric-PBI-Blog)
- [Blog over de Data Activator-ervaring in Fabric](https://aka.ms/Fabric-DA-Blog) 
- [Blog over beheer en governance in Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)
- [OneLake](https://aka.ms/Fabric-OneLake-Blog)[ in Fabric-blog](https://aka.ms/Fabric-OneLake-Blog)
- [Blog over de integratie van Dataverse en Microsoft Fabric](https://aka.ms/Dataverse-Fabric-Blog)

© 2023 Microsoft Corporation. Alle rechten voorbehouden.

Door gebruik te maken van deze demo/dit lab gaat u akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met als doel uw feedback te verkrijgen en u een leerervaring te bieden. U mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback aan Microsoft te geven. U mag het niet voor enig ander doel gebruiken. U mag deze demo/dit lab of een gedeelte hiervan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, er afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN DEEL ERVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE TEN BEHOEVE VAN VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARE-TECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE MET HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN GEPRESENTEERD, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DEZELFDE WIJZE ALS EEN DEFINITIEVE VERSIE. WE BRENGEN MOGELIJK OOK GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UIT. UW ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK AFWIJKEN.

**FEEDBACK**. Als u feedback geeft over de technologiefuncties, functionaliteit en/of concepten die in deze demo/dit lab worden beschreven aan Microsoft, geeft u Microsoft kosteloos het recht om uw feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, te delen en te commercialiseren. U geeft ook aan derden kosteloos alle patentrechten die nodig zijn voor hun producten, technologieën en diensten om specifieke onderdelen van een Microsoft-software of -service die de feedback bevat, te gebruiken of te integreren. U verstrekt geen feedback die onderworpen is aan een licentie die vereist dat Microsoft zijn software of documentatie aan derden in licentie geeft omdat we uw feedback daarin opnemen. Deze rechten blijven van kracht na afloop van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, INCLUSIEF ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, HETZIJ UITDRUKKELIJK, IMPLICIET OF WETTELIJK, GESCHIKTHEID VOOR EEN BEPAALD DOEL, TITEL EN NIET-INBREUK. MICROSOFT GEEFT GEEN GARANTIES OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE UITVOER DIE VOORTVLOEIT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR ENIG DOEL.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen veranderen in toekomstige versies van het product. In deze demo/dit lab leert u over enkele, maar niet alle, nieuwe functies.
