
# Microsoft Fabric - Fabric Analyst in a Day - Lab 4

# ![](../media/Lab_4.1_1.png)

# Inhoud

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


# Introductie 

In ons scenario bevindt Supplier Data zich in Snowflake, Customer Data in Dataverse en Employee Data in SharePoint. Al deze databronnen worden op verschillende tijdstippen bijgewerkt. Om het aantal datavernieuwingen van Dataflows te minimaliseren, gaan we voor elk van deze databronnen afzonderlijke Dataflows aanmaken.

**Opmerking**: In één enkele Dataflow worden meerdere databronnen ondersteund.

Aan het einde van dit lab heb je geleerd: 

- Hoe je via Dataflow Gen2 verbinding maakt met Snowflake en data inlaadt in Lakehouse

- Hoe je via Dataflow Gen2 verbinding maakt met SharePoint en data inlaadt in Lakehouse

- Hoe je via Dataflow Gen2 verbinding maakt met Dataverse en data inlaadt in Lakehouse


# Dataflow Gen2

## Taak 1: Snowflake-query's kopiëren naar Dataflow

1. Navigeer terug naar de Fabric workspace **FAIAD_<username>** die je hebt aangemaakt in Lab 2, Taak 9.

2. Selecteer in het bovenste menu **+ New -> Dataflow Gen2**.
  
   ![](../media/Lab_4.1_2.png)

Je wordt doorgestuurd naar de **Dataflow-pagina**. Nu we bekend zijn met Dataflow, gaan we de query's vanuit Power BI Desktop kopiëren naar Dataflow.

3. Als je het nog niet hebt geopend, open dan **FAIAD.pbix** in de map **C:\FAIAD\Reports** van je labomgeving.

4. Selecteer in het lint **Home -> Transform data**. Het Power Query-venster opent. Zoals je in het eerdere lab hebt gezien, zijn de query's in het linkerdeelvenster georganiseerd per databron.

5. Het Power Query-venster opent. Selecteer in het linkerdeelvenster, onder de map SnowflakeData, de volgende query's via **Ctrl+Select** of Shift+Select:

    a.	SupplierCategories

    b.	Suppliers

    c.	Supplier

    d.	PO

    e.	PO Line Items

6. **Klik met de rechtermuisknop** en selecteer **Copy**.

    ![](../media/Lab_4.1_3.png)
 
7. Navigeer terug naar de **browser**.

8. Selecteer in het Dataflow-deelvenster het **centrale deelvenster** en voer **Ctrl+V** in (rechtsklikken en Plakken wordt momenteel niet ondersteund). Als je een MAC-apparaat gebruikt, gebruik dan Cmd+V om te plakken.

    >**Opmerking**: Als je werkt in de labomgeving, selecteer dan de ellipsis rechtsbovenaan het scherm. Gebruik de schuifregelaar om **VM Native Clipboard in te schakelen**. Selecteer OK in het dialoogvenster. Zodra je de query's hebt geplakt, kun je deze optie uitschakelen.

    ![](../media/Lab_4.1_4.png)
 

## Taak 2: Verbinding maken met Snowflake

De vijf query's zijn geplakt en je hebt nu het Queries-deelvenster aan de linkerkant. Omdat er nog geen verbinding is aangemaakt voor Snowflake, verschijnt er een waarschuwingsbericht met het verzoek om de verbinding te configureren.

1. Selecteer **Configure connection**.
 
    ![](../media/Lab_4.1_5.png)

2. Het dialoogvenster Connect to data source opent. Zorg er in de **Connection**-dropdown voor dat **Create new connection** is geselecteerd.

3. **Authentication kind** moet **Snowflake** zijn.

4. Voer de **Snowflake Username en Password** in die beschikbaar zijn op het tabblad Environment Variables (naast het tabblad Lab Guide).

5. Selecteer **Connect**.

    ![](../media/Lab_4.1_6.png)
 
    De verbinding is tot stand gebracht en je kunt de data bekijken in het voorbeelddeelvenster. Je kunt vrijelijk door de Applied Steps van de query's navigeren. De Suppliers-query bevat de gegevens van leveranciers en SupplierCategories bevat, zoals de naam al aangeeft, de leverancierscategorieën. Deze twee tabellen worden samengevoegd om de Supplier-dimensie te maken met de kolommen die we nodig hebben. Op dezelfde manier worden PO Line Items samengevoegd met PO om het PO-feit te creëren. Nu moeten we de Supplier- en PO-data inladen in Lakehouse.

6. Zoals eerder vermeld, slaan we geen van deze data op via staging. Klik daarom met de **rechtermuisknop** op de **Supplier**-query in het Queries-deelvenster en selecteer **Enable staging** om het vinkje te verwijderen.

    ![](../media/Lab_4.1_7.png)
 
7. Klik op dezelfde manier met de rechtermuisknop op de **PO**-query. Selecteer **Enable staging** om het vinkje te verwijderen.

   > **Opmerking**: Voor de overige drie query's hoeven we staging niet uit te schakelen, omdat Enable Load al was uitgeschakeld in Power BI Desktop (van waaruit deze query's zijn gekopieerd).

## Taak 3: Data Destination configureren voor Supplier- en PO-query's

1. Selecteer de **Supplier**-query.

2. Selecteer in het lint **Home -> Add data destination -> Lakehouse**.

    ![](../media/Lab_4.1_8.png)
 
3. Het dialoogvenster Connect to data destination opent. Selecteer in de **Connection dropdown** de optie **Lakehouse (none)**.

4. Selecteer **Next**.

    ![](../media/Lab_4.1_9.png)

5. Het dialoogvenster Choose destination target opent. Zorg ervoor dat de **New table radio button** is **geselecteerd**, omdat we een nieuwe tabel aanmaken.

6. We willen de tabel aanmaken in de Lakehouse die we eerder hebben gemaakt. Navigeer in het linkerdeelvenster naar **Lakehouse -> FAIAD_<username>**. 

7. Selecteer **lh_FAIAD**

8. Laat de tabelnaam staan als **Supplier**

9. Selecteer **Next**.

    ![](../media/Lab_4.1_10.png)
 
10. Het dialoogvenster Choose destination settings opent. Dit keer gebruiken we de automatische instellingen, omdat hiermee een volledige update van de data wordt uitgevoerd. Ook worden de kolommen indien nodig hernoemd. Selecteer **Save settings**.

    ![](../media/Lab_4.1_11.png)

11. Je wordt teruggestuurd naar het **Power Query-venster**. Let op dat in de rechteronderhoek **Data destination** is ingesteld op **Lakehouse**. Stel op dezelfde manier **de Data Destination in voor de PO-query**. Wanneer dit is gedaan, moet de Data Destination van je PO-query zijn ingesteld op **Lakehouse**, zoals weergegeven in de onderstaande schermafbeelding.
 
    ![](../media/Lab_4.1_12.png)

## Taak 4: Snowflake Dataflow hernoemen en publiceren

1. Selecteer bovenaan het scherm de **pijl naast Dataflow 2** om te hernoemen.

2. Wijzig in het dialoogvenster de naam naar **df_Supplier_Snowflake**

3. Klik op **Enter** om de naamswijziging op te slaan.

    ![](../media/Lab_4.1_13.png)
 
4. Selecteer in de rechteronderhoek **Publish**.

    ![](../media/Lab_4.1_14.png)
 
    Je wordt teruggestuurd naar de **FAIAD_<username> workspace**. Het kan even duren voordat de Dataflow is gepubliceerd. Laten we nu een dataflow aanmaken om data uit Dataverse in te laden.

## Taak 5: Dataverse-query's kopiëren naar Dataflow

1. Selecteer in het bovenste menu **+ New -> Dataflow Gen2**.

    ![](../media/Lab_4.1_15.png)
 
    Je wordt doorgestuurd naar de Dataflow-pagina. Nu we bekend zijn met Dataflow, gaan we de query's vanuit Power BI Desktop kopiëren naar Dataflow.

2. Als je het nog niet hebt geopend, open dan **FAIAD.pbix** in de map **C:\FAIAD\Reports** van je labomgeving. 

3. Selecteer in het lint **Home -> Transform data**. Het Power Query-venster opent. Zoals je in het eerdere lab hebt gezien, zijn de query's in het linkerdeelvenster georganiseerd per databron.

4. Het Power Query-venster opent. Selecteer in het linkerdeelvenster, onder de map DataverseData, de volgende query's via **Ctrl+Select**:

    a.	BabyBoomer

    b.	GenX

    c.	GenY

    d.	GenZ

    e.	Customer

5. **Klik met de rechtermuisknop** en selecteer **Copy**.

    ![](../media/Lab_4.1_16.png)
    
6. Navigeer terug naar de **Dataflow-pagina** in je browser.

7. Voer in het **Dataflow-deelvenster** **Ctrl+V** in (rechtsklikken en Plakken wordt momenteel niet ondersteund). Als je een MAC-apparaat gebruikt, gebruik dan Cmd+V om te plakken.

    **Opmerking**: Als je werkt in de labomgeving, selecteer dan de ellipsis rechtsbovenaan het scherm. Gebruik de schuifregelaar om VM Native Clipboard in te schakelen. Selecteer OK in het dialoogvenster. Zodra je de query's hebt geplakt, kun je deze optie uitschakelen.

## Taak 6: Verbinding maken met Dataverse

De vijf query's zijn geplakt en je hebt nu het Queries-deelvenster aan de linkerkant. Omdat er nog geen verbinding is aangemaakt voor Dataverse, verschijnt er een waarschuwingsbericht met het verzoek om de verbinding te configureren.

1. Selecteer **Configure connection**.
    
    ![](../media/Lab_4.1_17.png)
 
2. Het dialoogvenster Connect to data source opent. Zorg er in de **Connection dropdown** voor dat **Create new connection** is **geselecteerd**.

3. **Authentication kind** moet **Organizational Account** zijn.

4. Selecteer **Connect**.
  
    ![](../media/Lab_4.1_18.png)

## Taak 7: Data destination aanmaken voor Customer-query

De verbinding is tot stand gebracht en je kunt de data bekijken in het voorbeelddeelvenster. Je kunt vrijelijk door de Applied Steps van de query's navigeren. Customer-data is beschikbaar per categorie: BabyBoomer, GenX, GenY en GenZ. Deze vier query's worden samengevoegd om de Customer-query te maken. Nu moeten we de Customer-data inladen in Lakehouse.

1. Zoals eerder vermeld, slaan we geen van deze data op via staging. Klik daarom met de **rechtermuisknop** op de **Customer**-query in het Queries-deelvenster en selecteer **Enable staging** om het vinkje te verwijderen.

    ![](../media/Lab_4.1_19.png)
 
2. Selecteer de **Customer**-query.

3. Selecteer in het lint **Home -> Add data destination -> Lakehouse**.

    ![](../media/Lab_4.1_20.png)

4. Het dialoogvenster Connect to data destination opent. Selecteer in de **Connection dropdown** de optie **Lakehouse (none)**.

5. Selecteer **Next**.

    ![](../media/Lab_4.1_21.png)

6. Het dialoogvenster Choose destination target opent. Zorg ervoor dat de **New table radio button** is geselecteerd, omdat we een nieuwe tabel aanmaken.

7. We willen de tabel aanmaken in de Lakehouse die we eerder hebben gemaakt. Navigeer in het linkerdeelvenster naar **Lakehouse -> FAIAD_<username>**

8. Selecteer **lh_FAIAD**

9. Laat de tabelnaam staan als **Customer**

10. Selecteer **Next**.
 
    ![](../media/Lab_4.1_22.png)

11. Het dialoogvenster Choose destination settings opent. Dit keer gebruiken we de automatische instellingen, omdat hiermee een volledige update van de data wordt uitgevoerd. Ook worden de kolommen indien nodig hernoemd. Selecteer **Save settings**.
 
    ![](../media/Lab_4.1_23.png)

## Taak 8: Dataverse Dataflow publiceren en hernoemen

1. Je wordt teruggestuurd naar het **Power Query-venster**. Let op dat in de rechteronderhoek **Data destination** is ingesteld op **Lakehouse**.

2. Selecteer in de rechteronderhoek **Publish**.

    ![](../media/Lab_4.1_24.png)
 
    **Opmerking**: Je wordt teruggestuurd naar de **FAIAD_<username> workspace**. Het kan even duren voordat de Dataflow is gepubliceerd. 

3. Dataflow 2 is de dataflow waaraan we hebben gewerkt. Laten we deze hernoemen voordat we verdergaan. Klik op de **ellipsis (…)** naast Dataflow 1. Selecteer **Properties**.

    ![](../media/Lab_4.1_25.png)
 
4. Het dialoogvenster Dataflow properties opent. Wijzig de **Naam** naar **df_Customer_Dataverse**

5. Voeg in het tekstvak **Description** de tekst **Dataflow to ingest Customer data from Dataverse to Lakehouse** toe.

6. Selecteer **Save**.

    ![](../media/Lab_4.1_26.png)
 
    Je wordt teruggestuurd naar de **FAIAD_<username> workspace**. Laten we nu een dataflow aanmaken om data uit SharePoint in te laden.

## Taak 9: SharePoint-query's kopiëren naar Dataflow

1. Selecteer in het bovenste menu **New -> Dataflow Gen2**.

    ![](../media/Lab_4.1_27.png)
 
    Je wordt doorgestuurd naar de **Dataflow-pagina**. Nu we bekend zijn met Dataflow, gaan we de query's vanuit Power BI Desktop kopiëren naar Dataflow.

7. Als je het nog niet hebt geopend, open dan **FAIAD.pbix** in de map **C:\FAIAD\Reports** van je labomgeving. 

8. Selecteer in het lint **Home -> Transform data**. Het Power Query-venster opent. Zoals je in het eerdere lab hebt gezien, zijn de query's in het linkerdeelvenster georganiseerd per databron.

9. Het Power Query-venster opent. Selecteer in het linkerdeelvenster, onder de map SharepointData, de **People**-query.

10. **Klik met de rechtermuisknop** en selecteer **Copy**.
  
    ![](../media/Lab_4.1_28.png)

11. Navigeer terug naar het **Dataflow-scherm** in de browser.

12.	Voer in het **Dataflow-deelvenster** **Ctrl+V** in (rechtsklikken en Plakken wordt momenteel niet ondersteund).

   	> **Opmerking**: Als je werkt in de labomgeving, selecteer dan de ellipsis rechtsbovenaan het scherm. Gebruik de schuifregelaar om **VM Native Clipboard in te schakelen**. Selecteer OK in het dialoogvenster. Zodra je de query's hebt geplakt, kun je deze optie uitschakelen.
    >
    > **Opmerking**: Let op dat de query is geplakt en beschikbaar is in het linkerdeelvenster. Omdat er nog geen verbinding is aangemaakt met SharePoint, verschijnt er een waarschuwingsbericht met het verzoek om de verbinding te configureren.

## Taak 10: SharePoint-verbinding aanmaken

1. Selecteer **Configure connection**.
 
    ![](../media/Lab_4.1_29.png)

2. Het dialoogvenster Connect to data source opent. Zorg er in de **Connection**-dropdown voor dat **Create new connection** is geselecteerd.

3. **Authentication kind** moet **Organizational Account** zijn.

4. Selecteer **Connect**.

    ![](../media/Lab_4.1_30.png)
 
## Taak 11: Data destination configureren voor People-query

De verbinding is tot stand gebracht en je kunt de data bekijken in het voorbeelddeelvenster. Je kunt vrijelijk door de Applied Steps van de query's navigeren. Nu moeten we People-data inladen in Lakehouse.

1. Zoals eerder vermeld, slaan we geen van deze data op via staging. Klik daarom met de **rechtermuisknop** op de **People**-query in het Queries-deelvenster en selecteer **Enable staging** om het vinkje te verwijderen.

    ![](../media/Lab_4.1_31.png)
 
2. Selecteer de **People**-query.

3. Selecteer in het lint **Home -> Add data destination -> Lakehouse**.
 
    ![](../media/Lab_4.1_32.png)

4. Het dialoogvenster Connect to data destination opent. Selecteer in de **Connection dropdown** de optie **Lakehouse (none)**.

5. Selecteer **Next**.

    ![](../media/Lab_4.1_33.png)
 
6. Het dialoogvenster Choose destination target opent. Zorg ervoor dat de **New table radio button** is geselecteerd, omdat we een nieuwe tabel aanmaken.

7. We willen de tabel aanmaken in de Lakehouse die we eerder hebben gemaakt. Navigeer in het linkerdeelvenster naar **Lakehouse -> FAIAD_<username>**. 

8. Selecteer **lh_FAIAD**

9. Laat de tabelnaam staan als **People**

10. Selecteer **Next**.

    ![](../media/Lab_4.1_34.png)
 
11. Het dialoogvenster Choose destination settings opent. Dit keer gebruiken we de automatische instellingen, omdat hiermee een volledige update van de data wordt uitgevoerd. Ook worden de kolommen indien nodig hernoemd. Selecteer **Save settings**.

    ![](../media/Lab_4.1_35.png)
 
## Taak 12: SharePoint Dataflow publiceren en hernoemen

1. Je wordt teruggestuurd naar het **Power Query-venster**. Let op dat in de **rechteronderhoek** Data destination is ingesteld op **Lakehouse**.

2. Selecteer in de rechteronderhoek **Publish**.

    ![](../media/Lab_4.1_36.png)
 
    **Opmerking**: Je wordt teruggestuurd naar de **FAIAD_<username> workspace**. Het kan even duren voordat de Dataflow is gepubliceerd. 

3. Dataflow 2 is de dataflow waaraan we hebben gewerkt. Laten we deze hernoemen voordat we verdergaan. Klik op de **ellipsis (…)** naast Dataflow 2. Selecteer **Properties**.

    ![](../media/Lab_4.1_37.png)
 
4. Het dialoogvenster Dataflow properties opent. Wijzig de **naam** naar **df_People_SharePoint**

5. Voeg in het tekstvak **Description** de tekst **Dataflow to ingest People data from SharePoint to Lakehouse** toe.

6. Selecteer **Save**.

   ![](../media/Lab_4.1_38.png)
 
Je wordt teruggestuurd naar de **FAIAD_<username> workspace**. We hebben nu alle data ingeladen in Lakehouse. In het volgende lab plannen we een Dataflow-vernieuwing.

# Referenties
Fabric Analyst in a Day (FAIAD) maakt je vertrouwd met een aantal van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service vind je in het gedeelte Help (?) links naar uitstekende bronnen.

   # ![](../media/img18.png) 
 
Hieronder vind je nog een aantal bronnen die je helpen bij je volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [Microsoft Fabric GA-aankondiging](https://aka.ms/Fabric-Hero-Blog-Ignite23)
- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)
- Meld je aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)
- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)
- Leer nieuwe vaardigheden door de [Fabric Learning-modules](https://aka.ms/learn-fabric) te volgen
- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)
- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om je vragen te stellen, feedback te delen en van anderen te leren

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

Door gebruik te maken van deze demo/dit lab, ga je akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met als doel feedback van jou te ontvangen en jou een leerervaring te bieden. Je mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback aan Microsoft te geven. Je mag het niet voor andere doeleinden gebruiken. Je mag deze demo/dit lab of een deel daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, er afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN DEEL DAARVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE VOOR VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARE-TECHNOLOGIE/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, WAARONDER MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN IN DEZE DEMO/DIT LAB VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DEZELFDE MANIER ALS EEN DEFINITIEVE VERSIE. WE BRENGEN MOGELIJK OOK GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UIT. JE ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK ANDERS ZIJN.

**FEEDBACK**. Als je feedback geeft over de technologiefuncties, -functionaliteit en/of -concepten die in deze demo/dit lab worden beschreven aan Microsoft, geef je Microsoft kosteloos het recht om je feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, te delen en te commercialiseren. Je geeft ook aan derden, kosteloos, eventuele octrooirechten die nodig zijn voor hun producten, technologieën en diensten om bepaalde onderdelen van een Microsoft-software of -service die de feedback bevat te gebruiken of te koppelen. Je geeft geen feedback die onderworpen is aan een licentie die Microsoft verplicht zijn software of documentatie aan derden in licentie te geven omdat we je feedback daarin opnemen. Deze rechten blijven van kracht na beëindiging van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, MET INBEGRIP VAN ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, ONGEACHT OF DEZE UITDRUKKELIJK, IMPLICIET OF WETTELIJK ZIJN, GESCHIKTHEID VOOR EEN BEPAALD DOEL, EIGENDOMSRECHT EN NIET-INBREUK. MICROSOFT GEEFT GEEN VERZEKERINGEN OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE UITVOER DIE VOORTKOMT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR EEN BEPAALD DOEL.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen veranderen in toekomstige versies van het product. In deze demo/dit lab leer je over enkele, maar niet alle, nieuwe functies.
