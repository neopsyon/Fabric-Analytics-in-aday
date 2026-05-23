# Microsoft Fabric - Fabric Analyst in a Day - Lab 3

# ![](../media/new5.png)

# Inhoudsopgave
   * Inleiding	3

   * Dataflow Gen2

     * Taak 1: Dataflow Gen2 aanmaken

     * Taak 2: Verbinding maken met ADLS Gen2

     * Taak 3: Base ADLS Gen2 folder query aanmaken

     * Taak 4: Cities query aanmaken

     * Taak 5: Countries query aanmaken

     * Taak 6: States aanmaken via Copy – Optie 1

     * Taak 7: Geo query aanmaken via Copy – Optie 2

     * Taak 8: Data Destination configureren voor Geo query

     * Taak 9: Dataflow publiceren

     * Taak 10: Dataflow hernoemen

     * Taak 11: Overige queries bouwen in Dataflow

     * Taak 12: Data Destination configureren voor overige queries

   * Referenties

# <a name="_toc152196222"></a>**Inleiding**
In ons scenario komen Sales-gegevens uit het ERP-systeem en worden opgeslagen in een ADLS Gen2-database. Deze worden elke dag om 12:00 uur bijgewerkt. We moeten deze gegevens transformeren en in de Lakehouse inladen om ze in ons model te gebruiken.

Er zijn meerdere manieren om deze gegevens in te laden.

- **Shortcuts:** Dit biedt geen mogelijkheid om gegevens te transformeren.
- **Notebooks:** Dit vereist dat we code schrijven. Het is een ontwikkelaarsvriendelijke aanpak.
- **Dataflow Gen2:** U bent waarschijnlijk bekend met Power Query of Dataflow Gen1. Dataflow Gen2, zoals de naam aangeeft, is de nieuwere versie van Dataflow. Het biedt alle mogelijkheden van Power Query / Dataflow Gen1 met de toegevoegde mogelijkheid om gegevens te transformeren en in te laden in meerdere gegevensbronnen. We introduceren dit in de komende labs.
- **Data Pipeline:** Dit is een orchestratiemiddel. Activiteiten kunnen worden georchestreerd om gegevens te extraheren, transformeren en inladen. We zullen Data Pipeline gebruiken om een Dataflow Gen2-activiteit uit te voeren, die op zijn beurt de extractie, transformatie en inlading verzorgt.

We beginnen met Dataflow Gen2 om de verbinding met de gegevensbron en de benodigde transformaties te maken. Vervolgens gebruiken we Data Pipeline om de Dataflow Gen2 te orkestreren/uit te voeren.

Aan het einde van dit lab heeft u geleerd:

- Hoe u Dataflow Gen2 aanmaakt
- Hoe u via Dataflow Gen2 verbinding maakt met ADLS Gen2 en gegevens transformeert
- Hoe u gegevens in de Lakehouse inlaadt


# <a name="_toc152196223"></a>**Dataflow Gen2**
### <a name="_toc152196224"></a>Taak 1: Dataflow Gen2 aanmaken
1. Navigeer terug naar de **Fabric workspace** die u in het eerdere Lab 2, Taak 8 hebt aangemaakt.
1. Als u na het vorige lab niet bent weggenavigeerd, bevindt u zich in het Lakehouse-scherm. Als u wel bent weggenavigeerd, is dat geen probleem. Selecteer **Data Engineering** linksonder in uw scherm.
1. Selecteer **Data Factory** in het geopende Fabric experience-dialoogvenster. Data Factory bevat de workloads die nodig zijn om gegevens te extraheren, transformeren en inladen.

   ![A screenshot of a dialog to select Data Factory experience](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.002.png)

1. U wordt doorgestuurd naar de Data Factory-startpagina. Selecteer onder New de optie **Dataflow Gen2**.

   ![A screenshot of Data Factory Home selecting Dataflow Gen2](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.003.png)

U wordt doorgestuurd naar de **Dataflow-pagina**. Dit scherm ziet er vertrouwd uit, want het lijkt op Dataflow Gen1 of Power Query. U ziet dat er opties beschikbaar zijn om verbinding te maken met verschillende gegevensbronnen, evenals de mogelijkheid om gegevens te transformeren. Laten we verbinding maken met de ADLS Gen2-gegevensbron en enkele transformaties uitvoeren.
### <a name="_toc152196225"></a>Taak 2: Verbinding maken met ADLS Gen2
1. Selecteer in het lint **Home -> Get data -> More…**

   ![A screenshot of Dataflow screen to select Get Data](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.004.png)

1. U wordt doorgestuurd naar het dialoogvenster **Get data Choose data source**. U kunt de gegevensbron zoeken via het zoekvak. In het linkerdeelvenster zijn opties beschikbaar voor een Blank table of Blank query. U ziet ook een nieuwe optie om bestanden te uploaden. Deze optie verkennen we in een later lab. Klik voor nu op **View more ->** in de rechterbovenhoek van uw scherm.

   ![A screenshot of Choose data source](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.005.png)

   Nu kunt u alle beschikbare gegevensbronnen bekijken. U heeft de mogelijkheid om de gegevensbronnen te filteren op File, Database, Microsoft Fabric, Power Platform, Azure, enzovoort.

    ![A screenshot of available data sources](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.006.png)

1. Selecteer **Azure** bovenaan om te filteren op Azure-gegevensbronnen.
1. Selecteer **Azure Data Lake Storage Gen2**.

   ![A screenshot of select Azure Data Lake Storage Gen2](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.007.png)

1. U wordt doorgestuurd naar het dialoogvenster Connect to Data Source. U moet een verbinding maken met de ADLS Gen2-gegevensbron. Voer onder **Connection Settings -> URL** het volgende in:
   ```
   https://stvnextblobstorage.dfs.core.windows.net/fabrikam-sales/Delta-Parquet-Format
   ```
   ![A screenshot of Connect to data source](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.008.png)

1. Selecteer **Account Key** in het vervolgkeuzemenu Authentication kind.
1. Kopieer de Account Key van het tabblad Environment Variables (naast het tabblad Lab Guide) en plak deze in het **Account key tekstvak**.

   ![A screenshot of Connect to data source](../media/new6.png)

1. Selecteer **Next** rechtsonder in het scherm.

### <a name="_toc152196226"></a>Taak 3: Base ADLS Gen2 folder query aanmaken
1. Zodra de verbinding tot stand is gebracht, wordt u doorgestuurd naar het scherm **Preview folder data**. Er bevinden zich veel bestanden in de ADLS Gen2-map. We hebben slechts gegevens uit een aantal ervan nodig. Selecteer **Create** om een verbinding met de map te maken.

   ![A screenshot of Preview folder dialog](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.010.png)

1. U bevindt zich nu in het **Power Query**-dialoogvenster. Dit is de verbinding met de hoofdmap van ADLS Gen2. We zullen deze query in latere queries als referentie gebruiken. Laten we de query hernoemen. In het **rechterdeelvenster**, onder **Query settings -> Properties -> Name**, wijzigt u de naam naar **ADLS Base Folder**.

1. Alle queries van Dataflow Gen2 worden standaard geladen in een Staging Lakehouse. In dit lab zullen we geen gegevens stagen. Om dit laden uit te schakelen, klikt u in het **linkerdeelvenster met de rechtermuisknop op de ADLS Base Folder**-query.

   >**Opmerking:** Staging wordt gebruikt wanneer we gegevens moeten stagen voor verdere transformatie voordat ze gereed zijn voor gebruik.

1. **Schakel de optie Enable Staging uit**.

   ![A screenshot to disable Staging](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.011.png)

   U ziet dat er twee bestandsformaten in de map aanwezig zijn: **json** en **parquet**.
   
   - **Parquet:** is een open-source bestandsformaat dat is ontworpen voor platte kolomgebaseerde opslagformaten. Parquet werkt goed met complexe gegevens in grote volumes en staat bekend om zowel de performante datacompressie als het vermogen om een breed scala aan coderingstypes te verwerken.
   - **Json:** het bestand bevat metadata zoals het schema en het gegevenstype van het parquet-bestand.

1. We hebben alleen het parquet-bestand nodig, omdat dit de benodigde gegevens bevat. Selecteer de **vervolgkeuzepijl van de Extension-kolom**.

1. **Schakel .json uit** zodat er gefilterd wordt op .parquet-bestanden.
1. Selecteer **OK**.

   ![A screenshot to filter out json files](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.012.png)

Nu is de Base query ingesteld. We kunnen hier voor alle queries van de ADLS Gen2-bron naar verwijzen.

### <a name="_toc152196227"></a>Taak 4: Cities query aanmaken
Sales-gegevens zijn beschikbaar op het niveau van Geography, Product, verkoper en Date. Laten we eerst een query aanmaken om de Geo-dimensie op te halen. Geo-gegevens zijn beschikbaar in drie verschillende bestanden in de volgende submappen:

- **Cities:** Application.Cities
- **Countries:** Application.Countries
- **State:** Application.StateProvinces

We moeten City-, State- en Country-gegevens uit deze drie bestanden combineren om de Geo-dimensie te maken.

1. Laten we beginnen met City. Klik in het linkerdeelvenster **met de rechtermuisknop op ADLS Base Folder**. Selecteer **Reference** om een nieuwe query te maken die verwijst naar de ADLS Base Folder-query.

   ![A screenshot to Reference ADLS Base folder](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.013.png)

1. Selecteer de **vervolgkeuzepijl van de Folder Path-kolom**.
1. Selecteer **Text filters -> Contains...**

   ![A screenshot to filter Folder Path](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.014.png)

1. Voer in het dialoogvenster **Filter rows** de waarde **Application.Cities** in.
   
   >**Opmerking:** Dit is hoofdlettergevoelig.

1. Selecteer **OK**.

   ![A screenshot of Filter Rows dialog](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.015.png)

1. De gegevens worden gefilterd naar één rij. Selecteer **Binary** onder de kolom **Content**.

   ![Screenshot of ADLS Base Folder(2)](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.016.png)

1. U ziet alle City-details. In het **rechterdeelvenster**, onder **Query settings -> Properties -> Name**, wijzigt u de naam naar **Cities**.

    >**Opmerking:** Zorg er in de rechterbenedenhoek van de schermafbeelding voor dat de query vier stappen heeft en wacht tot de query klaar is met laden. Dit kan enkele minuten duren.
   
      ![A screenshot to Rename query](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.017.png)

In het rechterdeelvenster, onder **Applied steps**, ziet u dat alle stappen zijn geregistreerd. Dit gedrag is vergelijkbaar met Power Query. Laten we nu een soortgelijk proces volgen om een **Country**-query te maken.

### <a name="_toc152196228"></a>Taak 5: Countries query aanmaken

1. Klik in het linkerdeelvenster **met de rechtermuisknop op ADLS Base Folder**. Selecteer **Reference** om een nieuwe query te maken die verwijst naar de ADLS Base Folder-query.

   ![A screenshot to reference ADLS Base Folder](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.018.png)

1. Selecteer de **vervolgkeuzepijl van de Folder Path-kolom**.

1. Selecteer **Text filters -> Contains...**

   ![A screenshot to filter by Folder Path](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.019.png)

1. Voer in het **dialoogvenster Filter rows** de waarde **Application.Countries** in.

   >**Opmerking:** Dit is hoofdlettergevoelig.

1. Selecteer **OK**.

   ![A screenshot of Filter rows dialog](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.020.png)

1. De gegevens worden gefilterd naar één rij. Selecteer **Binary** onder de kolom **Content**.

   ![Screenshot of ADLS Base Folder(2)](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.021.png)

1. U ziet alle Country-details. In het **rechterdeelvenster**, onder **Query settings -> Properties -> Name**, wijzigt u de naam naar **Countries**.

    >**Opmerking:** Zorg er in de rechterbenedenhoek van de schermafbeelding voor dat de query vier applied steps heeft en wacht tot de query klaar is met laden. Dit kan enkele minuten duren.

    ![A screenshot to Rename query](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.022.png)

We moeten vervolgens State inladen, maar de stappen beginnen zich te herhalen. We hebben de queries al in het Power BI Desktop-bestand. Laten we kijken of we de queries daarvandaan kunnen kopiëren.

### <a name="_toc152196229"></a>Taak 6: States aanmaken via Copy – Optie 1

1. Als u het nog niet heeft geopend, open dan **FAIAD.pbix** in de map **Report** op het **bureaublad** van uw labomgeving.
   
1. Selecteer in het lint **Home -> Transform data**. Het Power Query-venster wordt geopend. Zoals u in het eerdere lab heeft gezien, zijn de queries in het linkerdeelvenster georganiseerd per gegevensbron.

   ![A screenshot of Power BI Desktop report.](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.023.png)

1. Klik in het linkerdeelvenster, onder de map ADLSData, met de rechtermuisknop op de query **States** en selecteer **Copy**.

   ![A screenshot Power Query window](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.024.png)

1. Navigeer terug naar de **browser**. U zou zich in de Dataflow moeten bevinden waaraan we bezig waren.
1. Selecteer in het linkerdeelvenster het **Queries**-paneel en voer **Ctrl+V** in (momenteel wordt rechtsklikken om te plakken niet ondersteund).

   ![A screenshot Dataflow queries](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.025.png) 

   U ziet dat **ADLS Base Folder (2)** ook is gekopieerd. Dit is omdat States in Power BI Desktop verwijst naar de ADLS Base Folder, maar we hebben de ADLS Base Folder al. Laten we dit oplossen.

1. Selecteer de query **States**.
1. Selecteer in het **rechterdeelvenster**, onder **Applied** **steps**, de stap **Source**.
1. Wijzig in de formulebalk #"ADLS Base Folder (2)" naar **#"ADLS Base Folder"**.

   ![A screenshot of States query Source step](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.026.png) 

1. Klik op het **vinkje** naast de formulebalk of druk op **Enter**.

   ![A screenshot of States query Source step after updating formula bar](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.027.png)

1. Nu kunnen we ADLS Base Folder (2) verwijderen. Klik in het linkerdeelvenster, onder de sectie **Queries**, **met de rechtermuisknop** op de query **ADLS Base Folder (2)** en selecteer **Delete**.

   ![A screenshot of delete ADLS Base Folder (2) delete](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.028.png)

1. Het dialoogvenster Delete query verschijnt. Selecteer **Delete** ter bevestiging.

   >**Opmerking:** Zorg ervoor dat de query vier applied steps heeft en wacht tot de query klaar is met laden. Dit kan enkele minuten duren.

### <a name="_toc152196230"></a>Taak 7: Geo query aanmaken via Copy – Optie 2

Nu moeten we deze queries samenvoegen om de Geo-dimensie te maken. Laten we de query opnieuw kopiëren uit het Power BI Desktop-bestand. Ditmaal kopiëren we de code uit de Advanced Editor.

1. Navigeer terug naar het **Power Query-venster** van het Power BI Desktop-bestand.
1. Selecteer in het linkerdeelvenster, onder **Queries**, de query **Geo** in de map ADLSData.
1. Selecteer in het lint **Home -> Advanced Editor**.

   ![A screenshot of Power Query window from Power BI Desktop](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.029.png)

1. Het venster Advanced Editor wordt geopend. **Selecteer alle tekst** in de Advanced Editor.
1. Klik **met de rechtermuisknop** en selecteer **Copy**.

   ![A screen shot of Advanced Editor](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.030.png)

1. Selecteer de **X** in de rechterbovenhoek van het venster of selecteer **Done** om de Advanced Editor te sluiten.
1. Navigeer terug naar het **Dataflow**-venster in de browser.
1. Selecteer in het lint **Get Data -> Blank query**.

   ![A screenshot of Get Data -> Blank Query in Dataflow](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.031.png)

1. Het dialoogvenster Get data, Connect to the data source Advanced Editor wordt geopend. **Selecteer alle tekst** in de editor.
1. Druk op **Delete** op uw toetsenbord om alle tekst te verwijderen.
1. De Advanced Editor moet nu leeg zijn. Voer nu **Ctrl+V** in om de inhoud te plakken die u hebt gekopieerd uit de Advanced Editor van Power BI Desktop.
1. Selecteer **Next**.

   ![A screenshot of Advanced Editor](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.032.png)

1. Nu beschikken we over de Geo-dimensie. Laten we de query hernoemen. In het **rechterdeelvenster**, onder **Query settings -> Properties -> Name**, wijzigt u de naam naar **Geo**.

   >**Opmerking:** Wacht tot de query klaar is met laden. Dit kan enkele minuten duren.

Laten we de stappen doorlopen om te begrijpen hoe Geo is aangemaakt. Selecteer in het rechterdeelvenster, onder Applied Steps, de stap **Source**. Als u naar de formulebalk kijkt of op Settings klikt, ziet u dat de Source van deze query een join is tussen Cities en States. Als u de stappen doorloopt, ziet u dat het resultaat van de eerste join op zijn beurt wordt samengevoegd met Countries. Alle drie de queries worden dus gebruikt om een Geo-dimensie te maken.

   ![A screenshot of Formula bar for Geo query](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.033.png)

### <a name="_toc152196231"></a>Taak 8: Data Destination configureren voor Geo query

Nu we een dimensie hebben, laten we deze gegevens in de Lakehouse inladen. Dit is de nieuwe functie die beschikbaar is in Dataflow Gen2.

1. Zoals eerder vermeld, stagen we geen van deze gegevens. Klik daarom **met de rechtermuisknop** op de query **Cities** en selecteer **Enable staging** om het vinkje te verwijderen.

   ![A screenshot to disable Staging](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.034.png)

1. Volg dezelfde stappen voor de queries **Countries en Geo** **om het vinkje naast Enable staging te verwijderen**.
1. Selecteer de query **Geo**.
1. Selecteer rechtsonder **+** naast **Data destination**.
1. Selecteer **Lakehouse** in het dialoogvenster.

   ![A screenshot select Data Destination](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.035.png)

1. Het dialoogvenster Connect to data destination wordt geopend. We moeten een nieuwe verbinding met de Lakehouse maken. Zorg dat **Create new connection** is geselecteerd in de **Connection dropdown** en dat **Authentication kind** is ingesteld op **Organizational account**, en selecteer vervolgens **Next**.

   ![A screenshot of Connect to data destination](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.036.png)

1. Zodra de verbinding is aangemaakt, wordt het dialoogvenster choose destination target geopend. Zorg dat de **radioknop New table** is geselecteerd, omdat we een nieuwe tabel aanmaken.
1. We willen de tabel aanmaken in de eerder aangemaakte Lakehouse. Navigeer in het linkerdeelvenster naar **Lakehouse -> FAIAD_username**.
1. Selecteer **lh\_FAIAD**.
1. Laat de tabelnaam **Geo** staan.
1. Selecteer **Next**.

   ![A screenshot to Choose destination target](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.037.png)

1. Het dialoogvenster Choose destination settings wordt geopend. Elke keer dat Dataflow Gen2 wordt vernieuwd, willen we een volledige laadactie uitvoeren. Zorg dat **Update method** is ingesteld op **Replace**.
1. U ziet een waarschuwing: "Some column names contain unsupported characters. Should we fix them for you?" De Lakehouse ondersteunt geen kolomnamen met spaties. Selecteer **Fix it** om de waarschuwing te verwijderen.

   >**Opmerking:** U heeft ook de optie om gegevens te Append. Als u dit selecteert, worden bij elke vernieuwing van de dataflow nieuwe gegevens toegevoegd aan de bestaande gegevens.

1. Column mapping kan worden gebruikt om dataflow-kolommen aan bestaande kolommen te koppelen. In ons geval is het een New Table. We kunnen daarom de standaardinstellingen gebruiken. Selecteer **Save settings**.

   ![A screenshot to Choose destination settings](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.038.png)

   >**Opmerking:** Als u bepaalde kolommen niet in de Lakehouse wilt opnemen, gebruik dan het selectievakje rechts van de Source-kolom om de gewenste kolommen uit te vinken.

### <a name="_toc152196232"></a>Taak 9: Dataflow publiceren

1. U wordt teruggestuurd naar het **Power Query-venster**. In de rechterbenedenhoek ziet u dat **Data destination is ingesteld op Lakehouse**.

1. Laten we deze queries publiceren zodat we de Lakehouse kunnen bekijken. We komen later terug om meer queries toe te voegen. Selecteer rechtsonder **Publish**.

   ![A screenshot to Publish Dataflow](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.039.png)

1. U wordt teruggestuurd naar het **Data Factory-scherm**. Het kan even duren voordat de Dataflow is gepubliceerd. Selecteer daarna **lh\_FAIAD Lakehouse**.

   ![A screenshot to select Lakehouse](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.040.png)

1. U wordt doorgestuurd naar het scherm **Lakehouse Explorer**. Vouw in het linkerdeelvenster **lh\_FAIAD -> Tables** uit.

1. U ziet dat er nu een Geo-tabel in de Lakehouse aanwezig is. Vouw **Geo** uit en bekijk alle kolommen.

1. Selecteer de tabel **Geo** en de gegevenspreview wordt geopend in het rechterdeelvenster.

   ![A screenshot to explore Lakehouse tables](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.041.png)

Er is ook een SQL Endpoint beschikbaar waarmee u deze tabel kunt bevragen. We bekijken deze optie in een later lab. Nu we weten dat de Geo-gegevens in de Lakehouse zijn beland, laden we de overige gegevens van ADLS Gen2 in.

### <a name="_toc152196233"></a>Taak 10: Dataflow hernoemen

1. Selecteer in de linkermenubalk **FAIAD_username** om terug te navigeren naar de **workspace**.
1. We werken met Dataflow 1. Laten we dit hernoemen voordat we verdergaan. Klik op het **weglatingsteken (…)** naast Dataflow 1. Selecteer **Properties**.

   ![A screenshot to select Dataflow1 Properties](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.042.png)

1. Het dialoogvenster Dataflow properties wordt geopend. Wijzig de naam naar **df_Sales_ADLS**.

   >**Opmerking:** We voegen het voorvoegsel **df** toe aan de naam van de Dataflow. Dit maakt het eenvoudiger om te zoeken en te sorteren.
   
1. Voeg in het tekstvak **Description** het volgende toe: **Dataflow to ingest Sales Data from ADLS to Lakehouse**.
1. Selecteer **Save**.

   ![A screenshot Dataflow Properties dialog](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.043.png)

### <a name="_toc152196234"></a>Taak 11: Overige queries bouwen in Dataflow

1. U wordt teruggestuurd naar het Data Factory-scherm. Selecteer Dataflow **df\_Sales\_ADLS** om terug te navigeren naar de dataflow.

   ![A screenshot to select df_Sales_ADLS](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.044.png)

   Om het eenvoudiger te maken, kijken we of we de queries uit Power BI Desktop kunnen kopiëren.

1. Als u het nog niet heeft geopend, open dan **FAIAD.pbix** in de map **Report** op het **bureaublad** van uw labomgeving.
1. Selecteer in het lint **Home -> Transform**. Het Power Query-venster wordt geopend.
1. Selecteer in het **Queries**-paneel aan de linkerkant via **Ctrl+klik** de volgende queries uit **ADLSData**.
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

1. Klik **met de rechtermuisknop** en selecteer **Copy**.

   ![A screenshot to copy queries from Power Query window](../media/new7.png)
   
1. Navigeer terug naar het Dataflow-venster **df\_Sales\_ADF** in de browser.

1. Selecteer in het linkerdeelvenster het **Queries**-paneel en voer **Ctrl+V** in (momenteel wordt rechtsklikken om te plakken niet ondersteund).

   ![A screenshot copying queries to dataflow](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.046.png)

1. Zoals eerder vermeld, stagen we geen van deze gegevens. Klik daarom **met de rechtermuisknop** op de volgende queries en selecteer **Enable staging** om het vinkje te verwijderen.
   1. Product
   1. Product Details
   1. Reseller
   1. Date
   1. Sales

   >**Opmerking:** Als het laden is uitgeschakeld in Power BI Desktop, hoeven we staging niet uit te schakelen in Dataflow. We hoeven staging dus niet uit te schakelen voor Product Item Groups, Product Groups, enzovoort.

   ![A screenshot to disable Staging](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.047.png)

   Zorg ervoor dat **alle queries zijn verwerkt**. Daarna laden we deze gegevens in de Lakehouse in.

### <a name="_toc152196235"></a>Taak 12: Data Destination configureren voor overige queries

1. Selecteer de query **Product**.
1. Selecteer rechtsonder **+** naast **Data destination**.
1. Selecteer **Lakehouse** in het dialoogvenster.

   ![A screenshot configure Data Destination for Product query](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.048.png)

1. Het dialoogvenster Connect to data destination wordt geopend. Selecteer in de **Connection dropdown** de optie **Lakehouse (none)**.
1. Selecteer **Next**.

   ![A screenshot of Connect to data destination](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.049.png)

1. Het dialoogvenster Choose destination target wordt geopend. Zorg dat de **radioknop New table** is geselecteerd, omdat we een nieuwe tabel aanmaken.
1. We willen de tabel aanmaken in de eerder aangemaakte Lakehouse. Navigeer in het linkerdeelvenster naar **Lakehouse -> FAIAD_username**.
1. Selecteer **lh\_FAIAD**.
1. Laat de tabelnaam **Product** staan.
1. Selecteer **Next**.

   ![A screenshot of Choose destination target](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.050.png)

1. Het dialoogvenster Choose destination settings wordt geopend. Elke keer dat Dataflow Gen2 wordt vernieuwd, willen we een volledige laadactie uitvoeren. Zorg dat **Update method** is ingesteld op **Replace**.
1. U ziet een waarschuwing: "Some column names contain unsupported characters. Should we fix them for you?" De Lakehouse ondersteunt geen kolomnamen met spaties. Selecteer **Fix it** om de waarschuwing te verwijderen.
1. Column mapping kan worden gebruikt om dataflow-kolommen aan bestaande kolommen te koppelen. In ons geval is het een New Table. We kunnen daarom de standaardinstellingen gebruiken. Selecteer **Save settings**.

   ![A screenshot of Choose destination settings](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.051.png)

1. U wordt teruggestuurd naar het **Power Query-venster**. In de rechterbenedenhoek ziet u dat **data destination** is ingesteld op **Lakehouse**.

1. Stel op dezelfde manier de **Data Destination** in voor de volgende queries:
   
   a. Product Details
   
   b. Reseller

   c. Date

   d. Sales

1. We beschikken nu over een dataflow die gegevens van ADLS in de Lakehouse inlaadt. Laten we deze dataflow publiceren. Selecteer **Publish** rechtsonder.

   ![A screenshot of dataflow to Publish](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.052.png)

   U wordt teruggestuurd naar de Data Factory-startpagina. Het kan enkele minuten duren voordat de gegevens zijn vernieuwd.

   In het volgende lab laden we gegevens in vanuit de andere gegevensbronnen.

# <a name="_toc150777627"></a><a name="_toc152196236"></a>**Referenties**
Fabric Analyst in a Day (FAIAD) introduceert u in enkele van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service bevat de sectie Help (?) koppelingen naar uitstekende bronnen.

   ![A screenshot of help options](../media/Aspose.Words.cb0f9c33-ba43-4fa0-836b-a8ad8cd51945.053.png)

Hier zijn nog enkele bronnen die u helpen met uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [Microsoft Fabric GA announcement](https://aka.ms/Fabric-Hero-Blog-Ignite23)
- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)
- Meld u aan voor de [Microsoft Fabric free trial](https://aka.ms/try-fabric)
- Bezoek de [Microsoft Fabric website](https://aka.ms/microsoft-fabric)
- Leer nieuwe vaardigheden door de [Fabric Learning modules](https://aka.ms/learn-fabric) te verkennen
- Verken de [Fabric technical documentation](https://aka.ms/fabric-docs)
- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
- Word lid van de [Fabric community](https://aka.ms/fabric-community) om vragen te stellen, feedback te delen en van anderen te leren

Lees de meer uitgebreide aankondigingsblogs over Fabric-ervaringen:

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

© 2023 Microsoft Corporation. All rights reserved.

Door gebruik te maken van deze demo/dit lab, gaat u akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met het oog op het verkrijgen van uw feedback en het bieden van een leerervaring. U mag de demo/het lab uitsluitend gebruiken om dergelijke technologiekenmerken en -functionaliteit te evalueren en feedback aan Microsoft te geven. U mag het niet voor enig ander doel gebruiken. U mag deze demo/dit lab of een deel daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, afgeleide werken van maken, overdragen of verkopen.

COPYING OR REPRODUCTION OF THE DEMO/LAB (OR ANY PORTION OF IT) TO ANY OTHER SERVER OR LOCATION FOR FURTHER REPRODUCTION OR REDISTRIBUTION IS EXPRESSLY PROHIBITED.

THIS DEMO/LAB PROVIDES CERTAIN SOFTWARE TECHNOLOGY/PRODUCT FEATURES AND FUNCTIONALITY, INCLUDING POTENTIAL NEW FEATURES AND CONCEPTS, IN A SIMULATED ENVIRONMENT WITHOUT COMPLEX SET-UP OR INSTALLATION FOR THE PURPOSE DESCRIBED ABOVE. THE TECHNOLOGY/CONCEPTS REPRESENTED IN THIS DEMO/LAB MAY NOT REPRESENT FULL FEATURE FUNCTIONALITY AND MAY NOT WORK THE WAY A FINAL VERSION MAY WORK. WE ALSO MAY NOT RELEASE A FINAL VERSION OF SUCH FEATURES OR CONCEPTS. YOUR EXPERIENCE WITH USING SUCH FEATURES AND FUNCTIONALITY IN A PHYSICAL ENVIRONMENT MAY ALSO BE DIFFERENT.

**FEEDBACK**. If you give feedback about the technology features, functionality and/or concepts described in this demo/lab to Microsoft, you give to Microsoft, without charge, the right to use, share and commercialize your feedback in any way and for any purpose. You also give to third parties, without charge, any patent rights needed for their products, technologies and services to use or interface with any specific parts of a Microsoft software or service that includes the feedback. You will not give feedback that is subject to a license that requires Microsoft to license its software or documentation to third parties because we include your feedback in them. These rights survive this agreement.

MICROSOFT CORPORATION HEREBY DISCLAIMS ALL WARRANTIES AND CONDITIONS WITH REGARD TO THE DEMO/LAB, INCLUDING ALL WARRANTIES AND CONDITIONS OF MERCHANTABILITY, WHETHER EXPRESS, IMPLIED OR STATUTORY, FITNESS FOR A PARTICULAR PURPOSE, TITLE AND NON-INFRINGEMENT. MICROSOFT DOES NOT MAKE ANY ASSURANCES OR REPRESENTATIONS WITH REGARD TO THE ACCURACY OF THE RESULTS, OUTPUT THAT DERIVES FROM USE OF DEMO/ LAB, OR SUITABILITY OF THE INFORMATION CONTAINED IN THE DEMO/LAB FOR ANY PURPOSE.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen in toekomstige versies van het product worden gewijzigd. In deze demo/dit lab leert u over enkele, maar niet alle, nieuwe functies.
