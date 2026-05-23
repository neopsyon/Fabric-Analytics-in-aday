# Microsoft Fabric - Fabric Analyst in a Day - Lab 5

# ![](../media/new9.png)

# Inhoudsopgave
* Inleiding

* Dataflow Gen2

  * Taak 1: Geplande vernieuwing configureren voor Sales Dataflow
  
  * Taak 2: Geplande vernieuwing configureren voor Supplier en Customer Dataflow

* Data Pipeline

  * Taak 3: Data Pipeline aanmaken
  
  * Taak 4: Eenvoudigere Data Pipeline bouwen
        
  * Taak 5: Nieuwe Data Pipeline aanmaken
        
  * Taak 6: Until Activity aanmaken
        
  * Taak 7: Variables aanmaken
        
  * Taak 8: Until Activity configureren
        
  * Taak 9: Dataflow Activity configureren
        
  * Taak 10: 1<sup>e</sup> Set variable Activity configureren
        
  * Taak 11: 2<sup>e</sup> Set variable Activity configureren
        
  * Taak 12: 3<sup>e</sup> Set variable Activity configureren
        
  * Taak 13: Wait Activity configureren
        
  * Taak 14: Geplande vernieuwing configureren voor Data Pipeline
      
* Referenties


# <a name="_toc152204369"></a>**Inleiding** 

We hebben data uit verschillende databronnen in de Lakehouse opgenomen. In het vorige lab maakten we kennis met Lakehouse en werd er een datamodel aangemaakt. In dit lab stellen we een vernieuwingsschema in voor de databronnen. Ter herinnering de vereisten:

- **Sales Data:** in ADLS wordt elke dag om 12:00 uur 's middags bijgewerkt.
- **Supplier Data:** in Snowflake wordt elke dag om middernacht / 00:00 uur bijgewerkt.
- **Customer Data:** in Dataverse is altijd actueel. We moeten dit vier keer per dag vernieuwen: om middernacht / 00:00 uur, 6:00 uur, 12:00 uur 's middags en 18:00 uur.
- **Employee Data:** in SharePoint wordt elke dag om 9:00 uur bijgewerkt. We hebben echter geconstateerd dat er soms een vertraging is van 15 tot 30 minuten. We moeten een vernieuwingsschema opstellen dat hiermee rekening houdt.

Aan het einde van dit lab hebt u geleerd: 

- Hoe u een geplande vernieuwing van Dataflow Gen2 configureert
- Hoe u een Data Pipeline aanmaakt
- Hoe u een geplande vernieuwing van een Data Pipeline configureert

# <a name="_toc152204370"></a>**Dataflow Gen2**

### <a name="_toc152204371"></a>Taak 1: Geplande vernieuwing configureren voor Sales Dataflow

Laten we beginnen met het configureren van een geplande vernieuwing van de Sales Dataflow.

1. Ga terug naar de Fabric workspace **FAIAD_gebruikersnaam** die u in Lab 2, Taak 8 hebt aangemaakt.

2. Alle artefacten die u hebt aangemaakt, worden hier weergegeven. Typ rechts op het scherm in het **zoekvak** **df**. Hiermee worden de artefacten gefilterd op Dataflows.

      ![A screenshot of Fabric workspace](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.002.png)

3. Beweeg de cursor over de rij **df_Sales_ADLS**. U ziet de bekende pictogrammen voor **Refresh** en **Schedule Refresh**. Selecteer **ellipsis (…)**.
4. U ziet opties om de Dataflow te verwijderen, te bewerken en te exporteren. Via Properties kunt u de naam en beschrijving van de Dataflow bijwerken. We bekijken Refresh history zo dadelijk. Selecteer **Settings**.

      ![A screenshot of df_Sales_ADLS Settings](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.003.png)

     >**Opmerking:** De pagina Settings wordt geopend. In het linkerdeelvenster vindt u alle Dataflows weergegeven. 

5. Selecteer in het middelste deelvenster de koppeling **Refresh history**.

      ![A screenshot of Settings for df_Sales_ADLS](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.004.png)

6. Het dialoogvenster Refresh history wordt geopend. Er staat minimaal één vernieuwing vermeld. Dit is de vernieuwing die plaatsvond toen de dataflow werd gepubliceerd. Selecteer de koppeling **Start time**.

   >**Opmerking:** De Start time zal voor u anders zijn.

     ![A screenshot of Refresh history](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.005.png)

      Het scherm Details wordt geopend. Dit biedt details van de vernieuwing: het toont de start- en eindtijd en de duur. Ook de tabellen/activiteiten die zijn vernieuwd, worden weergegeven. Als er een fout is opgetreden, kunt u op de naam van de tabel/activiteit klikken om verder te onderzoeken.
      
      ![A screenshot of Refresh Details](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.006.png)

7. Ga terug door op de **X** rechtsboven te klikken. U wordt teruggeleid naar de **pagina met dataflow-instellingen**.
8. Vouw onder Gateway connection de sectie **Data source credentials** uit. Er wordt een lijst weergegeven met verbindingen die in de dataflow worden gebruikt. In dit geval Lakehouse en ADLS. 
   1. **Lakehouse:** Dit is de verbinding voor het opnemen van data vanuit de Dataflow.
   1. **ADLS:** Dit is de verbinding met de ADLS-brondata.

      ![A screenshot of Gateway Connections for df_Sales_ADLS](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.007.png)

9. Vouw **Refresh** uit.
10. Zet de schuifregelaar **Configure a refresh** **schedule** op **On**.
11. Stel de dropdown **Refresh frequency** in op **Daily**. U ziet dat er ook een optie is om dit op Weekly in te stellen.
12. Stel **Time Zone** in op uw gewenste tijdzone.

    **Opmerking:** Omdat dit een labomgeving is, kunt u de tijdzone naar wens instellen. In een echte situatie stelt u de tijdzone in op basis van uw eigen locatie of die van de databron.

13. Klik op de koppeling **Add another time**. U ziet dat de optie Time wordt weergegeven.
14. Stel **Time** in op **noon**. U ziet dat u de vernieuwing kunt instellen op het hele of halve uur.
15. Selecteer **Apply** om deze instelling op te slaan.

    **Opmerking:** Door op de koppeling Add another time te klikken, kunt u meerdere vernieuwingstijden toevoegen. 

    U kunt ook foutmeldingen sturen naar de eigenaar van de dataflow en andere contactpersonen.

      ![A screenshot of Refresh schedule for df_Sales_ADLS](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.008.png)

### <a name="_toc152204372"></a>Taak 2: Geplande vernieuwing configureren voor Supplier en Customer Dataflow

1. Selecteer in het linkerdeelvenster **df_Supplier_Snowflake**.
1. Configureer het vernieuwingsschema om **elke dag om middernacht / 00:00 uur** te vernieuwen. 
1. Selecteer **Apply** om deze instelling op te slaan.

      ![A screenshot of Refresh schedule for df_Sales_ADLS](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.009.png)

1. Selecteer in het linkerdeelvenster **df_Customer_Dataverse**.
1. Configureer het vernieuwingsschema voor vier keer per dag: **middernacht / 00:00 uur, 6:00 uur, 12:00 uur 's middags en 18:00 uur**.
1. Selecteer **Apply** om deze instelling op te slaan.

      ![A screenshot of Refresh schedule for df_Customer_Dataverse](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.010.png)

      Zoals eerder vermeld, moeten we aangepaste logica bouwen voor het geval het Employee-bestand in SharePoint niet op tijd wordt aangeleverd. Laten we Data Pipeline gebruiken om dit op te lossen.

# <a name="_toc152204373"></a>**Data Pipeline**

### <a name="_toc152204374"></a>Taak 3: Data Pipeline aanmaken

1. Selecteer linksonder in uw browservenster **Power BI**.
2. Het dialoogvenster Microsoft Fabric wordt geopend. Selecteer **Data Factory**. U wordt naar de startpagina van Data Factory geleid.

     ![A screenshot Fabric experiences dialog](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.011.png)

3. Selecteer in het bovenste menu **Data pipeline** om een nieuwe pipeline aan te maken.
4. Het dialoogvenster New pipeline wordt geopend. Geef de pipeline de **naam** **pl_Refresh_People_SharePoint**.
5. Selecteer **Create**.

     ![Screenshot of Data Factory Home to create new Data Pipeline](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.012.png)

   U wordt naar de **Data Pipeline-pagina** geleid. Als u eerder met Azure Data Factory hebt gewerkt, zal dit scherm bekend zijn. Laten we een kort overzicht geven van de indeling.
   
   U bevindt zich op het **Home**-scherm. Als u naar het bovenste menu kijkt, vindt u opties om veelgebruikte activiteiten toe te voegen, een pipeline te valideren en uit te voeren, en de uitvoeringsgeschiedenis te bekijken. In het middelste deelvenster vindt u ook snelle opties om te beginnen met het bouwen van de pipeline.
   
      ![A screenshot of Data Pipeline landing page](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.013.png)
 
6. Selecteer in het bovenste menu **Activities**. In het menu ziet u nu een lijst met veelgebruikte Activities. 
7. Selecteer **ellipsis (…)** rechts van het menu om alle andere beschikbare Activities te bekijken. We gaan in dit lab enkele van deze Activities gebruiken.

      ![A screenshot of Data Pipeline with available activities](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.014.png)

8. Klik in het bovenste menu op **Run**. U ziet opties om de pipeline-uitvoering te starten en in te plannen. U vindt ook de optie om de uitvoeringsgeschiedenis te bekijken via View Run History.
9. Selecteer in het bovenste menu **View**. Hier vindt u opties om de code in JSON-indeling te bekijken. U vindt ook opties om de activities op te maken.

     **Opmerking:** Als u een JSON-achtergrond hebt, selecteer dan aan het einde van het lab gerust View JSON code. U zult merken dat alle orkestratie die u via de ontwerpweergave uitvoert, ook in JSON kan worden geschreven. 
   
      ![A screenshot of View ribbon in Data Pipeline](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.015.png)
  
### <a name="_toc152204375"></a>Taak 4: Eenvoudigere Data Pipeline bouwen

Laten we beginnen met het bouwen van de pipeline. We hebben een activity nodig om de Dataflow te vernieuwen. Laten we een geschikte activity zoeken.

1. Selecteer in het bovenste menu **Activities -> Dataflow**. De Dataflow activity wordt toegevoegd aan het middelste ontwerpdeelvenster. Het onderste deelvenster toont nu configuratieopties voor de Dataflow activity.
2. We gaan de activity configureren om verbinding te maken met df_People_SharePoint. Selecteer in het **onderste** **deelvenster** **Settings**.
3. Zorg dat **Workspace** is ingesteld op **uw workspacenaam**.
4. Selecteer in de **Dataflow dropdown** **df_People_SharePoint**. Wanneer deze Dataflow activity wordt uitgevoerd, vernieuwt zij **df_People_SharePoint.** Dat was eenvoudig, toch? 😊

      **Opmerking:** De optie Notification is momenteel grijs weergegeven. Deze functie wordt binnenkort ingeschakeld. U kunt dan meldingen configureren bij het slagen of mislukken van deze activity. 

   In ons scenario wordt Employee Data niet op schema bijgewerkt. Soms is er een vertraging. Laten we kijken of we hier rekening mee kunnen houden.
   
      ![A screenshot of Dataflow activity settings configuration in Data Pipeline](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.016.png)

5. Selecteer in het **onderste** **deelvenster** **General**. Laten we de activity een naam en beschrijving geven.
6. Voer in het veld **Name** **dfactivity_People_SharePoint** in.
7. Voer in het veld **Description** **Data flow activity to refresh df_People_Sharepoint dataflow** in.
8. U ziet dat er een optie is om een activity te deactiveren. Deze functie is handig tijdens het testen of debuggen. Laat dit op **Activated** staan.
9. Er is een optie om **Timeout** in te stellen. Laat de **standaardwaarde** staan; deze biedt de dataflow voldoende tijd om te vernieuwen.

     **Opmerking:** Als de data niet op schema beschikbaar is, stellen we de activity in om elke 10 minuten opnieuw uit te voeren, maximaal drie keer. Als ook de derde poging mislukt, wordt er een fout gerapporteerd.

10. Stel **Retry** in op **3**. 
11. Vouw de sectie **Advanced** uit.
12. Stel **Retry interval (sec)** in op **600**. 
13. Selecteer in het menu **Home -> Save**-pictogram om de pipeline op te slaan.

      ![A screenshot of Dataflow activity General configuration in Data Pipeline](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.017.png)
   
     Let op het voordeel van het gebruik van de data pipeline ten opzichte van het instellen van de data flow op geplande vernieuwing (zoals we bij de eerdere data flows hebben gedaan):
   
   - Pipeline biedt de mogelijkheid meerdere keren opnieuw te proberen voordat de vernieuwing als mislukt wordt gemarkeerd.
   - Pipeline biedt de mogelijkheid om binnen seconden te vernieuwen, terwijl geplande vernieuwing via data flow elke 30 minuten plaatsvindt.

### <a name="_toc152204376"></a>Taak 5: Nieuwe Data Pipeline aanmaken

Laten we ons scenario iets complexer maken. We hebben geconstateerd dat als de data om 9:00 uur niet beschikbaar is, deze doorgaans binnen vijf minuten beschikbaar is. Als dit venster wordt gemist, duurt het 15 minuten voordat het bestand beschikbaar is. We willen de herhaalpogingen inplannen op vijf en 15 minuten. Laten we kijken hoe dit gerealiseerd kan worden door een nieuwe Data Pipeline aan te maken.

1. Klik in het linkerdeelvenster op **uw workspacenaam**; u wordt dan naar de startpagina van Data Factory geleid.
1. Klik in het bovenste menu op **New** en klik vervolgens in het dropdown op **Data pipeline**.
1. Het dialoogvenster New pipeline wordt geopend. Geef de pipeline de **naam** **pl_Refresh_People_SharePoint_Option2**.
1. Selecteer **Create**.

      ![A screenshot of create new data pipeline](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.018.png)

### <a name="_toc152204377"></a>Taak 6: Until Activity aanmaken

1. U wordt naar het Data Pipeline-scherm geleid. Selecteer in het menu **Activities**.
1. Klik op **ellipsis(…)** rechts.
1. Klik in de lijst met activities op **Until**. 

   **Until**: is een activity die wordt gebruikt om te herhalen totdat aan een voorwaarde is voldaan. 

    In ons scenario gaan we herhalen en de dataflow vernieuwen totdat dit succesvol is, of totdat we het drie keer hebben geprobeerd.

      ![A screenshot of adding Until activity in Data Pipeline](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.019.png)

### <a name="_toc152204378"></a>Taak 7: Variables aanmaken

1. We moeten variables aanmaken die worden gebruikt voor het herhalen en het instellen van de status. Selecteer een **leeg gebied** in het ontwerpdeelvenster van de pipeline.
1. Het menu in het onderste deelvenster wijzigt. Selecteer **Variables**.
1. Selecteer **New** om een nieuwe variable toe te voegen.
1. Er verschijnt een rij. Voer **varCounter** in als **Name**. We gebruiken deze variable om drie keer te herhalen.
1. Selecteer in de dropdown **Type** de waarde **Integer**.
1. Voer **0** in als **Default value**.

   **Opmerking:** We voegen de prefix var toe aan variablenamen, zodat ze gemakkelijk te vinden zijn. Dit is een goede praktijk.

      ![A screenshot of variables in Data Pipeline](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.020.png)

1. Selecteer **New** om nog een nieuwe variable toe te voegen.
1. Er verschijnt een rij. Voer als **Name** **varTempCounter** in. We gebruiken deze variable om de variable varCounter te verhogen.
1. Selecteer in de dropdown **Type** de waarde **Integer**.
1. Voer **0** in als **Default value**.
1. Volg vergelijkbare stappen om nog drie variables toe te voegen.
   1. **varIsSuccess** van het type **String** met standaardwaarde **No**. Deze variable wordt gebruikt om aan te geven of de dataflow-vernieuwing succesvol was.
   1. **varSuccess** van het type **String** met standaardwaarde **Yes**. Deze variable wordt gebruikt om de waarde van varIsSuccess in te stellen als de dataflow-vernieuwing succesvol is.
   1. **varWaitTime** van het type **Integer** met standaardwaarde **60**. Deze variable wordt gebruikt om de wachttijd in te stellen als de dataflow mislukt. (Ofwel 5 minuten/300 seconden of 15 minuten/900 seconden)

### <a name="_toc152204379"></a>Taak 8: Until Activity configureren

1. Selecteer **Until activity**. 
1. Selecteer in het **onderste deelvenster** **General**.
1. Voer als **Name** **Iterator** in.
1. Voer als **Description** **Iterator to refresh dataflow. It will retry up to 3 times** in. 

     ![A screenshot of General configuration of Until activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.021.png)

1. Selecteer in het onderste deelvenster **Settings**.
1. Selecteer het **tekstvak Expression**. We moeten een expressie invoeren in dit tekstvak die evalueert naar true of false. De Until activity herhaalt zolang deze expressie evalueert naar false. Zodra de expressie evalueert naar true, stopt de activity met herhalen.
1. Selecteer de koppeling **Add dynamic content** die onder het tekstvak verschijnt.

     ![A screenshot of Settings configuration of Until activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.022.png)

     We moeten een expressie schrijven die wordt uitgevoerd totdat ofwel de waarde van **varCounter gelijk is aan 3**, of de waarde van **varIsSuccess gelijk is aan Yes**. (varCounter en varIsSuccess zijn de variables die we zojuist hebben aangemaakt.)

1. Het dialoogvenster **Pipeline expression builder** wordt geopend. In de onderste helft van het dialoogvenster ziet u een menu:
   1. **Parameters:** Dit zijn constanten binnen een data factory die door een pipeline in elke expressie kunnen worden gebruikt.
   1. **System variables:** Deze variables kunnen in expressies worden gebruikt bij het definiëren van entiteiten binnen een van de services. Bijv. pipeline id, pipeline name, trigger name, enz.
   1. **Functions:** U kunt functies aanroepen binnen expressies. Functions zijn gecategoriseerd in Collection, Conversion, Date, Logical, Math en String. Bijv. concat is een String-functie, add is een Math-functie, enz.
   1. **Variables:** Pipeline variables zijn waarden die kunnen worden ingesteld en gewijzigd tijdens een pipeline-uitvoering. In tegenstelling tot pipeline parameters, die op pipeline-niveau worden gedefinieerd en niet kunnen worden gewijzigd tijdens een pipeline-uitvoering, kunnen pipeline variables worden ingesteld en gewijzigd binnen een pipeline via een Set Variable activity. We gaan de Set Variable activity zo dadelijk gebruiken.

     ![A screenshot of Pipeline expression builder dialog](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.023.png)

1. Klik op **Functions** in het onderste menu.
1. Vouw de sectie **Logical Functions** uit.
1. Selecteer **or function**. U ziet dat **@or()** wordt toegevoegd aan het tekstvak voor de dynamische expressie. De or function neemt twee parameters. We werken nu aan de eerste parameter.

     ![A screenshot of Pipeline expression builder dialog](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.024.png)

1. Plaats de cursor **tussen de haakjes** van de **@or**-functie.
1. Selecteer vanuit de sectie **Logical Functions** de **equals** function. U ziet dat dit wordt toegevoegd aan het tekstvak voor de dynamische expressie. 

   **Opmerking:** Uw functie zou er als volgt uit moeten zien: **@or(equals())**. De equals function neemt ook drie parameters. We gaan controleren of de variable varCounter gelijk is aan 3.
   
     ![A screenshot of Pipeline expression builder dialog](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.025.png)

1. Plaats nu de cursor **tussen de haakjes** van de **@equals**-functie om de parameters toe te voegen.
1. Selecteer in het onderste menu **Variables**.
1. Selecteer de variable **varCounter**, die de eerste parameter vormt.
1. Voer **3** in als tweede parameter van de equals function. Uw expressie wordt **@or(equals(variables('varCounter'),3))** zoals weergegeven in de onderstaande schermafbeelding.
  
     ![A screenshot of Pipeline expression builder dialog](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.026.png)

1. We moeten de tweede parameter aan de **or**-functie toevoegen. **Voeg een komma toe** tussen de twee afsluitende haakjes. Deze keer proberen we de functienaam te typen. Begin met typen **equ** en u krijgt een dropdown van beschikbare functies (dit heet IntelliSense). Selecteer de **equals** function.

     ![A screenshot of Pipeline expression builder dialog](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.027.png)

1. De eerste parameter van de equals function is een variable. Plaats de **cursor voor de komma**.
1. Begin met typen **variables(**
1. Selecteer met behulp van IntelliSense **variables('varIsSuccess')**.
1. Voer na de komma de tweede parameter in. Begin met typen **variables(**
1. Selecteer met behulp van IntelliSense **variables('varSuccess')**. Hier vergelijken we de waarde van varIsSuccess met de waarde van varSuccess. (varSuccess heeft standaard de waarde Yes.)

     ![A screenshot of Pipeline expression builder dialog](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.028.png)

1. Uw expressie zou er als volgt uit moeten zien:

   **@or(equals(variables('varCounter'),3),equals(variables('varIsSuccess'), variables('varSuccess')))**

1. Selecteer **OK**.

     ![A screenshot of Pipeline expression builder dialog](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.029.png)

### <a name="_toc152204380"></a>Taak 9: Dataflow Activity configureren
1. U wordt teruggeleid naar het ontwerpscherm met de **Until activity geselecteerd**. Selecteer in het **onderste deelvenster** **Activities**. We voegen nu de activities toe die moeten worden uitgevoerd.
2. Selecteer het **bewerkingspictogram** in de eerste rij. U wordt naar een leeg ontwerpscherm voor de iterator geleid.

     ![A screenshot of Activity configuration for Until activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.030.png)

3. Selecteer in het bovenste menu **Activities -> Dataflow**. De Dataflow activity wordt toegevoegd aan het ontwerpdeelvenster.
4. Selecteer met de **Dataflow activity geselecteerd** in het onderste deelvenster **General**. Laten we de activity een naam en beschrijving geven.
5. Voer in het veld **Name** **dfactivity_People_SharePoint** in.
6. Voer in het veld **Description** **Data flow activity to refresh df_People_Sharepoint dataflow** in.

     ![A screenshot of General configuration Dataflow activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.031.png)

7. Selecteer **Settings** in het onderste deelvenster.
8. Zorg dat **Workspace** is ingesteld op **uw workspacenaam**.
9. Selecteer in de **Dataflow dropdown** **df_People_SharePoint**. Wanneer deze Dataflow activity wordt uitgevoerd, vernieuwt zij **df_People_SharePoint**.

     ![A screenshot of Settings configuration Dataflow activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.032.png)

### <a name="_toc152204381"></a>Taak 10: 1<sup>e</sup> Set variable Activity configureren

We hebben de Dataflow activity geconfigureerd zoals eerder in het lab. Nu voegen we nieuwe logica toe. Als de dataflow-vernieuwing succesvol is, moeten we de Until-iterator verlaten. Een van de voorwaarden om de iterator te verlaten is het instellen van de waarde van de variable varIsSuccess op Yes.

1. Selecteer in het bovenste menu **Activities -> Set variable**. De Set variable activity wordt toegevoegd aan het ontwerpcanvas.
2. Selecteer met de **Set variable activity geselecteerd** in het onderste deelvenster **General**. Laten we de activity een naam en beschrijving geven.
3. Voer in het veld **Name** **set_varIsSuccess** in.
4. Voer in het veld **Description** **Set variable varIsSuccess to Yes** in.

   **Opmerking:** Beweeg de cursor over de **Dataflow activity**. Rechts van het activiteitsvak ziet u vier pictogrammen. Deze kunnen worden gebruikt om verbinding te maken met de volgende activity op basis van het resultaat van de activity:

   **Opmerking:** Het pictogram met de **grijze gebogen pijl** wordt gebruikt om de activity over te slaan.
   
   **Opmerking:** Het pictogram met het **groene vinkje** wordt gebruikt bij het slagen van de activity.

   **Opmerking:** Het pictogram met het **rode kruis** wordt gebruikt bij het mislukken van de activity.
   
   **Opmerking:** Het pictogram met de **blauwe rechte pijl** wordt gebruikt bij het voltooien van de activity.

5. Klik op het **groene vinkje** en sleep om de **Dataflow activity** te verbinden met de **Set variable activity**. Bij het succesvol vernieuwen van de data flow willen we de Set variable activity uitvoeren.

     ![A screenshot of General configuration Set variable activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.033.png)

6. Selecteer met de **Set variable activity geselecteerd** **Settings** in het onderste menu.
7. Zorg in het onderste deelvenster dat **Variable type** is ingesteld op **Pipeline variable**.
8. Selecteer in het veld **Name** **varIsSuccess**.
9. Dit is de variable waarvan we de waarde gaan instellen.
10. Selecteer in het veld **Value** het **tekstvak**. Selecteer de koppeling **Add dynamic content**.
   
     ![A screenshot of Settings configuration Set variable activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.034.png)

11. Het dialoogvenster Pipeline expression builder wordt geopend. Selecteer het **tekstgebied Add dynamic content hieronder**.
12. Selecteer in het onderste menu **Variables -> varSuccess**. U ziet dat @variables('varSuccess') wordt ingevoerd in het tekstgebied Add dynamic content hieronder. Toen we de variables aanmaakten, hadden we de waarde van de variable varSuccess vooraf ingesteld op Yes. Zo kennen we de waarde Yes toe aan de variable varIsSuccess.
13. Selecteer **OK**. U wordt teruggeleid naar het **ontwerpdeelvenster van de iterator**.

     ![A screenshot of Pipeline expression builder](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.035.png)

Nu moeten we de teller instellen als de dataflow activity mislukt. In Data Pipeline kunnen we geen variable naar zichzelf verwijzen. Dit betekent dat we de teller-variable varCounter niet kunnen verhogen door er één bij op te tellen (varCounter = varCounter + 1). Daarom maken we gebruik van de variable varTempCounter.

### <a name="_toc152204382"></a>Taak 11: 2<sup>e</sup> Set variable Activity configureren

1. Selecteer in het bovenste menu **Activities -> Set variable**. De Set variable activity wordt toegevoegd aan het ontwerpcanvas.
2. Selecteer met de **Set variable activity geselecteerd** in het onderste deelvenster **General**. Laten we de activity een naam en beschrijving geven.
3. Voer in het veld **Name** **set_varTempCounter** in.
4. Voer in het veld **Description** **Increment variable varTempCounter** in.
5. Klik op het **rode kruis** van de Dataflow activity naar de nieuwe Set variable activity. Bij het mislukken van de data flow-vernieuwing willen we deze Set variable activity uitvoeren.

     ![A screenshot of General configuration Set variable activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.036.png)

6. Selecteer met de **Set variable activity geselecteerd** **Settings** in het onderste menu.
7. Zorg in het onderste deelvenster dat **Variable type** is ingesteld op **Pipeline variable**.
8. Selecteer in het veld **Name** **varTempCounter**.
   Dit is de variable waarvan we de waarde gaan instellen.
9. Selecteer in het veld **Value** het **tekstvak**. Selecteer de koppeling **Add dynamic content**.
10. Het dialoogvenster Pipeline expression builder wordt geopend. Voer **@add(variables('varCounter'),1)** in.

    **Opmerking:** U kunt deze expressie vrij typen, via het menu de functies selecteren of plakken. 

     ![A screenshot of Settings configuration Set variable activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.037.png)

      Nu moeten we de waarde van de variable varCounter instellen op de waarde van varTempCounter. 

### <a name="_toc152204383"></a>Taak 12: 3<sup>e</sup> Set variable Activity configureren

1. Selecteer in het bovenste menu **Activities -> Set variable**. De Set variable activity wordt toegevoegd aan het ontwerpcanvas.
1. Selecteer met de **Set variable activity geselecteerd** in het onderste deelvenster **General**. Laten we de activity een naam en beschrijving geven.
1. Voer in het veld **Name** **set_varCounter** in.
1. Voer in het veld **Description** **Increment variable varCounter** in.
1. Selecteer het **groene vinkje** van de Set variable activity set_varTempCounter naar de nieuwe Set variable activity. 

     ![A screenshot of General configuration Set variable activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.038.png)

1. Selecteer met de **Set variable activity set_varCounter geselecteerd** **Settings** in het onderste menu.
1. Zorg in het onderste deelvenster dat **Variable type** is ingesteld op **Pipeline variable**.
1. Selecteer in het veld **Name** **varCounter**. Dit is de variable waarvan we de waarde gaan instellen.
1. Selecteer in het veld **Value** het **tekstvak**. Selecteer de koppeling **Add dynamic content**.
1. Het dialoogvenster Pipeline expression builder wordt geopend. Voer **@variables('varTempCounter')** in. U kunt deze expressie vrij typen, via het menu de functies selecteren of plakken. 

     **Opmerking:** Deze functie stelt de waarde van variable varCounter in op de waarde van variable varTempCounter (varCounter = varTempCounter). Aan het einde van elke iteratie hebben zowel varCounter als varTempCounter dezelfde waarde.
   
     ![A screenshot of Settings configuration Set variable activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.039.png)

### <a name="_toc152204384"></a>Taak 13: Wait Activity configureren

Vervolgens moeten we 5 minuten/300 seconden wachten als de data flow-vernieuwing de eerste keer mislukt voordat we het opnieuw proberen. Als de data flow-vernieuwing de tweede keer mislukt, moeten we 15 minuten/900 seconden wachten en het opnieuw proberen. We gaan de Wait activity en de variable varWaitTime gebruiken om de wachttijd in te stellen.

1. Selecteer in het bovenste menu **Activities -> ellipsis (…)-> Wait**. De Wait activity wordt toegevoegd aan het ontwerpcanvas.
2. Selecteer met de **Wait activity geselecteerd** in het onderste deelvenster **General**. Laten we de activity een naam en beschrijving geven.
3. Voer in het veld **Name** **wait_onFailure** in.
4. Voer in het veld **Description** **Wait for 300 seconds on 2nd try and 900 seconds on 3rd try** in.
5. Selecteer het **groene vinkje** van de Set variable activity set_varCounter naar de nieuwe Wait activity. 

     ![A screenshot of General configuration Wait activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.040.png)

6. Selecteer met de Wait activity geselecteerd **Settings** in het onderste menu.
7. Selecteer in het veld **Wait time in seconds** het tekstvak. Selecteer de koppeling **Add dynamic content**.
8. Het dialoogvenster Pipeline expression builder wordt geopend. Voer het volgende in:
  
       @if(
          greater(variables('varCounter'), 1),
          if(equals(variables('varCounter'), 2),
          mul(variables('varWaitTime'),15 ),
          mul(variables('varWaitTime'), 0)
          ),
          mul(variables('varWaitTime'),5 )
          )
     
     U kunt deze expressie vrij typen, via het menu de functies selecteren of plakken. 

      ![A screenshot of Settings configuration Wait activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.041.png)

We gebruiken hier twee nieuwe functies:

- **greater:** Neemt twee getallen als parameters en vergelijkt welke groter is.
- **mul:** Dit is een vermenigvuldigingsfunctie. Neemt twee parameters om te vermenigvuldigen. 

De expressie is een geneste if-instructie. Deze controleert of de waarde van de variable varCounter groter is dan 1. Als dat het geval is, wordt gecontroleerd of de waarde van de variable varCounter gelijk is aan 2. Als dat het geval is, wordt de wachttijd ingesteld op varWaitTime maal 15. We hadden de waarde van varWaitTime standaard ingesteld op 60. Dat zou 60\*15 = 900 seconden zijn. Als de waarde van de variable varCounter niet 2 is (dus groter dan 2, wat betekent dat de data flow-vernieuwing 3 keer is mislukt en we klaar zijn met herhalen. We hoeven niet meer te wachten), wordt de wachttijd ingesteld op varWaitTime \* 0. Dus op 0. Als de waarde van de variable varCounter 1 is, vermenigvuldigen we varWaitTime \* 5. Dat zou 60\*5 = 300 seconden zijn.

9. Selecteer **OK**. 

    **Controlepunt:** Uw Until Iterator zou er uit moeten zien als de onderstaande schermafbeelding.

      ![A screenshot of activities in Until activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.042.png)

10. Selecteer **pl_refresh_people_Sharepoint_option2** linksboven in het ontwerpcanvas om de Until iterator te verlaten. 

      ![A screenshot of activities in Until activity](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.043.png)

11. We zijn klaar met het aanmaken van de data pipeline. Selecteer in het bovenste menu **Home -> Save**-pictogram om de data pipeline op te slaan.

      ![A screenshot of Data Pipeline](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.044.png)

### <a name="_toc152204385"></a>Taak 14: Geplande vernieuwing configureren voor Data Pipeline

1. We kunnen de data pipeline testen door **Home -> Run** te selecteren. 
      **Opmerking:** Het kan een paar minuten duren voordat de data pipeline de vernieuwing voltooit. Dit is een trainingsomgeving, dus het bestand in SharePoint is altijd beschikbaar. Uw data pipeline zal daarom nooit mislukken.
2. We kunnen de data pipeline instellen om volgens een schema te worden uitgevoerd. Selecteer in het bovenste menu **Home -> Schedule**. Het dialoogvenster Schedule wordt geopend.
3. Zet de keuzeknop **Scheduled run** op **On**.
4. Stel de dropdown **Repeat** in op **Daily**.
5. Stel **Time** in op **9 AM**.
6. Stel **Start date and time** in op **vandaag**.
7. Stel **End date and time** in op een **toekomstige datum**.
8. Stel uw **Time zone** in.

    **Opmerking:** Omdat dit een labomgeving is, kunt u de tijdzone naar wens instellen. In een echte situatie stelt u de tijdzone in op basis van uw eigen locatie of die van de databron.

9. Selecteer **Apply**.
10. Selecteer de **X** rechtsboven in het dialoogvenster om het te sluiten.

       ![A screenshot of refresh schedule of Data Pipeline](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.045.png)

11. Selecteer **uw workspacenaam** in het linkerdeelvenster om naar het startscherm van Data Factory te navigeren.

  **Opmerking:** In het scherm Schedule is er geen optie om bij succes of mislukking een melding te sturen (zoals bij Dataflow Schedule). Meldingen kunnen worden gedaan door een activity toe te voegen in de Data Pipeline. We doen dit niet in dit lab omdat het een labomgeving is.

  We hebben vernieuwingsschema's ingesteld voor de verschillende databronnen. In het volgende lab maken we rapporten aan.

# <a name="_toc150777627"></a><a name="_toc150779083"></a><a name="_toc152204386"></a>**Referenties**

Fabric Analyst in a Day (FAIAD) maakt u vertrouwd met enkele van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service vindt u in de sectie Help (?) links naar nuttige bronnen.

   ![A screenshot of help options](../media/Aspose.Words.8e9803f1-24d8-45d0-b7f3-d4af1b019516.046.png)

Hieronder vindt u nog enkele bronnen die u helpen bij uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [aankondiging van Microsoft Fabric GA](https://aka.ms/Fabric-Hero-Blog-Ignite23)
- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)
- Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)
- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)
- Leer nieuwe vaardigheden via de [Fabric Learning-modules](https://aka.ms/learn-fabric)
- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)
- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om uw vragen te stellen, feedback te delen en van anderen te leren

Lees de meer uitgebreide aankondigingsblogs over Fabric-ervaringen:

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

Door gebruik te maken van deze demo/dit lab, gaat u akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation beschikbaar gesteld met het doel uw feedback te verzamelen en u een leerervaring te bieden. U mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback aan Microsoft te geven. U mag het niet voor enig ander doel gebruiken. U mag deze demo/dit lab of een deel ervan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN DEEL ERVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE TEN BEHOEVE VAN VERDERE REPRODUCTIE OF HERVERSPREIDING IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARE-TECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN IN DEZE DEMO/DIT LAB VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DEZELFDE MANIER ALS EEN DEFINITIEVE VERSIE. WE KUNNEN OOK BESLUITEN GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UIT TE BRENGEN. UW ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK ANDERS ZIJN.

**FEEDBACK**. Als u feedback geeft over de technologiefuncties, functionaliteit en/of concepten die in deze demo/dit lab worden beschreven aan Microsoft, geeft u Microsoft het recht om uw feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, te delen en te commercialiseren, zonder kosten. U geeft ook aan derden, zonder kosten, eventuele octrooirechten die nodig zijn voor hun producten, technologieën en diensten om bepaalde onderdelen van een Microsoft-software of -service die de feedback bevat te gebruiken of te koppelen. U geeft geen feedback die onderworpen is aan een licentie die vereist dat Microsoft zijn software of documentatie in licentie geeft aan derden omdat wij uw feedback daarin opnemen. Deze rechten blijven van kracht na afloop van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN AF MET BETREKKING TOT DE DEMO/HET LAB, INCLUSIEF ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, ZOWEL UITDRUKKELIJK, IMPLICIET ALS WETTELIJK, GESCHIKTHEID VOOR EEN BEPAALD DOEL, TITEL EN NIET-INBREUK. MICROSOFT GEEFT GEEN VERZEKERINGEN OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE OUTPUT DIE VOORTVLOEIT UIT GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR WELK DOEL DAN OOK.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen veranderen in toekomstige versies van het product. In deze demo/dit lab leert u over enkele, maar niet alle, nieuwe functies.
