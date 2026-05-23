# Microsoft Fabric - Fabric Analyst in a Day - Lab 6

# ![](../media/new10.png)

# Inhoudsopgave
 * Introductie

 * Lakehouse

     * Taak 1: Data opvragen met SQL

     * Taak 2: T-SQL-resultaat visualiseren

     * Taak 3: Visual query aanmaken

     * Taak 4: Queryresultaten visualiseren

     * Taak 5: Relaties aanmaken

     * Taak 6: Measures aanmaken

     * Taak 7: Optioneel gedeelte – Relaties aanmaken

     * Taak 8: Optioneel gedeelte – Measures aanmaken

 * Referenties

# <a name="_toc152200366"></a>**Introductie**

We hebben data uit diverse bronnen ingeladen in de Lakehouse. In dit lab werkt u met het datamodel. Normaal voerden we modelleringsactiviteiten zoals het aanmaken van relaties, het toevoegen van measures enzovoort uit in Power BI Desktop. Hier leren we hoe u deze modelleringsactiviteiten in de service kunt uitvoeren.

Aan het einde van dit lab heeft u geleerd:

- <a name="_hlk152198899"></a>Hoe u de Lakehouse verkent
- Hoe u de SQL view van de Lakehouse verkent
- Hoe u datamodellering in de Lakehouse verkent

# <a name="_toc152200367"></a>**Lakehouse**

### <a name="_toc152200368"></a>Taak 1: Data opvragen met SQL

1. Navigeer terug naar de Fabric workspace, **FAIAD_username** die u in Lab 2, Taak 8 hebt aangemaakt.
1. Navigeer terug naar het **Data Factory-scherm**.
1. U ziet drie typen lh_FAIAD – Semantic model, SQL endpoint en Lakehouse. We hebben de Lakehouse-optie in een eerder lab verkend. Selecteer de optie **lh_FAIAD SQL analytics endpoint** om de SQL-optie te verkennen. U wordt doorgestuurd naar de **SQL view** van de explorer.

    ![A screenshot of Data Factory Home](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.002.png)

    Als u de data wilt verkennen voordat u een datamodel aanmaakt, kunt u daarvoor SQL gebruiken. Laten we twee opties bekijken om SQL te gebruiken: de eerste is geschikt voor developers, de tweede optie is voor analisten.

    Stel dat u snel wilt weten hoeveel eenheden er per Supplier zijn verkocht met behulp van SQL. We hebben twee opties: een SQL-statement schrijven of een visual gebruiken om het SQL-statement op te stellen.

    Let op het linker paneel: u kunt daar de Tables bekijken. Als u de tables uitvouwt, ziet u de Columns waaruit de table bestaat. Er zijn ook opties om SQL Views, Functions en Stored Procedures aan te maken. Als u een SQL-achtergrond heeft, kunt u deze opties gerust verkennen. Laten we een eenvoudige SQL query proberen te schrijven.

1. Selecteer **New SQL query** in het **bovenste menu** of selecteer **Query** onderaan het **linker paneel**. U wordt doorgestuurd naar de SQL query-weergave.

   ![A screenshot of SQL Query view](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.003.png)

1. **Plak** de onderstaande SQL query in het **queryvenster**. Deze query geeft de eenheden per Supplier Name terug. De Sales table wordt samengevoegd met de Product- en Supplier-table om dit te bereiken.

   ```
   SELECT su.Supplier_Name, SUM(Quantity) as Units   
   FROM dbo.Sales s
   JOIN dbo.Product p on p.StockItemID = s.StockItemID
   JOIN dbo.Supplier su on su.SupplierID = p.SupplierID
   GROUP BY su.Supplier_Name
   ```
1. Klik op **Run** om de resultaten te bekijken.
1. U ziet dat er een optie is om deze query als View op te slaan via Save as view.
1. In het rechter **Explorer**-paneel, onder de **Queries section**, ziet u dat deze query is opgeslagen onder **My queries** als **SQL query 1**. Dit biedt de mogelijkheid om de query te hernoemen en op te slaan voor toekomstig gebruik. Er is ook een optie om queries te bekijken die met u zijn gedeeld via de map **Shared queries**.

   ![A screenshot of SQL query screen](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.004.png)

### <a name="_hlk152164208"></a> <a name="_toc152200369"></a>Taak 2: T-SQL-resultaat visualiseren

1. We kunnen het resultaat van deze query ook visualiseren. **Selecteer de query** in het queryvenster, ga naar de dropdown **Explore this Data(Preview)** en selecteer vervolgens **Visualize results** in het **Results pane**.

   ![A screenshot of SQL query screen with result](../media/L6T2S1.png)

1. Het dialoogvenster Visualize results wordt geopend. Selecteer **Continue**.

   ![A screenshot of Visualize results dialog](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.006.png)

1. Het bekende rapportweergavevenster wordt geopend. Vouw in het **Data** pane de **SQL query 1** uit.
1. Selecteer de **velden** **Supplier_Name** en **Units**. Standaard wordt een tabelvisual aangemaakt.
1. Wijzig het visualtype door **Stacked column chart** te selecteren in de sectie **Visualization**.
1. **Pas de grootte** van de visual naar behoefte aan. Het grafiektype verandert.

   **Opmerking:** U ziet dat alle opties die beschikbaar zijn voor het opmaken van een visual in een Power BI-rapport hier ook beschikbaar zijn.

1. Selecteer **Save as report**.
1. Het dialoogvenster voor het opslaan van uw rapport wordt geopend. Typ **Units by Supplier** in het tekstvak **Enter a name for your report**.
1. Zorg ervoor dat de doelworkspace **uw workspacenaam** is.
1. Selecteer **Save**.

   ![A screenshot of Visualize results screen](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.007.png)

### <a name="_toc152200370"></a>Taak 3: Visual query aanmaken

U wordt teruggeleid naar de **SQL analytics endpoint-weergave**. Als u niet bekend bent met SQL, kunt u een vergelijkbare query uitvoeren met behulp van de visual query.

1. Selecteer **New visual query** in het bovenste menu. Er wordt een visual query-venster geopend.
1. Sleep vanuit het **Explorer** pane de tabellen **Sales, Product en Supplier** naar het visual query-venster.
1. Selecteer met de **Sales**-table geselecteerd in het menu van het visual query-venster de optie **Combine -> Merge queries**.

   ![A screenshot of Visual query screen](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.008.png)

1. Het dialoogvenster Merge wordt geopend. Selecteer **Product** in de dropdown **Right table for merge**.
1. Selecteer **StockItemID** uit zowel de **Sales**- als de **Product**-table. Hiermee worden de tabellen Product en Sales samengevoegd.
1. Selecteer bij **Join kind** de optie **Left Outer**.
1. Selecteer **OK**.

   ![A screenshot of merge query dialog](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.009.png)

1. Klik in het **results** pane op de **dubbele pijl** naast de kolom **Product**.
1. Er wordt een dialoogvenster geopend; selecteer **SupplierID** uit het dialoogvenster.
1. Selecteer **OK**.

   ![A screenshot of visual query dialog](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.010.png)

   U ziet dat de stappen Merged queries en Expanded Product zijn aangemaakt in de Sales-table.

1. Laten we op vergelijkbare wijze de Supplier-table samenvoegen. Selecteer in de **Sales**-table het **"+"**-teken (na Expanded Product) om een nieuwe stap toe te voegen. Er wordt een dialoogvenster geopend.
1. Selecteer **Combine -> Merge queries**.

   ![A screenshot to add Merge query step](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.011.png)

1. Het dialoogvenster Merge wordt geopend. Selecteer **Supplier** in de dropdown **Right table for merge**.
1. Selecteer **SupplierID** uit zowel de **Sales**- als de **Supplier**-table. Hiermee worden de tabellen Supplier en Sales samengevoegd.
1. Selecteer bij **Join kind** de optie **Left Outer**.
1. Selecteer **OK**.

   ![A screenshot of merge query dialog](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.012.png)

1. Klik in het **results** pane op de **dubbele pijl** naast de kolom **Supplier**.
1. Er wordt een dialoogvenster geopend; selecteer **Supplier_Name** uit het dialoogvenster.
1. Selecteer **OK**. U ziet dat alle **stappen zijn vastgelegd** in de Sales-table.

### <a name="_toc152200371"></a>Taak 4: Queryresultaten visualiseren

1. Nu de query gereed is, bekijken we het resultaat. Selecteer **Visualize results** in het results pane.

      ![A screenshot of visual query dialog](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.013.png)

1. Het dialoogvenster Visualize results wordt geopend, dat eruitziet als een Power BI-venster. Selecteer in het **Data** pane aan de rechterkant de velden **Supplier_Name** en **Quantity**.
1. Hiermee wordt een tabelvisual aangemaakt met een resultaat vergelijkbaar met het SQL query-resultaat van eerder. Als u dat wilt, kunt u dit rapport opslaan. Omdat we eerder al een vergelijkbaar rapport hebben opgeslagen, selecteren we **Cancel**.

   ![A screenshot of visualize report dialog](../media/new16.png)

### <a name="_toc152200372"></a>Taak 5: Relaties aanmaken

Nu zijn we klaar om het model te bouwen, relaties tussen tabellen aan te maken en measures te definiëren.

1. Selecteer **Model** onderaan het **linker paneel**. U ziet dat het centrale venster eruitziet als de Model-weergave in Power BI Desktop.
1. **Pas de grootte aan en herschik** de tabellen naar behoefte.
1. Laten we een relatie aanmaken tussen Sales en Resellers. Selecteer **ResellerID** uit de **Sales**-table en sleep het naar **ResellerID** in de **Reseller**-table.

   ![A screenshot of modeling view](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.015.png)

1. Het dialoogvenster New relationship wordt geopend. Zorg ervoor dat **Table 1** gelijk is aan **Sales** en **Column** gelijk is aan **ResellerID**.
1. Zorg ervoor dat **Table 2** gelijk is aan **Reseller** en **Column** gelijk is aan **ResellerID**.
1. Zorg ervoor dat **Cardinality** gelijk is aan **Many to one (\*:1)**.
1. Zorg ervoor dat **Cross filter direction** gelijk is aan **Single**.
1. Selecteer **Ok**.

   ![A screenshot of New relationship dialog](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.016.png)

1. Maak op vergelijkbare wijze een relatie aan tussen Sales en Date. Selecteer **InvoiceDate** uit de **Sales**-table en sleep het naar **Date** in de **Date**-table.
1. Het dialoogvenster New relationship wordt geopend. Zorg ervoor dat **Table 1** gelijk is aan **Sales** en **Column** gelijk is aan **InvoiceDate**.
1. Zorg ervoor dat **Table 2** gelijk is aan **Date** en **Column** gelijk is aan **Date**.
1. Zorg ervoor dat **Cardinality** gelijk is aan **Many to one (\*:1)**.
1. Zorg ervoor dat **Cross filter direction** gelijk is aan **Single**.
1. Selecteer **Ok**.

   ![A screenshot of New relationship dialog](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.017.png)

     **Controlepunt:** Uw model zou de twee relaties moeten bevatten zoals weergegeven in de schermafbeelding:

  ![A screenshot of model so far](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.018.png)

Vanwege de beschikbare tijd maken we niet alle relaties aan. Als de tijd het toelaat, kunt u het optionele gedeelte aan het einde van het lab voltooien. Het optionele gedeelte doorloopt de stappen voor het aanmaken van de overige relaties.

### <a name="_toc152200373"></a>Taak 6: Measures aanmaken

Laten we een aantal measures toevoegen die nodig zijn om het Sales-dashboard te maken.

1. Selecteer de **Sales-table** in de modelweergave. We willen de measures aan de Sales-table toevoegen.
1. Selecteer **Home -> New Measure** in het bovenste menu. De formulebalk wordt weergegeven.

    >**Opmerking:** Als u niet op de optie New Measure kunt klikken, ga dan naar **Reporting (1)** en selecteer **Automatically update semantic model (2)**.

    ![A screenshot of modeling view with formula bar to add measure](../media/Fabricnewone4.png)

1. Voer **Sales = SUM(Sales[Sales_Amount])** in de **formulebalk** in.
1. Klik op het **vinkje** in de formulebalk of klik op de Enter-knop.
1. Vouw in het Properties-paneel aan de rechterkant de sectie **Formatting** uit.
1. Selecteer **Currency** in de dropdown **Format**.

   ![A screenshot of modeling view with formula bar to add measure](../media/new13.png)

1. Klik met de **Sales-table geselecteerd** op **New Measure** in het bovenste menu.
1. Voer **Units = SUM(Sales[Quantity])** in de **formulebalk** in.
1. Klik op het **vinkje** in de formulebalk of klik op de Enter-knop.
1. Vouw in het Properties-paneel aan de rechterkant de sectie **Formatting** uit (het kan even duren voordat het Properties-paneel is geladen).
1. Selecteer **Whole number** in de dropdown **Format**.

   ![A screenshot of modeling view with formula bar to add measure](../media/new14.png)

1. Selecteer met de **Sales-table geselecteerd** de optie **New Measure** in het bovenste menu.
1. Voer **Orders = DISTINCTCOUNT(Sales[InvoiceID])** in de **formulebalk** in.
1. Klik op het **vinkje** in de formulebalk of klik op de Enter-knop.
1. Vouw in het Properties-paneel aan de rechterkant de sectie **Formatting** uit.
1. Selecteer **Whole number** in de dropdown **Format**.

   ![A screenshot of modeling view with formula bar to add measure](../media/new15.png)

Ook hier maken we vanwege de beschikbare tijd niet alle measures aan. Als de tijd het toelaat, kunt u het optionele gedeelte aan het einde van het lab voltooien. Het optionele gedeelte doorloopt de stappen voor het aanmaken van de overige measures.

We hebben een datamodel aangemaakt; de volgende stap is het instellen van een vernieuwingsschema voor de verschillende databronnen. Dat doen we in de volgende labs.

### <a name="_toc152200374"></a>Taak 7: Optioneel gedeelte – Relaties aanmaken

Laten we de overige relaties toevoegen.

1. Maak een **many to one**-relatie aan tussen **Sales** en **Product**. Selecteer **StockItemID** uit **Sales** en **StockItemID** uit **Product**.
1. Maak op vergelijkbare wijze een **many to one**-relatie aan tussen **Sales** en **People**. Selecteer **SalespersonPersonID** uit **Sales** en **PersonID** uit **People**.

      **Controlepunt:** Uw model zou er moeten uitzien als de onderstaande schermafbeelding.

    ![A screenshot of modeling view](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.022.png)

1. Laten we nu een relatie aanmaken tussen Product en Supplier. Selecteer **SupplierID** uit de **Product**-table en sleep het naar **SupplierID** in de **Supplier**-table.
1. Het dialoogvenster New relationship wordt geopend. Zorg ervoor dat **Table 1** gelijk is aan **Product** en **Column** gelijk is aan **SupplierID**.
1. Zorg ervoor dat **Table 2** gelijk is aan **Supplier** en **Column** gelijk is aan **SupplierID**.
1. Zorg ervoor dat **Cardinality** gelijk is aan **Many to one (*:1)**.
1. Zorg ervoor dat **Cross filter direction** gelijk is aan **Both**.
1. Selecteer **Ok**.

      ![A screenshot of New relationship dialog](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.023.png)

1. Maak op vergelijkbare wijze een **many to one**-relatie aan met **Cross filter direction** als **Both** tussen **Product_Details** en **Product**. Selecteer **StockItemID** uit **Product_Details** en **StockItemID** uit **Product**.
1. Laten we nu een relatie aanmaken tussen Reseller en Geo. Selecteer **PostalCityID** uit de **Reseller**-table en sleep het naar **CityID** in de **Geo**-table.
1. Het dialoogvenster New relationship wordt geopend. Zorg ervoor dat **Table 1** gelijk is aan **Reseller** en **Column** gelijk is aan **PostalCityID**.
1. Zorg ervoor dat **Table 2** gelijk is aan **Geo** en **Column** gelijk is aan **CityID**.
1. Zorg ervoor dat **Cardinality** gelijk is aan **Many to one (*:1)**.
1. Zorg ervoor dat **Cross filter direction** gelijk is aan **Both**.
1. Selecteer **Ok**.

   ![A screenshot of New relationship dialog](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.024.png)

      **Controlepunt:** Uw model zou er moeten uitzien als de onderstaande schermafbeelding.

   ![A screenshot of modeling view](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.026.png)

1. Laten we nu een relatie aanmaken tussen PO en Date. Selecteer **Order_Date** uit de **PO**-table en sleep het naar **Date** in de **Date**-table.
1. Het dialoogvenster New relationship wordt geopend. Zorg ervoor dat **Table 1** gelijk is aan **PO** en **Column** gelijk is aan **Order_Date**.
1. Zorg ervoor dat **Table 2** gelijk is aan **Date** en **Column** gelijk is aan **Date**.
1. Zorg ervoor dat **Cardinality** gelijk is aan **Many to one (*:1)**.
1. Zorg ervoor dat **Cross filter direction** gelijk is aan **Single**.
1. Selecteer **OK**.

      ![A screenshot of New relationship dialog](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.027.png)

1. Maak op vergelijkbare wijze een **many to one**-relatie aan tussen **PO** en **Product**. Selecteer **StockItemID** uit **PO** en **StockItemID** uit **Product**.
1. Maak op vergelijkbare wijze een **many to one**-relatie aan tussen **PO** en **People**. Selecteer **ContactPersonID** uit **PO** en **PersonID** uit **People**.

  Alle relaties zijn nu aangemaakt.

   **Controlepunt:** Uw model zou er moeten uitzien als de onderstaande schermafbeelding.

   ![A screenshot of modeling view](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.028.png)

### <a name="_toc152200375"></a>Taak 8: Optioneel gedeelte – Measures aanmaken

Laten we de overige measures toevoegen.

1. Voer **Avg Order = DIVIDE([Sales], [Orders])** in de formulebalk in.
1. Klik op het **vinkje** in de formulebalk of klik op de Enter-knop.
1. Zodra de measure is opgeslagen, ziet u de optie Measure tools in het bovenste menu. Klik op **Measure tools**.
1. Klik in de dropdown Format op **Currency**.

   ![A screenshot of modeling view with formula bar to add measure](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.029.png)

1. Volg vergelijkbare stappen om de volgende measures toe te voegen:
   1. **GM = SUM(Sales[Line\_Profit])** opgemaakt als **Currency, Decimal places of 2**
   1. **GM% = DIVIDE([GM], [Sales])** opgemaakt als **Percentage, Decimal places of 2**
   1. **No of Customers = COUNTROWS(Customer)** opgemaakt als **Whole Number**

# <a name="_toc150777627"></a><a name="_toc150779083"></a><a name="_toc152200376"></a>**Referenties**

Fabric Analyst in a Day (FAIAD) maakt u vertrouwd met een aantal van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. Via het menu van de service bevat de Help (?)-sectie links naar uitstekende bronnen.

  ![A screenshot of help options](../media/Aspose.Words.81f0a6eb-66e8-4803-8eb7-2aca2def2ac4.030.png)

Hieronder vindt u nog enkele bronnen die u helpen bij uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [aankondiging van Microsoft Fabric GA](https://aka.ms/Fabric-Hero-Blog-Ignite23)
- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)
- Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)
- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)
- Doe nieuwe vaardigheden op door de [Fabric Learning-modules](https://aka.ms/learn-fabric) te verkennen
- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)
- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om uw vragen te stellen, feedback te delen en van anderen te leren

Lees de uitgebreidere aankondigingsblogs over Fabric-ervaringen:

- [Data Factory-ervaring in Fabric-blog](https://aka.ms/Fabric-Data-Factory-Blog)
- [Synapse Data Engineering-ervaring in Fabric-blog](https://aka.ms/Fabric-DE-Blog)
- [Synapse Data Science-ervaring in Fabric-blog](https://aka.ms/Fabric-DS-Blog)
- [Synapse Data Warehousing-ervaring in Fabric-blog](https://aka.ms/Fabric-DW-Blog)
- [Synapse Real-Time Analytics-ervaring in Fabric-blog](https://aka.ms/Fabric-RTA-Blog)
- [Power BI-aankondigingsblog](https://aka.ms/Fabric-PBI-Blog)
- [Data Activator-ervaring in Fabric-blog](https://aka.ms/Fabric-DA-Blog)
- [Beheer en governance in Fabric-blog](https://aka.ms/Fabric-Admin-Gov-Blog)
- [OneLake](https://aka.ms/Fabric-OneLake-Blog)[ in Fabric-blog](https://aka.ms/Fabric-OneLake-Blog)
- [Dataverse en Microsoft Fabric-integratieblog](https://aka.ms/Dataverse-Fabric-Blog)

© 2023 Microsoft Corporation. Alle rechten voorbehouden.

Door gebruik te maken van deze demo/dit lab gaat u akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met het doel uw feedback te verzamelen en u een leerervaring te bieden. U mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback aan Microsoft te geven. U mag het niet voor enig ander doel gebruiken. U mag deze demo/dit lab of een gedeelte daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, er afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN GEDEELTE DAARVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE VOOR VERDERE REPRODUCTIE OF VERDERE VERSPREIDING IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARETECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJK NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN GEPRESENTEERD, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DEZELFDE MANIER ALS EEN DEFINITIEVE VERSIE. WE KUNNEN OOK BESLUITEN EEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN NIET UIT TE BRENGEN. UW ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK AFWIJKEN.

**FEEDBACK**. Als u feedback geeft over de technologiefuncties, functionaliteit en/of concepten die in deze demo/dit lab worden beschreven aan Microsoft, verleent u Microsoft kosteloos het recht om uw feedback op welke wijze dan ook en voor welk doel dan ook te gebruiken, te delen en te commercialiseren. U verleent derden ook kosteloos alle octrooirechten die nodig zijn voor hun producten, technologieën en diensten om gebruik te maken van of te koppelen aan specifieke onderdelen van Microsoft-software of -diensten die de feedback bevatten. U geeft geen feedback die onderworpen is aan een licentie die vereist dat Microsoft zijn software of documentatie aan derden in licentie geeft omdat we uw feedback daarin opnemen. Deze rechten blijven van kracht na afloop van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, INCLUSIEF ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, ONGEACHT OF DEZE UITDRUKKELIJK, IMPLICIET OF WETTELIJK ZIJN, GESCHIKTHEID VOOR EEN BEPAALD DOEL, TITEL EN NIET-INBREUK. MICROSOFT GEEFT GEEN GARANTIES OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE UITVOER DIE VOORTVLOEIT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR ENIG DOEL.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen worden gewijzigd in toekomstige versies van het product. In deze demo/dit lab leert u over enkele, maar niet alle, nieuwe functies.
