# Microsoft Fabric - Fabric Analyst in a Day - Lab 4

# ![](../media/new8.png)

# Inhoudsopgave
- Introductie
  
- Dataflow Gen2

   - Taak 1: Snowflake-query's kopiëren naar Dataflow
   
   - Taak 2: Verbinding maken met Snowflake
   
   - Taak 3: Data Destination configureren voor Supplier- en PO-query's
   
   - Taak 4: Snowflake Dataflow hernoemen en publiceren
   
   - Taak 5: Dataverse-query's kopiëren naar Dataflow
   
   - Taak 6: Verbinding maken met Dataverse
   
   - Taak 7: Data destination aanmaken voor Customer-query
   
   - Taak 8: Dataverse Dataflow publiceren en hernoemen
   
   - Taak 9: SharePoint-query's kopiëren naar Dataflow
   
   - Taak 10: SharePoint-verbinding aanmaken
   
   - Taak 11: Data destination configureren voor People-query
   
   - Taak 12: SharePoint Dataflow publiceren en hernoemen

- Referenties


# <a name="_toc152198704"></a>**Introductie** 

In ons scenario bevindt Supplier Data zich in Snowflake, Customer Data in Dataverse en Employee Data in SharePoint. Al deze gegevensbronnen worden op verschillende tijden bijgewerkt. Om het aantal data refreshes van Dataflows te minimaliseren, gaan we voor elk van deze gegevensbronnen afzonderlijke Dataflows aanmaken.

**Opmerking:** Meerdere gegevensbronnen worden ondersteund in één enkele Dataflow.

Aan het einde van dit lab hebt u het volgende geleerd:

- Hoe u verbinding maakt met Snowflake via Dataflow Gen2 en gegevens inlaadt in Lakehouse
- Hoe u verbinding maakt met SharePoint via Dataflow Gen2 en gegevens inlaadt in Lakehouse
- Hoe u verbinding maakt met Dataverse via Dataflow Gen2 en gegevens inlaadt in Lakehouse

# <a name="_toc152198705"></a>**Dataflow Gen 2**
### <a name="_toc152151584"></a><a name="_toc152198706"></a>Taak 1: Snowflake-query's kopiëren naar Dataflow

1. Navigeer terug naar de Fabric-workspace **FAIAD_username** die u eerder hebt aangemaakt in Lab 2, Taak 8.
1. Selecteer in het bovenste menu **New -> Dataflow Gen2**.

      ![A screenshot to select New -> Dataflow Gen2](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.002.png)

      U wordt doorgestuurd naar de **Dataflow page**. Nu we vertrouwd zijn met Dataflow, gaan we de query's kopiëren vanuit Power BI Desktop naar Dataflow.

3. Als u het nog niet hebt geopend, open dan **FAIAD.pbix** in de map **Report** op het **bureaublad** van uw lab-omgeving.

4. Selecteer in het lint **Home -> Transform data**. Het Power Query-venster opent. Zoals u in het eerdere lab hebt opgemerkt, zijn de query's in het linker paneel georganiseerd per gegevensbron.

5. Het Power Query-venster opent. Selecteer in het linker paneel, onder de map SnowflakeData, via **Ctrl+Select** of Shift+Select de volgende query's:
   1. SupplierCategories
   2. Suppliers
   3. Supplier
   4. PO
   5. PO Line Items

6. **Klik met de rechtermuisknop** en selecteer **Copy**.

      ![A screenshot to copy queries from Power Query window](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.003.png)

7. Navigeer terug naar de **browser**.
8. Selecteer in het **Dataflow pane** het **centrale venster** en druk op **Ctrl+V** (momenteel wordt rechtsklikken en Plakken niet ondersteund).

### <a name="_toc152198707"></a>Taak 2: Verbinding maken met Snowflake

U ziet dat de vijf query's zijn geplakt en dat het Queries panel nu aan de linkerkant zichtbaar is. Omdat er nog geen verbinding is aangemaakt voor Snowflake, ziet u een waarschuwingsbericht met het verzoek de verbinding te configureren.

1. Selecteer **Configure connection**.

      ![A screenshot of dataflow to configure connection](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.004.png)

2. Het dialoogvenster Connect to data source opent. Zorg er in de **Connection** dropdown voor dat **Create new connection** is geselecteerd.
3. **Authentication kind** moet **Snowflake** zijn.
4. **Username** moet **TE_SNOWFLAKE** zijn.
5. **Password** moet **8UpfRpExVDXv2AC** zijn.
6. Selecteer **Connect**.

      ![A screenshot to connect to data source](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.005.png)

      De verbinding is tot stand gebracht en u kunt de gegevens bekijken in het voorbeeldvenster. U kunt naar eigen inzicht door de Applied Steps van de query's navigeren. De Suppliers-query bevat de leveranciersgegevens en SupplierCategories bevat, zoals de naam aangeeft, de leverancierscategorieën. Deze twee tabellen worden samengevoegd om de Supplier-dimensie te maken met de kolommen die we nodig hebben. Op dezelfde manier zijn PO Line Items samengevoegd met PO om het PO-feit te maken. Nu moeten we de Supplier- en PO-gegevens inladen in Lakehouse.

7. Zoals eerder vermeld, stagen we geen van deze gegevens. Klik daarom met de **rechtermuisknop** op de **Supplier**-query in het Queries-venster en selecteer **Enable staging** om het vinkje te verwijderen.

      ![A screenshot to Enable Staging](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.006.png)

8. Klik op dezelfde manier met de rechtermuisknop op de **PO**-query. Selecteer **Enable staging** om het vinkje te verwijderen.

   **Opmerking:** We hoeven staging niet uit te schakelen voor de andere drie query's, omdat Enable Load al was uitgeschakeld in Power BI Desktop (van waaruit deze query's zijn gekopieerd).
   
### <a name="_toc152198708"></a>Taak 3: Data Destination configureren voor Supplier- en PO-query's

1. Selecteer de **Supplier**-query.
2. Selecteer in de rechteronderhoek **+** naast **Data destination**.
3. Selecteer **Lakehouse** in het dialoogvenster.

      ![A screenshot to select Data Destination for Supplier query](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.007.png)

4. Het dialoogvenster Connect to data destination opent. Selecteer in de **Connection dropdown** de optie **Lakehouse (none)**.
5. Selecteer **Next**.

      ![A screenshot to Connect to data destination](../media/L4T3S5.png)

6. Het dialoogvenster Choose destination target opent. Zorg ervoor dat de **New table radio button** is **geselecteerd**, omdat we een nieuwe tabel aanmaken.
7. We willen de tabel aanmaken in de Lakehouse die we eerder hebben gemaakt. Navigeer in het linker paneel naar **Lakehouse -> de naam van uw workspace**.
8. Selecteer **lh_FAIAD**.
9. Laat de tabelnaam staan op **Supplier**.
10. Selecteer **Next**.

      ![A screenshot to Choose destination target](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.009.png)

11. Het dialoogvenster Choose destination settings opent. Elke keer dat Dataflow Gen2 wordt vernieuwd, willen we een volledige laadbewerking uitvoeren. Zet de schakelaar **Use Automatic Settings** op **OFF** en zorg ervoor dat **Update method** is ingesteld op **Replace**.
12. U ziet een waarschuwing: "Some column names contain unsupported characters. Should we fix them for you?". Lakehouse ondersteunt geen kolomnamen met spaties. Selecteer **Fix it** om de waarschuwing te verwijderen.
13. Column mapping kan worden gebruikt om dataflow-kolommen te koppelen aan bestaande kolommen. In ons geval is het een New Table. Daarom kunnen we de standaardwaarden gebruiken. Selecteer **Save settings**.

      ![A screenshot to Choose destination settings](../media/L4T3S13.png)

14. U wordt teruggestuurd naar het **Power Query-venster**. U ziet dat **Data destination** in de rechteronderhoek is ingesteld op **Lakehouse**. **Stel op dezelfde manier de Data Destination in voor de PO-query**. Zodra dit is gedaan, moet uw PO-query **Data Destination** hebben ingesteld op **Lakehouse**, zoals weergegeven in de onderstaande schermafbeelding.

      ![A screenshot showing Data Destintion for PO](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.011.png)

### <a name="_toc152198709"></a>Taak 4: Snowflake Dataflow hernoemen en publiceren

1. Selecteer bovenaan het scherm de **pijl naast Dataflow1** om de naam te wijzigen.
2. Wijzig de naam in het dialoogvenster naar **df_Supplier_Snowflake**.
3. Druk op **Enter** om de naamswijziging op te slaan.

      ![A screenshot showing renaming of Dataflow1](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.012.png)

4. Selecteer in de rechteronderhoek **Publish**.

      ![A screenshot to Publish Dataflow](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.013.png)

      U wordt teruggestuurd naar het **Data Factory-scherm**. Het kan even duren voordat de Dataflow is gepubliceerd.

      >**Opmerking:** Soms wordt de naam van de Dataflow niet bijgewerkt. Volg in dat geval de onderstaande stappen. Als de Dataflow al is hernoemd, kunt u doorgaan naar de volgende taak.

5. Zodra Dataflow 1 klaar is met publiceren, gaan we de naam wijzigen. Klik op het **beletselteken (…)** naast Dataflow 1. Selecteer **Properties**.

      ![A screenshot to select Properties for Dataflow1](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.014.png)

6. Het dialoogvenster Dataflow properties opent. Wijzig de **naam** naar **df_Supplier_Snowflake**.
7. Voeg in het tekstvak **Description** toe: **Dataflow to ingest Supplier data from Snowflake to Lakehouse**.
8. Selecteer **Save**.

      ![A screenshot of Properties dialog of Dataflow1](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.015.png)

U wordt teruggestuurd naar het **Data Factory-scherm**. Laten we nu een dataflow aanmaken om gegevens uit Dataverse in te laden.

### <a name="_toc152198710"></a>Taak 5: Dataverse-query's kopiëren naar Dataflow

1. Selecteer in het bovenste menu **New -> Dataflow Gen2**.

      ![A screenshot to select New -> Dataflow Gen2](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.016.png)

      U wordt doorgestuurd naar de **Dataflow page**. Nu we vertrouwd zijn met Dataflow, gaan we de query's kopiëren vanuit Power BI Desktop naar Dataflow.

2. Als u het nog niet hebt geopend, open dan **FAIAD.pbix** in de map **Report** op het **bureaublad** van uw lab-omgeving.
3. Selecteer in het lint **Home -> Transform data**. Het Power Query-venster opent. Zoals u in het eerdere lab hebt opgemerkt, zijn de query's in het linker paneel georganiseerd per gegevensbron.
4. Het Power Query-venster opent. Selecteer in het linker paneel, onder de map DataverseData, via **Ctrl+Select** de volgende query's:
   1. BabyBoomer
   1. GenX
   1. GenY
   1. GenZ
   1. Customer
5. **Klik met de rechtermuisknop** en selecteer **Copy**.

      ![A screenshot copy queries from Power Query window](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.017.png)

6. Navigeer terug naar de **Dataflow page** in uw browser.
7. Druk in het **Dataflow pane** op **Ctrl+V** (momenteel wordt rechtsklikken en Plakken niet ondersteund).

   U ziet dat de vijf query's zijn geplakt en dat het Queries panel nu aan de linkerkant zichtbaar is. Omdat er nog geen verbinding is aangemaakt voor Dataverse, ziet u een waarschuwingsbericht met het verzoek de verbinding te configureren.

### <a name="_toc152198711"></a>Taak 6: Verbinding maken met Dataverse

1. Selecteer **Configure connection**.

      ![A screenshot Configure connection in Dataflow](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.018.png)

2. Het dialoogvenster Connect to data source opent. Zorg er in de **Connection** dropdown voor dat **Create new connection** is geselecteerd.
3. **Authentication kind** moet **Organizational Account** zijn.

      ![Picture80](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/e68c1646-3f3f-4b0c-841b-bcfc3faaaf2f)
   
4. Selecteer **Connect**.

### <a name="_toc152198712"></a>Taak 7: Data destination aanmaken voor Customer-query

De verbinding is tot stand gebracht en u kunt de gegevens bekijken in het voorbeeldvenster. U kunt naar eigen inzicht door de Applied Steps van de query's navigeren. Customer-gegevens zijn beschikbaar per categorie: BabyBoomer, GenX, GenY en GenZ. Deze vier query's worden samengevoegd om de Customer-query te maken. Nu moeten we de Customer-gegevens inladen in Lakehouse.

1. Zoals eerder vermeld, stagen we geen van deze gegevens. Klik daarom met de **rechtermuisknop** op de **Customer**-query in het Queries-venster en selecteer **Enable staging** om het vinkje te verwijderen.

      ![A screenshot to disable Staging](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.020.png)

2. Selecteer de **Customer**-query.
3. Selecteer in de rechteronderhoek **+** naast **Data destination**.
4. Selecteer **Lakehouse** in het dialoogvenster.

      ![A screenshot to configure Data Destination for Customer query](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.021.png)

5. Het dialoogvenster Connect to data destination opent. Selecteer in de **Connection dropdown** de optie **Lakehouse (none)**.
6. Selecteer **Next**.

      ![Picture81](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/3b11a768-0a6a-41e2-aabd-864aac096e62)

7. Het dialoogvenster Choose destination target opent. Zorg ervoor dat de **New table radio button** is geselecteerd, omdat we een nieuwe tabel aanmaken.
8. We willen de tabel aanmaken in de Lakehouse die we eerder hebben gemaakt. Navigeer in het linker paneel naar **Lakehouse -> de naam van uw workspace**.
9. Selecteer **lh_FAIAD**.
10. Laat de tabelnaam staan op **Customer**.
11. Selecteer **Next**.

      ![A screenshot of Choose destination target](../media/L4T3S5.png)

12. Het dialoogvenster Choose destination settings opent. Elke keer dat Dataflow Gen2 wordt vernieuwd, willen we een volledige laadbewerking uitvoeren. Zet de schakelaar **Use Automatic Settings** op **OFF** en zorg ervoor dat **Update method** is ingesteld op **Replace**.
13. U ziet een waarschuwing: "Some column names contain unsupported characters. Should we fix them for you?". Lakehouse ondersteunt geen kolomnamen met spaties. Selecteer **Fix it** om de waarschuwing te verwijderen.
14. Column mapping kan worden gebruikt om dataflow-kolommen te koppelen aan bestaande kolommen. In ons geval is het een New Table. Daarom kunnen we de standaardwaarden gebruiken. Selecteer **Save settings**.

    ![A screenshot of Choose destination settings](../media/L4T7S14.png)

### <a name="_toc152198713"></a>Taak 8: Dataverse Dataflow publiceren en hernoemen

1. U wordt teruggestuurd naar het **Power Query-venster**. U ziet dat **Data destination** in de **rechteronderhoek** is ingesteld op **Lakehouse**.
2. Selecteer in de rechteronderhoek **Publish**.

      ![A screenshot to Publish queries](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.024.png)

      **Opmerking:** U wordt teruggestuurd naar het **Data Factory-scherm**. Het kan even duren voordat de Dataflow is gepubliceerd.

1. Dataflow 1 is de dataflow waarmee we hebben gewerkt. Laten we de naam wijzigen voordat we verdergaan. Klik op het **beletselteken (…)** naast Dataflow 1. Selecteer **Properties**.
2. Het dialoogvenster Dataflow properties opent. Wijzig de **naam** naar **df\_Customer\_Dataverse**.
3. Voeg in het tekstvak **Description** toe: **Dataflow to ingest Customer data from Dataverse to Lakehouse**.
4. Selecteer **Save**.

      ![A screenshot of Properties dialog of Dataflow1](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.026.png)

      U wordt teruggestuurd naar het **Data Factory-scherm**. Laten we nu een dataflow aanmaken om gegevens uit SharePoint in te laden.

### <a name="_toc152198714"></a>Taak 9: SharePoint-query's kopiëren naar Dataflow

1. Selecteer in het bovenste menu **New -> Dataflow Gen2**.

      ![A screenshot to select New -> Dataflow Gen2](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.016.png)

      U wordt doorgestuurd naar de **Dataflow page**. Nu we vertrouwd zijn met Dataflow, gaan we de query's kopiëren vanuit Power BI Desktop naar Dataflow.

2. Als u het nog niet hebt geopend, open dan **FAIAD.pbix** in de map **Report** op het **bureaublad** van uw lab-omgeving.
3. Selecteer in het lint **Home -> Transform data**. Het Power Query-venster opent. Zoals u in het eerdere lab hebt opgemerkt, zijn de query's in het linker paneel georganiseerd per gegevensbron.
4. Het Power Query-venster opent. Selecteer in het linker paneel, onder de map SharepointData, de **People**-query.
5. **Klik met de rechtermuisknop** en selecteer **Copy**.

      ![A screenshot to copy queries from Power Query window](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.027.png)

6. Navigeer terug naar het **Dataflow-scherm** in de browser.
7. Druk in het **Dataflow pane** op **Ctrl+V** (momenteel wordt rechtsklikken en Plakken niet ondersteund).

   U ziet dat de query is geplakt en beschikbaar is in het linker paneel. Omdat er nog geen verbinding is aangemaakt met SharePoint, ziet u een waarschuwingsbericht met het verzoek de verbinding te configureren.

### <a name="_toc152198715"></a>Taak 10: SharePoint-verbinding aanmaken
1. Selecteer **Configure connection**.

      ![A screenshot to configure connection for People query in Dataflow](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.028.png)

2. Het dialoogvenster Connect to data source opent. Zorg er in de **Connection** dropdown voor dat **Create new connection** is geselecteerd.
3. **Authentication kind** moet **Organizational Account** zijn.
4. Selecteer **Connect**.

      ![A screenshot of Connect to data source](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.029.png)

### <a name="_toc152198716"></a>Taak 11: Data destination configureren voor People-query
De verbinding is tot stand gebracht en u kunt de gegevens bekijken in het voorbeeldvenster. U kunt naar eigen inzicht door de Applied Steps van de query's navigeren. Nu moeten we de People-gegevens inladen in Lakehouse.

1. Zoals eerder vermeld, stagen we geen van deze gegevens. Klik daarom met de **rechtermuisknop** op de **People**-query in het Queries-venster en selecteer **Enable staging** om het vinkje te verwijderen.

      ![A screenshot to disable Staging](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.030.png)

2. Selecteer de **People**-query.
3. Selecteer in de rechteronderhoek **+** naast **Data destination**.
4. Selecteer **Lakehouse** in het dialoogvenster.

      ![A screenshot to configure Data Destination for People query](../media/L4T3S5.png)

5. Het dialoogvenster Connect to data destination opent. Selecteer in de **Connection dropdown** de optie **Lakehouse (none)**.
6. Selecteer **Next**.

      ![A screenshot of Connect to data destination](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.008.png)

7. Het dialoogvenster Choose destination target opent. Zorg ervoor dat de **New table radio button** is geselecteerd, omdat we een nieuwe tabel aanmaken.
8. We willen de tabel aanmaken in de Lakehouse die we eerder hebben gemaakt. Navigeer in het linker paneel naar **Lakehouse-> de naam van uw workspace**.
9. Selecteer **lh_FAIAD**.
10. Laat de tabelnaam staan op **People**.
11. Selecteer **Next**.

      ![A screenshot of Choose destination target](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.032.png)

12. Het dialoogvenster Choose destination settings opent. Elke keer dat Dataflow Gen2 wordt vernieuwd, willen we een volledige laadbewerking uitvoeren. Zet de schakelaar **Use Automatic Settings** op **OFF** en zorg ervoor dat **Update method** is ingesteld op **Replace**.
13. U ziet een waarschuwing: "Some column names contain unsupported characters. Should we fix them for you?". Lakehouse ondersteunt geen kolomnamen met spaties. Selecteer **Fix it** om de waarschuwing te verwijderen.
14. Column mapping kan worden gebruikt om dataflow-kolommen te koppelen aan bestaande kolommen. In ons geval is het een New Table. Daarom kunnen we de standaardwaarden gebruiken. Selecteer **Save settings**.

      ![A screenshot of Choose destination settings](../media/L4T11S14.png)

### <a name="_toc152198717"></a>Taak 12: SharePoint Dataflow publiceren en hernoemen

1. U wordt teruggestuurd naar het **Power Query-venster**. U ziet dat **Data destination** in de rechteronderhoek is ingesteld op **Lakehouse**.

2. Selecteer in de rechteronderhoek **Publish**.

      ![A screenshot of publishing People query](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.034.png)

      >**Opmerking:** U wordt teruggestuurd naar het **Data Factory-scherm**. Het kan even duren voordat de Dataflow is gepubliceerd.

3. Dataflow 1 is de dataflow waarmee we hebben gewerkt. Laten we de naam wijzigen voordat we verdergaan. Klik op het **beletselteken (…)** naast Dataflow 1. Selecteer **Properties**.

      ![A screenshot of Dataflow1 -> Properties](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.014.png)

4. Het dialoogvenster Dataflow properties opent. Wijzig de **naam** naar **df_People_SharePoint**.
5. Voeg in het tekstvak **Description** toe: **Dataflow to ingest People data from SharePoint to Lakehouse**.
6. Selecteer **Save**.

      ![A screenshot of Dataflow1 dialog](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.035.png)

U wordt teruggestuurd naar het **Data Factory-scherm**. We hebben nu alle gegevens ingeladen in Lakehouse. In het volgende lab werken we verder met Lakehouse.

# **Referenties**
Fabric Analyst in a Day (FAIAD) introduceert u tot enkele van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service vindt u in de sectie Help (?) links naar een aantal uitstekende bronnen.

   ![A screenshot of help options](../media/Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.036.png)

Hieronder vindt u nog enkele aanvullende bronnen die u helpen bij uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [Microsoft Fabric GA-aankondiging](https://aka.ms/Fabric-Hero-Blog-Ignite23)
- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)
- Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)
- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)
- Leer nieuwe vaardigheden door de [Fabric Learning modules](https://aka.ms/learn-fabric) te verkennen
- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)
- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om uw vragen te stellen, feedback te delen en van anderen te leren

Lees de uitgebreidere aankondigingsblogs over de Fabric-ervaringen:

- [Data Factory experience in Fabric blog](https://aka.ms/Fabric-Data-Factory-Blog) 
- [Synapse Data Engineering experience in Fabric blog](https://aka.ms/Fabric-DE-Blog) 
- [Synapse Data Science experience in Fabric blog](https://aka.ms/Fabric-DS-Blog) 
- [Synapse Data Warehousing experience in Fabric blog](https://aka.ms/Fabric-DW-Blog) 
- [Synapse Real-Time Analytics experience in Fabric blog](https://aka.ms/Fabric-RTA-Blog)
- [Power BI announcement blog](https://aka.ms/Fabric-PBI-Blog)
- [Data Activator experience in Fabric blog](https://aka.ms/Fabric-DA-Blog) 
- [Administration and governance in Fabric blog](https://aka.ms/Fabric-Admin-Gov-Blog)
- [OneLake](https://aka.ms/Fabric-OneLake-Blog)[ in Fabric blog](https://aka.ms/Fabric-OneLake-Blog)
- [Dataverse and Microsoft Fabric integration blog](https://aka.ms/Dataverse-Fabric-Blog)


[A screenshot to Connect to data destination]: Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.008.png
[A screenshot to select Properties for Dataflow1]: Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.014.png
[A screenshot to select New -> Dataflow Gen2]: Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.016.png
[A screenshot to select Dataflow1 -> Properties]: Aspose.Words.76514971-fec6-4d06-9b79-6109687c7a81.025.png

© 2023 Microsoft Corporation. Alle rechten voorbehouden.

Door gebruik te maken van deze demo/dit lab gaat u akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation beschikbaar gesteld met het doel uw feedback te verkrijgen en u een leerervaring te bieden. U mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback te geven aan Microsoft. U mag het niet gebruiken voor enig ander doel. U mag deze demo/dit lab of een gedeelte ervan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, licentiëren, er afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN GEDEELTE ERVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE TEN BEHOEVE VAN VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARETECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN GEPRESENTEERD, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DEZELFDE MANIER ALS EEN DEFINITIEVE VERSIE. WE KUNNEN OOK BESLUITEN EEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN NIET UIT TE BRENGEN. UW ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK ANDERS ZIJN.

**FEEDBACK**. Als u feedback geeft over de technologiefuncties, -functionaliteit en/of -concepten die in deze demo/dit lab worden beschreven aan Microsoft, geeft u Microsoft, kosteloos, het recht om uw feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, te delen en te commercialiseren. U geeft ook aan derden, kosteloos, alle octrooirechten die nodig zijn voor hun producten, technologieën en diensten om specifieke onderdelen van Microsoft-software of -diensten die de feedback bevatten te gebruiken of ermee te communiceren. U geeft geen feedback die onderworpen is aan een licentie die Microsoft verplicht haar software of documentatie in licentie te geven aan derden omdat wij uw feedback erin opnemen. Deze rechten blijven van kracht na beëindiging van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, MET INBEGRIP VAN ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, EXPLICIET, IMPLICIET OF WETTELIJK, GESCHIKTHEID VOOR EEN BEPAALD DOEL, EIGENDOMSRECHT EN NIET-INBREUK. MICROSOFT GEEFT GEEN GARANTIES OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE UITVOER DIE VOORTVLOEIT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR ENIG DOEL.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een gedeelte van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen veranderen in toekomstige versies van het product. In deze demo/dit lab leert u over enkele, maar niet alle, nieuwe functies.
