# Microsoft Fabric - Fabric Analyst in a Day - Lab 3

# ![](../media/ImageNew_faided3.1_1.png)

# Inhoud
   * Inleiding	3

   * Dataflow Gen2

     * Taak 1: Dataflow Gen2 aanmaken

     * Taak 2: Verbinding maken met ADLS Gen2

     * Taak 3: Base ADLS Gen2 folder query aanmaken

     * Taak 4: Cities query aanmaken

     * Taak 5: Countries query aanmaken

     * Taak 6: States aanmaken via Copy – Optie 1

     * Taak 7: Geo query aanmaken via Copy – Optie 2

     * Taak 8: Data Destination configureren voor de Geo query

     * Taak 9: Dataflow publiceren

     * Taak 10: Dataflow hernoemen

     * Taak 11: Overige queries bouwen in Dataflow

     * Taak 12: Data destination configureren voor overige queries

   * Referenties

# **Inleiding**
In ons scenario zijn de verkoopgegevens afkomstig uit het ERP-systeem en opgeslagen in een ADLS Gen2-database. De gegevens worden elke dag om 12:00 uur bijgewerkt. We moeten deze gegevens transformeren en inladen in de Lakehouse om ze in ons model te gebruiken.

Er zijn meerdere manieren om deze gegevens in te laden.

- **Shortcuts:** Dit biedt geen mogelijkheid om gegevens te transformeren.
- **Notebooks:** Hiervoor is het schrijven van code vereist. Dit is een ontwikkelaarsvriendelijke aanpak.
- **Dataflow Gen2:** U bent waarschijnlijk bekend met Power Query of Dataflow Gen1. Dataflow Gen2 is, zoals de naam al aangeeft, de nieuwere versie van Dataflow. Het biedt alle mogelijkheden van Power Query / Dataflow Gen1, aangevuld met de mogelijkheid om gegevens te transformeren en in te laden in meerdere databronnen. We introduceren dit in de komende labs.
- **Data Pipeline:** Dit is een orchestratietool. Activiteiten kunnen worden georkestreerd om gegevens te extraheren, transformeren en inladen. We gebruiken Data Pipeline om een Dataflow Gen2-activiteit uit te voeren, die op zijn beurt de extractie, transformatie en inlading uitvoert.

We beginnen met Dataflow Gen2 om de verbinding met de databron en de benodigde transformaties aan te maken. Vervolgens gebruiken we Data Pipeline om de Dataflow Gen2 te orkestreren/uitvoeren.

Aan het einde van dit lab hebt u het volgende geleerd:

- Hoe u een Dataflow Gen2 aanmaakt
- Hoe u met Dataflow Gen2 verbinding maakt met ADLS Gen2 en gegevens transformeert
- Hoe u gegevens inlaadt in de Lakehouse


# **Dataflow Gen2**
### Taak 1: Dataflow Gen2 aanmaken
1. Navigeer terug naar de **Fabric workspace** die u hebt aangemaakt in het eerdere Lab 2, Taak 9.
1. Als u na het vorige lab niet van scherm bent gewisseld, bevindt u zich nog in het Lakehouse-scherm. Als u wel van scherm bent gewisseld, is dat geen probleem. Selecteer het pictogram van de **Fabric experience selector** linksonder in uw scherm.
1. Selecteer **Data Factory** in het geopende Fabric experience-dialoogvenster. Data Factory bevat de workloads die nodig zijn om gegevens te extraheren, transformeren en inladen.

   ![A screenshot of a dialog to select Data Factory experience](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.002.png)

1. U wordt doorgestuurd naar de Data Factory Home-pagina. Selecteer onder New de optie **Dataflow Gen2**.

   ![A screenshot of Data Factory Home selecting Dataflow Gen2](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.003.png)

U wordt doorgestuurd naar de **Dataflow-pagina**. Dit scherm zal vertrouwd aanvoelen, want het lijkt op Dataflow Gen1 of Power Query. U zult merken dat er opties beschikbaar zijn om verbinding te maken met diverse databronnen, samen met de mogelijkheid om gegevens te transformeren. Laten we verbinding maken met de ADLS Gen2-databron en enkele transformaties uitvoeren.
### Taak 2: Verbinding maken met ADLS Gen2
1. Selecteer in het lint **Home -> Get data -> More…**

   ![A screenshot of Dataflow screen to select Get Data](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.004.png)

1. U wordt doorgestuurd naar het dialoogvenster **Get data Choose data source**. U kunt naar een databron zoeken door iets in het zoekvak te typen. In het linkerdeelvenster zijn er opties om een Blank table of Blank query te gebruiken. U vindt ook een nieuwe optie om bestanden te uploaden. Deze optie verkennen we in een later lab. Klik voor nu op **View more ->** in de rechterbovenhoek van uw scherm.

   ![A screenshot of Choose data source](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.005.png)

   Nu kunt u alle beschikbare databronnen bekijken. U hebt de optie om de databronnen te filteren op File, Database, Microsoft Fabric, Power Platform, Azure, enzovoort.

    ![A screenshot of available data sources](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.006.png)

1. Selecteer **Azure** bovenaan om te filteren op Azure-databronnen.
1. Selecteer **Azure Data Lake Storage Gen2**.

   ![A screenshot of select Azure Data Lake Storage Gen2](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.007.png)

1. U wordt doorgestuurd naar het dialoogvenster Connect to Data Source. U moet een verbinding aanmaken met de ADLS Gen2-databron. Voer onder **Connection Settings -> URL** het volgende in:
   ```
   https://stvnextblobstorage.dfs.core.windows.net/fabrikam-sales/Delta-Parquet-Format
   ```
   ![A screenshot of Connect to data source](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.008.png)

1. Selecteer **Account Key** in de vervolgkeuzelijst Authentication kind.
1. Kopieer de **Adls storage account Access Key** uit het tabblad **Environment Variables** (naast het tabblad Lab Guide) en plak deze in het tekstvak Account key.

   ![A screenshot of Connect to data source](../media/new6.png)

1. Selecteer **Next** rechtsonder in het scherm.

### Taak 3: Base ADLS Gen2 folder query aanmaken
1. Zodra de verbinding tot stand is gebracht, wordt u doorgestuurd naar het scherm **Preview folder data**. Er staan veel bestanden in de ADLS Gen2-map. We hebben gegevens uit slechts enkele van deze bestanden nodig. Selecteer **Create** om een verbinding met de map te maken.

   ![A screenshot of Preview folder dialog](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.010.png)

1. U bent terug in het **Power Query**-dialoogvenster. Dit wordt de verbinding met de hoofdmap van ADLS Gen2. We verwijzen naar deze query in volgende queries. Laten we de query hernoemen. Wijzig in het rechterdeelvenster, onder **Query settings -> Properties -> Name**, de naam in **ADLS Base Folder for Geo** en druk op Enter.
1. Alle queries uit Dataflow Gen2 worden standaard geladen naar een Staging Lakehouse. In dit lab gaan we geen gegevens stagen. Om dit laden uit te schakelen, klikt u in het **linkerdeelvenster met de rechtermuisknop op de query ADLS Base Folder for Geo**.

   >**Opmerking:** Staging wordt gebruikt wanneer we gegevens tijdelijk moeten opslaan voor verdere transformatie voordat ze beschikbaar zijn voor gebruik.

1. **Schakel de optie Enable Staging uit**.

   ![A screenshot to disable Staging](../media/faiadlab2-4.png)

   Er zijn twee bestandsindelingen in de map: **json** en **parquet**.

   - **Parquet:** is een open-source bestandsindeling die is ontworpen voor platte kolomgebaseerde opslagformaten. Parquet werkt goed met complexe gegevens in grote volumes en staat bekend om zijn krachtige gegevenscompressie en zijn vermogen om een breed scala aan coderingstypen te verwerken.

   - **Json:** een bestand dat metadata bevat, zoals het schema en het gegevenstype van het parquet-bestand.

1. We hebben alleen het parquet-bestand nodig, omdat dit de gegevens bevat die we nodig hebben. Selecteer de **vervolgkeuzepijl van de kolom Extension**.

1. **Schakel .json uit** zodat er gefilterd wordt op .parquet-bestanden.
1. Selecteer **OK**.

   ![A screenshot to filter out json files](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.012.png)

De Base query is nu ingesteld. We kunnen hier voor alle queries van de ADLS Gen2-bron naar verwijzen.

### Taak 4: Cities query aanmaken
Verkoopgegevens zijn beschikbaar op het niveau van Geography, Product, verkoper en Date. Laten we eerst een query aanmaken om de Geo-dimensie op te halen. Geo-gegevens zijn beschikbaar in drie verschillende bestanden in de volgende submappen:

- **Cities:** Application.Cities
- **Countries:** Application.Countries
- **State:** Application.StateProvinces

We moeten de gegevens over City, State en Country uit deze drie bestanden combineren om de Geo-dimensie aan te maken.

1. Laten we beginnen met City. In het linkerdeelvenster klikt u **met de rechtermuisknop op ADLS Base Folder for Geo**. Selecteer **Reference** om een nieuwe query aan te maken die verwijst naar de ADLS Base Folder-query.

   ![A screenshot to Reference ADLS Base folder](../media/faiadlab2-5.png)

1. Selecteer de **vervolgkeuzepijl van de kolom Folder Path**.
1. Selecteer **Text filters -> Contains...**

   ![A screenshot to filter Folder Path](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.014.png)

1. Voer in het dialoogvenster **Filter rows** de waarde **Application.Cities** in.

   >**Opmerking:** Dit is hoofdlettergevoelig.

1. Selecteer **OK**.

   ![A screenshot of Filter Rows dialog](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.015.png)

1. De gegevens worden gefilterd tot één rij. Selecteer **Binary** onder de kolom **Content**.

   ![Screenshot of ADLS Base Folder(2)](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.016.png)

1. U ziet nu alle City-gegevens. Wijzig in het **rechterdeelvenster**, onder **Query settings -> Properties -> Name**, de naam in **Cities** en druk op Enter.

    >**Opmerking:** Controleer in de rechterbenedenhoek van de schermafbeelding of de query vier stappen heeft en wacht tot de query klaar is met laden. Dit kan enkele minuten duren.

      ![A screenshot to Rename query](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.017.png)

In het rechterdeelvenster, onder **Applied steps**, zijn alle stappen geregistreerd. Dit gedrag is vergelijkbaar met Power Query. Laten we nu een soortgelijk proces volgen om een **Country**-query aan te maken.

### Taak 5: Countries query aanmaken

1. In het linkerdeelvenster klikt u **met de rechtermuisknop op ADLS Base Folder for Geo**. Selecteer **Reference** om een nieuwe query aan te maken die verwijst naar de ADLS Base Folder-query.

   ![A screenshot to reference ADLS Base Folder](../media/faiadlab2-5.png)

1. Selecteer de **vervolgkeuzepijl van de kolom Folder Path**.

1. Selecteer **Text filters -> Contains...**

   ![A screenshot to filter by Folder Path](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.019.png)

1. Voer in het **dialoogvenster Filter rows** de waarde **Application.Countries** in.

   >**Opmerking:** Dit is hoofdlettergevoelig.

1. Selecteer **OK**.

   ![A screenshot of Filter rows dialog](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.020.png)

1. De gegevens worden gefilterd tot één rij. Selecteer **Binary** onder de kolom **Content**.

   ![Screenshot of ADLS Base Folder(2)](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.021.png)

1. U ziet nu alle Country-gegevens. Wijzig in het **rechterdeelvenster**, onder **Query settings -> Properties -> Name**, de naam in **Countries** en druk op Enter.

    >**Opmerking:** Controleer in de rechterbenedenhoek van de schermafbeelding of de query vier toegepaste stappen heeft en wacht tot de query klaar is met laden. Dit kan enkele minuten duren.

    ![A screenshot to Rename query](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.022.png)

We moeten hierna State inladen, maar de stappen worden steeds herhalender. We hebben de queries al in het Power BI Desktop-bestand staan. Laten we kijken of we de queries van daaruit kunnen kopiëren.

### Taak 6: States aanmaken via Copy – Optie 1

1. Als u het nog niet hebt geopend, open dan **FAIAD.pbix** in de map **Report** op het **bureaublad** van uw lab-omgeving.

1. Selecteer in het lint **Home -> Transform data -> Transform data**. Het Power Query-venster wordt geopend. Zoals u in het eerdere lab hebt gezien, zijn de queries in het linkerdeelvenster georganiseerd per databron.

   ![A screenshot of Power BI Desktop report.](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.023.png)

1. Klik in het linkerdeelvenster, onder de map ADLSData, met de rechtermuisknop op de query **States** en selecteer **Copy**.

   ![A screenshot Power Query window](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.024.png)

1. Navigeer terug naar de **browser**. U bevindt zich nu in de Dataflow waaraan we werkten.
1. Selecteer in het linkerdeelvenster het paneel **Queries** en druk op **Ctrl+V** (rechtsklikken en Plakken wordt momenteel niet ondersteund). Als u een **Mac-apparaat** gebruikt, gebruik dan **Cmd+V** om te plakken.

   >**Opmerking**: Als u in de lab-omgeving werkt, selecteer dan de ellips rechtsboven in het scherm. Gebruik de schuifregelaar om **VM Native Clipboard** in te schakelen. Selecteer OK in het dialoogvenster. Nadat u de query hebt geplakt, kunt u deze optie weer uitschakelen.

      ![A screenshot Dataflow queries](../media/faiadlab2-6.png)

      U ziet dat ook **ADLS Base Folder** wordt gekopieerd. Dit komt doordat States in Power BI Desktop verwijst naar de ADLS Base Folder, maar we hebben al een ADLS Base Folder. Laten we dit oplossen.

1. Selecteer de query **States**.
1. Selecteer in het **rechterdeelvenster**, onder **Applied** **steps**, de stap **Source**.
1. Wijzig in de formulebalk **#"ADLS Base Folder"** in **#"ADLS Base Folder for Geo"**.

   ![A screenshot of States query Source step](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.026.png)

1. Klik op het **vinkje** naast de formulebalk of druk op **Enter**.

   ![A screenshot of States query Source step after updating formula bar](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.027.png)

1. Nu kunnen we de ADLS Base Folder (2) verwijderen. Klik in het linkerdeelvenster, onder de sectie **Queries**, met de **rechtermuisknop** op de query **ADLS Base Folder** en selecteer **Delete**.

   ![A screenshot of delete ADLS Base Folder (2) delete](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.028.png)

1. Het dialoogvenster voor het verwijderen van de query verschijnt. Selecteer **Delete** ter bevestiging.

   >**Opmerking:** Controleer of de query vier toegepaste stappen heeft en wacht tot de query klaar is met laden. Dit kan enkele minuten duren.

### Taak 7: Geo query aanmaken via Copy – Optie 2

Nu moeten we deze queries samenvoegen om de Geo-dimensie aan te maken. Laten we de query opnieuw kopiëren vanuit het Power BI Desktop-bestand. Deze keer kopiëren we de code vanuit Advanced Editor.

1. Navigeer terug naar het **Power Query-venster** van het Power BI Desktop-bestand.
1. Selecteer in het linkerdeelvenster, onder **Queries**, de query **Geo** in de map ADLSData.
1. Selecteer in het lint **Home -> Advanced Editor**.

   ![A screenshot of Power Query window from Power BI Desktop](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.029.png)

1. Het venster Advanced Editor wordt geopend. **Selecteer alle tekst** in Advanced Editor.
1. Klik met de **rechtermuisknop** en selecteer **Copy**.

   ![A screen shot of Advanced Editor](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.030.png)

1. Selecteer de **X** in de rechterbovenhoek van het venster of selecteer **Done** om het venster Advanced Editor te sluiten.
1. Navigeer terug naar het **Dataflow**-venster in de browser.
1. Selecteer in het lint **Get data -> Blank query**.

   ![A screenshot of Get Data -> Blank Query in Dataflow](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.031.png)

1. Het dialoogvenster Get data, Connect to the data source Advanced Editor wordt geopend. **Selecteer alle tekst** in de editor.
1. Druk op **Delete** op uw toetsenbord om alle tekst te verwijderen.
1. Advanced Editor is nu leeg. Druk nu op **Ctrl+V** om de inhoud te plakken die u hebt gekopieerd vanuit de Advanced Editor van Power BI Desktop.
1. Selecteer **Next**.

   ![A screenshot of Advanced Editor](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.032.png)

1. We hebben nu de Geo-dimensie. Laten we de query hernoemen. Wijzig in het **rechterdeelvenster**, onder **Query settings -> Properties -> Name**, de naam in **Geo**.

   >**Opmerking:** Wacht tot de query klaar is met laden. Dit kan enkele minuten duren.

Laten we de stappen doorlopen om te begrijpen hoe Geo is aangemaakt. Selecteer in het rechterdeelvenster, onder Applied Steps, de stap **Source**. Als u naar de formulebalk kijkt of op Settings klikt, ziet u dat de bron van deze query een samenvoeging is van Cities en States. Door de stappen te doorlopen ziet u dat het resultaat van de eerste samenvoeging op zijn beurt wordt samengevoegd met Countries. Alle drie de queries worden dus gebruikt om een Geo-dimensie aan te maken.

   ![A screenshot of Formula bar for Geo query](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.033.png)

### Taak 8: Data Destination configureren voor de Geo query

Nu we een dimensie hebben, gaan we deze gegevens inladen in de Lakehouse. Dit is de nieuwe functie die beschikbaar is in Dataflow Gen2.

1. Zoals eerder vermeld, stagen we geen van deze gegevens. Klik daarom met de **rechtermuisknop** op de query **Cities** en selecteer **Enable staging** om het vinkje te verwijderen.

   ![A screenshot to disable Staging](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.034.png)

1. Volg dezelfde stappen voor de queries **Countries en Geo** **om het vinkje naast Enable staging te verwijderen**.

1. Selecteer de query **Geo**.

1. Selecteer in de rechterbenedenhoek **+** naast **Data destination**.

1. Selecteer **Lakehouse** in het dialoogvenster.

   ![A screenshot select Data Destination](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.035.png)

1. Het dialoogvenster Connect to data destination wordt geopend. We moeten een nieuwe verbinding met de Lakehouse aanmaken. Zorg dat **Create new connection** is geselecteerd in de **Connection dropdown** en dat **Authentication kind** is ingesteld op **Organizational account**, en selecteer vervolgens **Next**.

   ![A screenshot of Connect to data destination](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.036.png)

1. Zodra de verbinding is aangemaakt, wordt het dialoogvenster Choose destination target geopend. Zorg dat de **keuzeknop New table** is geselecteerd, omdat we een nieuwe tabel aanmaken.
1. We willen de tabel aanmaken in de Lakehouse die we eerder hebben aangemaakt. Navigeer in het linkerdeelvenster naar **Lakehouse -> FAIAD_username**.
1. Selecteer **lh\_FAIAD**.
1. Laat de tabelnaam staan op **Geo**.
1. Selecteer **Next**.

   ![A screenshot to Choose destination target](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.037.png)

1. Het dialoogvenster Choose destination settings wordt geopend. Gebruik de schuifregelaar om de automatische instellingen uit te schakelen. Laten we de opties bekijken.
   U ziet dat er opties zijn om gegevens toe te voegen aan een bestaande tabel of te vervangen.
   U ziet ook Schema-opties bij publiceren. U kunt kiezen voor een vast schema, of als het schema in de loop van de tijd zal veranderen, is er een optie voor een dynamisch schema.

1. U ziet een waarschuwing dat "Some column names contain unsupported characters. Should we fix them for you?" De Lakehouse ondersteunt geen kolomnamen met spaties. Als u Fix it selecteert, worden de spaties in kolomnamen vervangen door underscores.

   >**Opmerking:** Met het selectievakje rechts van de bronkolom kunt u alleen de kolommen selecteren die u wilt laden naar de Lakehouse.

1. In ons scenario maken we gebruik van de automatische instellingen. **Schakel de schuifregelaar Use automatic settings in**. U ziet dat de doelkolomnamen automatisch worden gecorrigeerd met een underscore.

1. Kolomkoppeling kan worden gebruikt om dataflow-kolommen te koppelen aan bestaande kolommen. In ons geval is dit een nieuwe tabel, dus we kunnen de standaardwaarden gebruiken. Selecteer **Save settings**.

   ![A screenshot to Choose destination settings](../media/Fabrichey1.png)


### Taak 9: Dataflow publiceren

1. U wordt teruggeleid naar het **Power Query-venster**. U ziet dat in de rechterbenedenhoek **Data destination is ingesteld op Lakehouse**.

1. Laten we deze queries publiceren zodat we de Lakehouse kunnen bekijken. We komen later terug om meer queries toe te voegen. Selecteer rechtsonder **Publish**.

   ![A screenshot to Publish Dataflow](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.039.png)

1. U wordt teruggeleid naar de werkruimte **FAIAD_<username>**. Het kan enkele ogenblikken duren voordat de Dataflow is gepubliceerd. Zodra dit klaar is, selecteert u **lh_FAIAD Lakehouse** in het middelste deelvenster of het linkerdeelvenster.

   ![A screenshot to select Lakehouse](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.040.png)

1. U wordt doorgestuurd naar het **Lakehouse Explorer-scherm**. Vouw in het linkerdeelvenster **lh\_FAIAD -> Tables** uit.

1. U ziet dat er nu een Geo-tabel in de Lakehouse staat. Vouw **Geo** uit en bekijk alle kolommen.

1. Selecteer de tabel **Geo** en de gegevensvoorvertoning wordt geopend in het rechterdeelvenster.

   ![A screenshot to explore Lakehouse tables](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.041.png)

Er is ook een SQL Endpoint beschikbaar waarmee u deze tabel kunt opvragen. We bekijken deze optie in een later lab. Nu we weten dat de Geo-gegevens zijn geland in de Lakehouse, gaan we de rest van de gegevens ophalen uit ADLS Gen2.

### Taak 10: Dataflow hernoemen

1. Selecteer in de linker menubalk **FAIAD_username** om terug te navigeren naar de **werkruimte**.

1. We werken met Dataflow 1. Laten we dit hernoemen voordat we verdergaan. Klik op de **ellips (…)** naast Dataflow 1. Selecteer **Properties**.

   ![A screenshot to select Dataflow1 Properties](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.042.png)

1. Het dialoogvenster Dataflow properties wordt geopend. Wijzig de naam in **df_Sales_ADLS**.

   >**Opmerking:** We voegen de prefix **df** toe aan de naam van de Dataflow. Dit maakt het gemakkelijker om te zoeken en te sorteren.

1. Voeg in het tekstvak **Description** de tekst **Dataflow to ingest Sales Data from ADLS to Lakehouse** toe.
1. Selecteer **Save**.

   ![A screenshot Dataflow Properties dialog](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.043.png)

### Taak 11: Overige queries bouwen in Dataflow

1. U wordt teruggeleid naar de werkruimte **FAIAD_<username>**. Selecteer de Dataflow **df_Sales_ADLS** om terug te navigeren naar de dataflow.

   ![A screenshot to select df_Sales_ADLS](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.044.png)

   Laten we kijken of we de queries kunnen kopiëren vanuit Power BI Desktop om het eenvoudiger te maken.

1. Als u het nog niet hebt geopend, open dan **FAIAD.pbix** in de map **C:\FAIAD\Reports** van uw lab-omgeving.

1. Selecteer in het lint **Home -> Transform**. Het Power Query-venster wordt geopend.
1. Selecteer in het paneel **Queries** aan de linkerkant de volgende queries uit **ADLSData** via **Ctrl+klik**.

   1. Product
   1. Product Groups
   1. Product Item Group
   1. Product Details
   1. Invoice
   1. InvoiceLineItems
   1. Sales
   1. BuyingGroup
   1. Reseller
   1. Date

      ![A screenshot to copy queries from Power Query window](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.045.png)

1. Klik met de **rechtermuisknop** en selecteer **Copy**.

   ![A screenshot to copy queries from Power Query window](../media/new7.png)

1. Navigeer terug naar het Dataflow-venster van **df\_Sales\_ADLS** in de browser.

1. Selecteer in het linkerdeelvenster het paneel **Queries** en druk op **Ctrl+V** (rechtsklikken en Plakken wordt momenteel niet ondersteund). Als u een **Mac-apparaat** gebruikt, gebruik dan **Cmd+V** om te plakken.

   >**Opmerking**: Als u in de lab-omgeving werkt, selecteer dan de ellips rechtsboven in het scherm. Gebruik de schuifregelaar om VM Native Clipboard in te schakelen. Selecteer OK in het dialoogvenster. Nadat u de queries hebt geplakt, kunt u deze optie weer uitschakelen.
   ![A screenshot copying queries to dataflow](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.046.png)

1. Zoals eerder vermeld, stagen we geen van deze gegevens. Klik daarom met de **rechtermuisknop** op de volgende queries en selecteer **Enable staging** om het vinkje te verwijderen.

   1. Product

   1. Product Details

   1. Reseller

   1. Date

   1. Sales

   >**Opmerking:** Als laden is uitgeschakeld in Power BI Desktop, hoeven we staging in Dataflow niet uit te schakelen. Daarom hoeven we staging niet uit te schakelen voor Product Item Groups, Product Groups, enzovoort.

   ![A screenshot to disable Staging](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.047.png)

   Zorg ervoor dat **alle queries zijn verwerkt**. Zodra dit klaar is, gaan we deze gegevens inladen in de Lakehouse.

### Taak 12: Data destination configureren voor overige queries

1. Selecteer de query **Product**.
1. Selecteer in de rechterbenedenhoek **+** naast **Data destination**.
1. Selecteer in het lint **Home -> Add data destination -> Lakehouse**.

   ![A screenshot configure Data Destination for Product query](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.048.png)

1. Het dialoogvenster Connect to data destination wordt geopend. Selecteer **Lakehouse (none)** in de **Connection dropdown**.
1. Selecteer **Next**.

   ![A screenshot of Connect to data destination](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.049.png)

1. Het dialoogvenster Choose destination target wordt geopend. Zorg dat de **keuzeknop New table** is geselecteerd, omdat we een nieuwe tabel aanmaken.
1. We willen de tabel aanmaken in de Lakehouse die we eerder hebben aangemaakt. Navigeer in het linkerdeelvenster naar **Lakehouse -> FAIAD_username**.
1. Selecteer **lh\_FAIAD**.
1. Laat de tabelnaam staan op **Product**.
1. Selecteer **Next**.

   ![A screenshot of Choose destination target](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.050.png)

1. Het dialoogvenster Choose destination settings wordt geopend. Deze keer gebruiken we de automatische instellingen, omdat hiermee een volledige update van de gegevens wordt uitgevoerd. Ook worden kolomnamen indien nodig hernoemd. Selecteer **Save settings**.
1. U wordt teruggeleid naar het **Power Query-venster**. In de rechterbenedenhoek is **Data destination** ingesteld op **Lakehouse**.
1. Stel op dezelfde manier de **Data Destination** in voor de volgende queries:

      1. Product Details

      2. Reseller

      3. Sales

      4. Date

1. We hebben een dataflow die gegevens inlaadt van ADLS naar de Lakehouse. Laten we deze dataflow publiceren. Selecteer Publish rechtsonder.

   ![A screenshot of Choose destination settings](../media/Fabrichey2.png)

1. We hebben een dataflow die gegevens inlaadt van ADLS naar de Lakehouse. Laten we deze dataflow publiceren. Selecteer **Publish** rechtsonder.

   ![A screenshot of dataflow to Publish](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.052.png)

   U wordt teruggeleid naar de Data Factory Home-pagina. Het kan enkele minuten duren voordat de gegevens worden vernieuwd.

   In het volgende lab gaan we gegevens inladen van de andere databronnen.

# **Referenties**
Fabric Analyst in a Day (FAIAD) maakt u bekend met een aantal van de belangrijkste functies van Microsoft Fabric. In het menu van de service vindt u in de sectie Help (?) links naar uitstekende bronnen.

   ![A screenshot of help options](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.053.png)

Hieronder vindt u nog enkele aanvullende bronnen die u helpen bij uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige aankondiging van [Microsoft Fabric GA](https://aka.ms/Fabric-Hero-Blog-Ignite23)
- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)
- Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)
- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)
- Leer nieuwe vaardigheden door de [Fabric Learning-modules](https://aka.ms/learn-fabric) te verkennen
- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)
- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om uw vragen te stellen, feedback te delen en van anderen te leren

Lees de uitgebreidere aankondigingsblogs per Fabric-ervaring:

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

© 2023 Microsoft Corporation. Alle rechten voorbehouden.

Door gebruik te maken van deze demo/dit lab, gaat u akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met als doel uw feedback te verzamelen en u een leerervaring te bieden. U mag de demo/het lab alleen gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback aan Microsoft te geven. U mag het niet voor enig ander doel gebruiken. U mag deze demo/dit lab of een deel ervan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN DEEL DAARVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE TEN BEHOEVE VAN VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARE-TECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF INRICHTING VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN GEPRESENTEERD, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET ZOALS EEN DEFINITIEVE VERSIE ZOU WERKEN. HET IS OOK MOGELIJK DAT WE GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UITBRENGEN. UW ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK ANDERS ZIJN.

**FEEDBACK**. Als u feedback geeft over de technologiefuncties, -functionaliteit en/of -concepten die in deze demo/dit lab worden beschreven aan Microsoft, verleent u Microsoft kosteloos het recht om uw feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, te delen en te commercialiseren. U verleent ook aan derden, kosteloos, de octrooirechten die nodig zijn voor hun producten, technologieën en diensten om gebruik te maken van of te koppelen aan specifieke onderdelen van een Microsoft-software of -service die de feedback bevat. U geeft geen feedback die onderworpen is aan een licentie die Microsoft verplicht zijn software of documentatie in licentie te geven aan derden omdat we uw feedback daarin opnemen. Deze rechten blijven van kracht na afloop van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, INCLUSIEF ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, ONGEACHT OF DEZE UITDRUKKELIJK, IMPLICIET OF WETTELIJK ZIJN, GESCHIKTHEID VOOR EEN BEPAALD DOEL, TITEL EN NIET-INBREUK. MICROSOFT GEEFT GEEN GARANTIES OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE UITVOER DIE VOORTVLOEIT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR ENIG DOEL.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen veranderen in toekomstige versies van het product. In deze demo/dit lab leert u over enkele, maar niet alle, nieuwe functies.
