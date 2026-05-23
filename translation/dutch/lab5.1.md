
# Microsoft Fabric - Fabric Analyst in a Day - Lab 5

# ![](../media/Lab_5.1_1.png)
 
# Inhoud

- Introductie	

- Dataflow Gen2	

    - Taak 1: Geplande vernieuwing configureren voor Sales Dataflow	

    - Taak 2: Geplande vernieuwing configureren voor Supplier en Customer Dataflow	

- Data Pipeline	

    - Taak 3: Data Pipeline aanmaken	

    - Taak 4: Eenvoudige Data Pipeline bouwen	

    - Taak 5: Nieuwe Data Pipeline aanmaken	

    - Taak 6: Until Activity aanmaken	

    - Taak 7: Variables aanmaken	

    - Taak 8: Until Activity configureren	

    - Taak 9: Dataflow Activity configureren	

    - Taak 10: 1e Set variable Activity configureren	

    - Taak 11: 2e Set variable Activity configureren	

    - Taak 12: 3e Set variable Activity configureren	

    - Taak 13: Wait Activity configureren	

    - Taak 14: Geplande vernieuwing configureren voor Data Pipeline	

- Referenties	



# Introductie 

We hebben gegevens uit verschillende databronnen opgenomen in de Lakehouse. In dit lab stel je een vernieuwingsschema in voor de databronnen. Ter herinnering, de vereisten zijn:

- Sales-data: ADLS wordt elke dag bijgewerkt om 12:00 uur (noon / 12 PM).

- Supplier-data: Snowflake wordt elke dag bijgewerkt om middernacht / 12 AM.

- Customer-data: Dataverse is altijd actueel. We moeten dit vier keer per dag vernieuwen: om middernacht / 12 AM, 6 AM, noon / 12 PM en 6 PM.

- Employee-data: in SharePoint wordt elke dag om 9 AM bijgewerkt. We hebben echter geconstateerd dat er soms een vertraging is van 5 tot 15 minuten. We moeten een vernieuwingsschema maken dat hiermee rekening houdt.

Aan het einde van dit lab heb je geleerd: 

- Hoe je een geplande vernieuwing van Dataflow Gen2 configureert

- Hoe je een Data Pipeline aanmaakt

- Hoe je een geplande vernieuwing van een Data Pipeline configureert

# Dataflow Gen2

## Taak 1: Geplande vernieuwing configureren voor Sales Dataflow
Laten we beginnen met het configureren van een geplande vernieuwing van de Sales Dataflow.

1. Navigeer terug naar de Fabric workspace, **FAIAD_** die je hebt aangemaakt in Lab 2, Taak 9.

2. Alle artefacten die je hebt aangemaakt worden hier weergegeven. Rechts in het scherm, in de **Search box**, typ je **df**. Hierdoor worden de artefacten gefilterd op Dataflows.

    ![](../media/Lab_5.2.png)
 
3. Beweeg de cursor over de rij **df_Sales_ADLS**. Je ziet dat de vertrouwde pictogrammen **Refresh** en **Schedule Refresh** beschikbaar zijn. Selecteer de **ellipsis (…)**.

4. Er zijn opties om de Dataflow te verwijderen, te bewerken en te exporteren. Via Properties kun je de naam en beschrijving van de Dataflow bijwerken. We bekijken Refresh history zo meteen. Selecteer **Settings**.

    ![](../media/Lab_5.3.png)
 
    >**Opmerking**: De pagina Settings opent. In het linkerdeelvenster zie je alle Dataflows weergegeven. 

5. Selecteer in het middelste deelvenster de koppeling **Refresh history**.

    ![](../media/Lab_5.4.png)
 
6. Het dialoogvenster Refresh history opent. Je ziet een aantal vernieuwingen weergegeven. Dit zijn de vernieuwingen die plaatsvinden wanneer de dataflow wordt gepubliceerd. Selecteer de koppeling **Start time**.

    **Opmerking**: De starttijd zal bij jou anders zijn.
 
    ![](../media/Lab_5.5.png)

    Het scherm Details opent. Dit geeft details van de vernieuwing weer: de start- en eindtijd en de duur. Ook worden de tabellen/activiteiten weergegeven die zijn vernieuwd. Als er een fout optreedt, kun je op de naam van de tabel/activiteit klikken om verder onderzoek te doen.

    ![](../media/Lab_5.6.png)
 
7. Navigeer weg door op de **X** in de rechterbovenhoek te klikken. Je keert terug naar de **pagina met dataflow-instellingen**.

8. Vouw onder Gateway connection de sectie **Data source credentials** uit. Er wordt een lijst weergegeven van verbindingen die in de dataflow worden gebruikt. In dit geval Lakehouse en ADLS. 

    a. **Lakehouse**: Dit is de verbinding voor het opnemen van gegevens vanuit de Dataflow.

    b. **ADLS**: Dit is de verbinding met de ADLS-brondata.
 
    ![](../media/Lab_5.7.png)

9. Vouw **Refresh** uit.

10. Zet de schuifregelaar **Configure a refresh schedule** op **On**.

11. Stel de **Refresh frequency dropdown** in op **Daily**. Je ziet dat er ook een optie is om dit in te stellen op Weekly.

12. Stel de **Time Zone** in op je gewenste tijdzone. 

    >**Opmerking**: Omdat dit een labomgeving is, kun je de tijdzone instellen op je voorkeurstijdzone. In een echte situatie stel je de tijdzone in op basis van jouw locatie of de locatie van de databron.

13. Klik op de koppeling **Add another time**. Je ziet dat de optie **Time** verschijnt.

14. Stel **Time** in op **noon**. Je kunt de vernieuwing instellen op het hele of halve uur.

15. Selecteer **Apply** om deze instelling op te slaan.

    **Opmerking**: Door op de koppeling Add another time te klikken, kun je meerdere vernieuwingstijden toevoegen. 

    Je kunt ook foutmeldingen sturen naar de eigenaar van de dataflow en andere contactpersonen.
    
    ![](../media/Lab_5.8.png)

## Taak 2: Geplande vernieuwing configureren voor Supplier en Customer Dataflow

1. Selecteer in het linkerdeelvenster **df_Supplier_Snowflake**.

2. Configureer het vernieuwingsschema zodat het **elke dag om middernacht / 12 AM** wordt vernieuwd. 

3. Selecteer **Apply** om deze instelling op te slaan.

    ![](../media/Lab_5.9.png)
 
4. Selecteer in het linkerdeelvenster **df_Customer_Dataverse**.

5. Configureer het vernieuwingsschema voor vier keer per dag: **middernacht / 12 AM, 6 AM, noon / 12 PM en 6 PM**.

6. Selecteer **Apply** om deze instelling op te slaan.

    ![](../media/Lab_5.10.png)
 
    Zoals eerder vermeld, moeten we aangepaste logica bouwen voor het scenario waarbij het Employee-bestand in SharePoint niet op tijd wordt aangeleverd. Laten we Data Pipeline gebruiken om dit op te lossen.

# Data Pipeline

## Taak 3: Data Pipeline aanmaken

1. Selecteer het pictogram **Fabric experience selector** linksonder in het scherm.

2. Het dialoogvenster Microsoft Fabric opent. Selecteer **Data Factory**. Je navigeert naar de startpagina van Data Factory.
 
    ![](../media/Lab_5.11.png)

3. Selecteer in het bovenste paneel **Data pipeline** om een nieuwe pipeline aan te maken.

4. Het dialoogvenster New pipeline opent. Geef de pipeline de naam **pl_Refresh_People_SharePoint**

5. Selecteer **Create**.
  
    ![](../media/Lab_5.12.png)

    Je navigeert naar de pagina **Data Pipeline**. Als je eerder met Azure Data Factory hebt gewerkt, is dit scherm je bekend. Laten we een kort overzicht geven van de indeling.

    Je bevindt je op het scherm **Home**. In het bovenste menu vind je opties om veelgebruikte activiteiten toe te voegen: valideren, een pipeline uitvoeren en de uitvoeringsgeschiedenis bekijken. In het middelste deelvenster vind je ook snelkoppelingen om de pipeline te beginnen bouwen.

    ![](../media/Lab_5.13.png)
 
6. Selecteer in het bovenste menu **Activities**. In het menu zie je nu een lijst van veelgebruikte activiteiten.

7. Selecteer de **ellipsis (…)** rechts van het menu om alle andere beschikbare activiteiten te bekijken. We gaan een aantal van deze activiteiten gebruiken in het lab.

    ![](../media/Lab_5.14.png)
 
8. Klik in het bovenste menu op **Run**. Je vindt hier opties om de pipeline uit te voeren en in te plannen. Je kunt ook de uitvoeringsgeschiedenis bekijken via View Run History.

9. Selecteer in het bovenste menu **View**. Hier vind je opties om de code in JSON-formaat te bekijken. Je vindt hier ook opties om de activiteiten op te maken.

    **Opmerking**: Als je een achtergrond hebt met JSON, kun je aan het einde van het lab View JSON code selecteren. Je zult zien dat alle orchestratie die je via de ontwerpweergave uitvoert, ook in JSON kan worden geschreven. 

    ![](../media/Lab_5.15.png)
 
## Taak 4: Eenvoudige Data Pipeline bouwen

Laten we beginnen met het bouwen van de pipeline. We hebben een activiteit nodig om de Dataflow te vernieuwen. Laten we een geschikte activiteit zoeken.

1. Selecteer in het bovenste menu **Activities -> Dataflow**. De Dataflow activity wordt toegevoegd aan het middelste ontwerpdeelvenster. In het onderste deelvenster zie je nu configuratieopties voor de Dataflow activity.

2. We gaan de activiteit configureren om verbinding te maken met de activiteit df_People_SharePoint. Selecteer in het **onderste deelvenster** **Settings**.

3. Zorg ervoor dat **Workspace** is ingesteld op je Fabric workspace, **FAIAD_<username>**.

4. Selecteer in de **Dataflow dropdown** **df_People_SharePoint**. Wanneer deze Dataflow activity wordt uitgevoerd, wordt **df_People_SharePoint** vernieuwd. Dat was eenvoudig, toch? 😊

    **Opmerking**: De Notification-optie is momenteel grijs weergegeven. Deze functie wordt binnenkort ingeschakeld. Je kunt dan meldingen configureren bij het slagen of mislukken van deze activiteit. 

    In ons scenario worden de Employee-gegevens niet op schema bijgewerkt. Soms is er een vertraging. Laten we kijken of we dit kunnen opvangen.

    ![](../media/Lab_5.16.png)
 
5. Selecteer in het **onderste deelvenster** **General**. Laten we de activiteit een naam en beschrijving geven.

6. Voer in het veld **Name** in: **dfactivity_People_SharePoint**

7. Voer in het veld **Description** in: **Dataflow activity to refresh df_People_Sharepoint dataflow**.

8. Er is een optie om een activiteit te deactiveren. Deze functie is handig tijdens testen of debuggen. Laat dit op **Activated** staan.

9. Er is een optie om **Timeout** in te stellen. Laat de **standaardwaarde** staan, deze geeft de dataflow voldoende tijd om te vernieuwen.

    **Opmerking**: Als de data niet op schema beschikbaar is, stel de activiteit dan in om elke 10 minuten opnieuw te worden uitgevoerd, drie keer. Als de derde poging ook mislukt, wordt er een fout gerapporteerd.
    
10. Stel **Retry** in op **3** 

11. Vouw de sectie **Advanced** uit.

12. Stel **Retry interval (sec)** in op **600**. 

13. Selecteer in het menu **Home -> Save** om de pipeline op te slaan.

    ![](../media/Lab_5.17.png)
 
Let op het voordeel van het gebruik van de data pipeline ten opzichte van het instellen van geplande vernieuwing op de dataflow (zoals we voor de eerdere dataflows hebben gedaan):

- De pipeline biedt de mogelijkheid om meerdere keren opnieuw te proberen voordat de vernieuwing als mislukt wordt beschouwd.

- De pipeline biedt de mogelijkheid om binnen seconden te vernieuwen, terwijl bij een dataflow de geplande vernieuwing minimaal elke 30 minuten plaatsvindt.

## Taak 5: Nieuwe Data Pipeline aanmaken

Laten we ons scenario iets complexer maken. We hebben geconstateerd dat als de data niet beschikbaar is om 9 AM, deze doorgaans binnen vijf minuten beschikbaar komt. Als dit tijdvenster wordt gemist, duurt het 15 minuten voordat het bestand beschikbaar is. We willen de nieuwe pogingen plannen op vijf en 15 minuten. Laten we kijken hoe dit kan worden gerealiseerd door een nieuwe Data Pipeline aan te maken.

1. Klik in het linkerdeelvenster op **FAIAD_<username>** om naar de workspace-startpagina te navigeren.

2. Klik in het bovenste menu op **New** en klik in de **dropdown** op **Data pipeline**.

3. Het dialoogvenster New pipeline opent. Geef de pipeline de **naam** **pl_Refresh_People_SharePoint_Option2**

4. Selecteer **Create**.

    ![](../media/Lab_5.18.png)
 
## Taak 6: Until Activity aanmaken

1. Je navigeert naar het scherm Data Pipeline. Selecteer in het menu **Activities**.

2. Klik op de **ellipsis(…)** aan de rechterkant.

3. Klik in de lijst met activiteiten op **Until**. 

    **Until**: is een activiteit die wordt gebruikt om te itereren totdat aan een voorwaarde is voldaan. 

    In ons scenario gaan we itereren en de dataflow vernieuwen totdat dit succesvol is of we drie keer hebben geprobeerd.
 
    ![](../media/Lab_5.19.png)

## Taak 7: Variables aanmaken

1. We moeten variables aanmaken die worden gebruikt om te itereren en de status in te stellen. Selecteer het **lege gebied** in het ontwerpdeelvenster van de pipeline.

2. Het menu in het onderste deelvenster wijzigt. Selecteer **Variables**.

3. Selecteer **+ New** om een nieuwe variabele toe te voegen.

4. Er verschijnt een rij. Voer **varCounter** in het **tekstvak Name** in. We gebruiken deze variabele om drie keer te itereren.

5. Selecteer in de **Type dropdown** **Integer**.

6. Voer de **Default value** **0** in.

    **Opmerking**: We zetten de prefix var voor de namen van variabelen, zodat ze gemakkelijk te vinden zijn. Dit is ook een goede praktijk.
 
    ![](../media/Lab_5.20.png)

7. Selecteer **New** om nog een nieuwe variabele toe te voegen.

8. Er verschijnt een rij. Voer **varTempCounter** in het **tekstvak Name** in. We gebruiken deze variabele om de variabele varCounter te verhogen.

9. Selecteer in de **Type dropdown** **Integer**.

10. Voer de **Default value** **0** in.

11. Voer vergelijkbare stappen uit om nog drie variabelen toe te voegen:

    a. **varIsSuccess** van het type **String** met als standaardwaarde **No**. Deze variabele wordt gebruikt om aan te geven of de vernieuwing van de dataflow succesvol was.

    b. **varSuccess** van het type **String** met als standaardwaarde **Yes**. Deze variabele wordt gebruikt om de waarde van varIsSuccess in te stellen als de vernieuwing van de dataflow succesvol was.

    c. **varWaitTime** van het type **Integer** met als standaardwaarde **60**. Deze variabele wordt gebruikt om de wachttijd in te stellen als de dataflow mislukt. (Ofwel 5 minuten/300 seconden of 15 minuten/900 seconden.)

## Taak 8: Until Activity configureren

1. Selecteer de **Until** activity. 

2. Selecteer in het **onderste deelvenster** **General**.

3. Voer als **Name** in: **Iterator**

4. Voer als **Description** in: **Iterator to refresh dataflow. It will retry up to 3 times**. 

    ![](../media/Lab_5.21.png)
 
5. Selecteer in het onderste deelvenster **Settings**.

6. Selecteer het **tekstvak Expression**. We moeten een expressie invoeren die evalueert naar true of false. De Until activity itereert zolang deze expressie evalueert naar false. Zodra de expressie evalueert naar true, stopt de activiteit met itereren.

7. Selecteer de koppeling **Add dynamic content** die onder het tekstvak verschijnt.
 
    ![](../media/Lab_5.22.png)

    We moeten een expressie schrijven die blijft uitvoeren totdat de waarde van **varCounter 3** is of de waarde van **varIsSuccess Yes** is. (varCounter en varIsSuccess zijn de variabelen die we zojuist hebben aangemaakt.)

8. Het dialoogvenster **Pipeline expression builder** opent. In de onderste helft van het dialoogvenster vind je een menu:

    a. **Parameters**: Dit zijn constanten binnen een data factory die door een pipeline kunnen worden gebruikt in elke expressie.

    b. **System variables**: Deze variabelen kunnen worden gebruikt in expressies bij het definiëren van entiteiten binnen een service. Bijvoorbeeld: pipeline id, pipeline name, trigger name, enzovoort.

    c. **Functions**: Je kunt functies aanroepen binnen expressies. Functies zijn gecategoriseerd in Collection, Conversion, Date, Logical, Math en String functies. Bijvoorbeeld: concat is een String-functie, add is een Math-functie, enzovoort.

    d. **Variables**: Pipeline variables zijn waarden die kunnen worden ingesteld en gewijzigd tijdens een pipeline-uitvoering. In tegenstelling tot pipeline parameters, die worden gedefinieerd op het niveau van de pipeline en niet kunnen worden gewijzigd tijdens een pipeline-uitvoering, kunnen pipeline variables worden ingesteld en gewijzigd binnen een pipeline met behulp van een Set Variable activity. We gaan de Set Variable activity zo meteen gebruiken.

    ![](../media/Lab_5.23.png)
 
9. Klik op **Functions** in het onderste menu.

10. Selecteer in de sectie **Logical Functions** de **or function**. Je ziet dat **@or()** wordt toegevoegd aan het tekstvak voor de dynamische expressie. De or-functie heeft twee parameters; we werken aan de eerste parameter.

    ![](../media/Lab_5.24.png)
 
11. Plaats de cursor **tussen de haakjes** van de **@or**-functie.

12. Selecteer in de sectie **Logical Functions** de **equals**-functie. Je ziet dat deze wordt toegevoegd aan het tekstvak voor de dynamische expressie. 

    **Opmerking**: Je functie zou er als volgt uit moeten zien: **@or(equals())**. De equals-functie heeft ook twee parameters. We controleren of de variabele varCounter gelijk is aan 3.

    ![](../media/Lab_5.25.png)
 
13. Plaats nu de cursor **tussen de haakjes** van de **@equals**-functie om de parameters toe te voegen.

14. Selecteer in het onderste menu **Variables**.

15. Selecteer de variabele **varCounter** als eerste parameter.

16. Voer 3 in als tweede parameter van de equals-functie. Zoals in de schermafbeelding hieronder zal je expressie zijn: **@or(equals(variables('varCounter'),3))** 

    ![](../media/Lab_5.26.png)
 
17. We moeten de tweede parameter toevoegen aan de or-functie. **Voeg een komma toe** tussen de twee afsluitende haakjes. Deze keer proberen we de functienaam zelf te typen. Begin met typen: **equ** en je krijgt een dropdown met beschikbare functies (dit wordt IntelliSense genoemd). Selecteer de **equals**-functie.

    ![](../media/Lab_5.27.png)
 
18. De eerste parameter van de equals-functie is een variabele. Plaats de **cursor vóór de komma**.

19. Begin met typen: **variables(**

20. Selecteer met behulp van IntelliSense **variables('varIsSuccess')**

21. Voer na de komma de tweede parameter in. Begin met typen: **variables(**

22. Selecteer met behulp van IntelliSense **variables('varSuccess')**. Hier vergelijken we de waarde van varIsSuccess met de waarde van varSuccess. (varSuccess heeft als standaardwaarde Yes.)

    ![](../media/Lab_5.28.png)
 
23. Je expressie moet zijn: **@or(equals(variables('varCounter'),3),equals(variables('varIsSuccess'), variables('varSuccess')))**

24. Selecteer **OK**.
 
    ![](../media/Lab_5.29.png)

## Taak 9: Dataflow Activity configureren

1. Je navigeert terug naar het ontwerpscherm. Met de **Until activity** geselecteerd, selecteer je in het **onderste deelvenster** **Activities**. We voegen nu de activiteiten toe die moeten worden uitgevoerd.

2. Selecteer het **bewerkingspictogram** in de eerste rij. Je navigeert naar een leeg iteratorontwerpscherm.

    ![](../media/Lab_5.30.png)
 
3. Selecteer in het bovenste menu **Activities -> Dataflow**. De Dataflow activity wordt toegevoegd aan het ontwerpdeelvenster.

4. Selecteer met de **Dataflow activity geselecteerd** in het onderste deelvenster **General**. Laten we de activiteit een naam en beschrijving geven.

5. Voer in het veld **Name** in: **dfactivity_People_SharePoint**

6. Voer in het veld **Description** in: **Dataflow activity to refresh df_People_Sharepoint dataflow**.

   ![](../media/Lab_5.31.png)
 
7. Selecteer **Settings** in het onderste deelvenster.

8. Zorg ervoor dat **Workspace** is ingesteld op je workspace, **FAIAD_<username>**.

9. Selecteer in de **Dataflow dropdown** **df_People_SharePoint**. Wanneer deze Dataflow activity wordt uitgevoerd, wordt **df_People_SharePoint** vernieuwd.

    ![](../media/Lab_5.32.png)
 

## Taak 10: 1e Set variable Activity configureren

We hebben de Dataflow activity geconfigureerd zoals we eerder in het lab hebben gedaan. Nu voegen we nieuwe logica toe. Als de vernieuwing van de dataflow succesvol is, moeten we de Until-iterator afsluiten. Onthoud dat één van de voorwaarden om de iterator af te sluiten is dat de waarde van de variabele varIsSuccess op Yes wordt ingesteld.

1. Selecteer in het bovenste menu **Activities -> Set variable**. De Set variable activity wordt toegevoegd aan het ontwerpcanvas.

2. Selecteer met de **Set variable activity** geselecteerd in het onderste deelvenster **General**. Laten we de activiteit een naam en beschrijving geven.

3. Voer in het veld **Name** in: **set_varIsSuccess**

4. Voer in het veld **Description** in: **Set variable varIsSuccess to Yes**.

    **Opmerking**: Beweeg de cursor over de **Dataflow activity**. Rechts van het activiteitsvak zijn vier pictogrammen zichtbaar. Deze kunnen worden gebruikt om verbinding te maken met de volgende activiteit op basis van het resultaat van de activiteit:

    a. Het pictogram met de **grijze gebogen pijl** wordt gebruikt om de activiteit over te slaan.

    b. Het pictogram met het **groene vinkje** wordt gebruikt bij succes van de activiteit.

    c. Het pictogram met het **rode kruisje** wordt gebruikt bij mislukking van de activiteit.

    d. Het pictogram met de **blauwe rechte pijl** wordt gebruikt bij voltooiing van de activiteit.

5. Klik op het **groene vinkje** van de Dataflow activity dfactivity_People_SharePoint en sleep dit naar de nieuwe **Set variable activity set_varIsSuccess**. Bij succes van de dataflowvernieuwing willen we de Set variable activity uitvoeren.

    ![](../media/Lab_5.33.png)
 
6. Selecteer met de **Set variable activity** geselecteerd, **Settings** in het onderste menu.

7. Zorg er in het onderste deelvenster voor dat **Variable type** is ingesteld op **Pipeline variable**.

8. Selecteer in het veld **Name** **varIsSucces**. Dit is de variabele waarvan we de waarde gaan instellen.

9. Selecteer in het veld **Value** het **tekstvak**. Selecteer de koppeling **Add dynamic content**.

    ![](../media/Lab_5.34.png)
 
10. Het dialoogvenster Pipeline expression builder opent. Selecteer het **tekstvak Add dynamic content below using any combination of expressions, functions, and system variables**.

11. Selecteer in het onderste menu **Variables -> varSuccess**. Je ziet dat @variables('varSuccess') wordt ingevoerd in het tekstvak Add dynamic content below. Onthoud dat we bij het aanmaken van de variabelen de waarde van de variabele varSuccess hebben ingesteld op Yes. We kennen dus de waarde Yes toe aan de variabele varIsSuccess.

12. Selecteer **OK**. Je navigeert terug naar het **iteratorontwerpdeelvenster**.

    ![](../media/Lab_5.35.png)
 
Nu moeten we de teller instellen als de dataflow activity mislukt. In Data Pipeline kunnen we een variabele niet naar zichzelf verwijzen. Dit betekent dat we de tellervariabele varCounter niet kunnen verhogen door er één bij op te tellen (varCounter = varCounter + 1). Daarom gebruiken we de variabele varTempCounter.

## Taak 11: 2e Set variable Activity configureren

1. Selecteer in het bovenste menu **Activities -> Set variable**. De Set variable activity wordt toegevoegd aan het ontwerpcanvas.

2. Selecteer met de **Set variable activity** geselecteerd in het onderste deelvenster **General**. Laten we de activiteit een naam en beschrijving geven.

3. Voer in het veld **Name** in: **set_varTempCounter**

4. Voer in het veld **Description** in: **Increment variable varTempCounter**.

5. Klik op het **rode kruisje** van de Dataflow activity naar de nieuwe Set variable activity. Bij mislukking van de dataflowvernieuwing willen we deze Set variable activity uitvoeren.

    ![](../media/Lab_5.36.png)
 
6. Selecteer met de **Set variable activity** geselecteerd, **Settings** in het onderste menu.

7. Zorg er in het onderste deelvenster voor dat **Variable type** is ingesteld op **Pipeline variable**.

8. Selecteer in het veld **Name** **varTempCounter**. Dit is de variabele waarvan we de waarde gaan instellen.

9. Selecteer in het veld **Value** het **tekstvak**. Selecteer de koppeling **Add dynamic content**.

10. Het dialoogvenster Pipeline expression builder opent. Voer in: **@add(variables('varCounter'),1)**

    >**Opmerking**: Je kunt deze expressie zelf intypen, het menu gebruiken om de functies te selecteren, of deze kopiëren en plakken. 

    >**Opmerking**: Deze functie stelt de waarde van de variabele varTempCounter in op de waarde van de variabele varCounter plus één (varTempCounter = varCounter + 1).

    ![](../media/Lab_5.37.png)
 
Nu moeten we de waarde van de variabele varCounter instellen op de waarde van varTempCounter. 

## Taak 12: 3e Set variable Activity configureren

1. Selecteer in het bovenste menu **Activities -> Set variable**. De Set variable activity wordt toegevoegd aan het ontwerpcanvas.

2. Selecteer met de **Set variable activity** geselecteerd in het onderste deelvenster **General**. Laten we de activiteit een naam en beschrijving geven.

3. Voer in het veld **Name** in: **set_varCounter**

4. Voer in het veld **Description** in: **Increment variable varCounter**.

5. Klik op het **groene vinkje** van de Set variable activity set_varTempCounter en sleep dit naar de nieuwe **Set variable activity set_varCounter**. 

    ![](../media/Lab_5.38.png)
 
6. Selecteer met de **Set variable activity set_varCounter** geselecteerd, **Settings** in het onderste menu.

7. Zorg er in het onderste deelvenster voor dat **Variable type** is ingesteld op **Pipeline variable**.

8. Selecteer in het veld **Name** **varCounter**. Dit is de variabele waarvan we de waarde gaan instellen.

9. Selecteer in het veld **Value** het **tekstvak**. Selecteer de koppeling **Add dynamic content**.

10. Het dialoogvenster Pipeline expression builder opent. Voer in: **@variables('varTempCounter')**. Je kunt deze expressie zelf intypen, het menu gebruiken om de functies te selecteren, of deze kopiëren en plakken.

    >**Opmerking**: Deze functie stelt de waarde van de variabele varCounter in op de waarde van de variabele varTempCounter (varCounter = varTempCounter). Aan het einde van elke iteratie hebben zowel varCounter als varTempCounter dezelfde waarde.
 
    ![](../media/Lab_5.39.png)

## Taak 13: Wait Activity configureren

Vervolgens moeten we 5 minuten/300 seconden wachten als de dataflowvernieuwing de eerste keer mislukt voordat we het opnieuw proberen. Als de dataflowvernieuwing de tweede keer mislukt, moeten we 15 minuten/900 seconden wachten en het opnieuw proberen. We gaan de Wait activity en de variabele varWaitTime gebruiken om de wachttijd in te stellen.

1. Selecteer in het bovenste menu **Activities -> ellipsis (…) -> Wait**. De Wait activity wordt toegevoegd aan het ontwerpcanvas.

2. Selecteer met de **Wait activity** geselecteerd in het onderste deelvenster **General**. Laten we de activiteit een naam en beschrijving geven.

3. Voer in het veld **Name** in: **wait_onFailure**

4. Voer in het veld **Description** in: **Wait for 300 seconds on 2nd try and 900 seconds on 3rd try**.

5. Klik op het **groene vinkje** van de Set variable activity set_varCounter en sleep dit naar de nieuwe **Wait activity wait_onFailure**. 

    ![](../media/Lab_5.40.png)
 
6. Selecteer met de **Wait activity** geselecteerd, **Settings** in het onderste menu.

7. Selecteer in het veld **Wait time in seconds** het **tekstvak** en selecteer de koppeling **Add dynamic content**.

8. Het dialoogvenster Pipeline expression builder opent. Voer het volgende in: 

    ```
            @if(
                greater(variables('varCounter'), 1),
                if(equals(variables('varCounter'), 2),
                    mul(variables('varWaitTime'),15 ), 
                    mul(variables('varWaitTime'), 0)
                ),
                mul(variables('varWaitTime'),5 )
            )
    ```

    Je kunt deze expressie zelf intypen, het menu gebruiken om de functies te selecteren, of deze kopiëren en plakken. 

    ![](../media/Lab_5.41.png)

We gebruiken hier twee nieuwe functies:

- **greater**: Neemt twee getallen als parameters en vergelijkt welk getal groter is.

- **mul**: Dit is een vermenigvuldigingsfunctie die twee parameters neemt om te vermenigvuldigen. 

De expressie is een geneste if-instructie. Er wordt gecontroleerd of de waarde van de variabele varCounter groter is dan 1. Als dat het geval is, wordt gecontroleerd of de waarde van de variabele varCounter 2 is. Als dat het geval is, wordt de wachttijd ingesteld op varWaitTime maal 15. Onthoud dat we de standaardwaarde van varWaitTime op 60 hebben ingesteld. Dat zou 60*15 = 900 seconden zijn. Als de waarde van de variabele varCounter niet 2 is (maar groter dan 2, wat betekent dat de dataflowvernieuwing 3 keer is mislukt en we klaar zijn met itereren; we hoeven niet meer te wachten), wordt de wachttijd ingesteld op varWaitTime * 0. Dus op 0. Als de waarde van de variabele varCounter 1 is, vermenigvuldigen we varWaitTime * 5. Dat zou 60*5 = 300 seconden zijn.

9. Selecteer **OK**. 

    **Controlepunt**: Je Until Iterator moet eruitzien als de schermafbeelding hieronder.
 
    ![](../media/Lab_5.42.png)

10. Selecteer linksboven in het ontwerpcanvas **pl_Refresh_People_Sharepoint_Option2** om uit de Until-iterator te navigeren. 

    ![](../media/Lab_5.43.png)
 
11. We zijn klaar met het aanmaken van de data pipeline. Selecteer in het bovenste menu **Home -> Save** om de data pipeline op te slaan.
  
    ![](../media/Lab_5.44.png)

## Taak 14: Geplande vernieuwing configureren voor Data Pipeline

1. We kunnen de data pipeline testen door **Home -> Run** te selecteren. 

    >**Opmerking**: Het kan een paar minuten duren voordat de data pipeline de vernieuwing heeft voltooid. Dit is een trainingsomgeving, dus het bestand in SharePoint is altijd beschikbaar. Hierdoor zal je data pipeline nooit mislukken.

2. We kunnen de data pipeline instellen om op een schema te worden uitgevoerd. Selecteer in het bovenste menu **Home -> Schedule**. Het dialoogvenster Schedule opent.

3. Stel de radioknop **Scheduled run** in op **On**.

4. Stel de **Repeat dropdown** in op **Daily**.

5. Stel **Time** in op **9 AM**.

6. Stel **Start date and time** in op **Today**.

7. Stel de End date and time in op een datum in de toekomst.

8. Stel je **Time zone** in.

    >**Opmerking**: Omdat dit een labomgeving is, kun je de tijdzone instellen op je voorkeurstijdzone. In een echte situatie stel je de tijdzone in op basis van jouw locatie of de locatie van de databron.

9. Selecteer **Apply**.

10. Selecteer het **X**-pictogram rechtsbovenin het dialoogvenster om het te sluiten.

    ![](../media/Lab_5.45.png)
 
11. Selecteer je Fabric workspace **FAIAD_<username>** in het linkerdeelvenster om naar de workspace te navigeren.

    >**Opmerking**: In het scherm Schedule is er geen optie om meldingen te sturen bij succes of mislukking (zoals bij Dataflow Schedule). Meldingen kunnen worden verzonden door een activiteit toe te voegen in de Data Pipeline. We doen dit niet in dit lab omdat het een labomgeving betreft.

We hebben vernieuwingsschema's ingesteld voor de verschillende databronnen. In het volgende lab gaan we relaties, metingen en andere modelleringsactiviteiten uitvoeren.

# Referenties
Fabric Analyst in a Day (FAIAD) introduceert je aan een aantal van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service bevat het gedeelte Help (?) koppelingen naar uitstekende resources.

   ![](../media/img18.png) 
 
Hier zijn nog enkele resources die je helpen met je volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige aankondiging van [Microsoft Fabric GA](https://aka.ms/Fabric-Hero-Blog-Ignite23)
- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)
- Meld je aan voor de [gratis proefperiode van Microsoft Fabric](https://aka.ms/try-fabric)
- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)
- Leer nieuwe vaardigheden door de [Fabric Learning modules](https://aka.ms/learn-fabric) te verkennen
- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)
- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om vragen te stellen, feedback te delen en van anderen te leren

Lees de meer gedetailleerde aankondigingsblogs over Fabric-ervaringen:

- [Data Factory-ervaring in Fabric blog](https://aka.ms/Fabric-Data-Factory-Blog) 
- [Synapse Data Engineering-ervaring in Fabric blog](https://aka.ms/Fabric-DE-Blog) 
- [Synapse Data Science-ervaring in Fabric blog](https://aka.ms/Fabric-DS-Blog) 
- [Synapse Data Warehousing-ervaring in Fabric blog](https://aka.ms/Fabric-DW-Blog) 
- [Synapse Real-Time Analytics-ervaring in Fabric blog](https://aka.ms/Fabric-RTA-Blog)
- [Power BI-aankondigingsblog](https://aka.ms/Fabric-PBI-Blog)
- [Data Activator-ervaring in Fabric blog](https://aka.ms/Fabric-DA-Blog) 
- [Beheer en governance in Fabric blog](https://aka.ms/Fabric-Admin-Gov-Blog)
- [OneLake](https://aka.ms/Fabric-OneLake-Blog)[ in Fabric blog](https://aka.ms/Fabric-OneLake-Blog)
- [Dataverse en Microsoft Fabric-integratie blog](https://aka.ms/Dataverse-Fabric-Blog)

© 2023 Microsoft Corporation. Alle rechten voorbehouden.

Door gebruik te maken van deze demo/dit lab, ga je akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met als doel feedback van je te verkrijgen en je een leerervaring te bieden. Je mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback te geven aan Microsoft. Je mag het niet voor enig ander doel gebruiken. Je mag deze demo/dit lab of een gedeelte daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, er afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN GEDEELTE DAARVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE TEN BEHOEVE VAN VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARE-TECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN IN DEZE DEMO/DIT LAB VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIONALITEIT EN WERKEN MOGELIJK NIET ZOALS EEN DEFINITIEVE VERSIE ZOU WERKEN. WE KUNNEN OOK BESLUITEN EEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN NIET UIT TE BRENGEN. JE ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK ANDERS ZIJN.

**FEEDBACK**. Als je feedback geeft over de technologiefuncties, functionaliteit en/of concepten die in deze demo/dit lab worden beschreven aan Microsoft, geef je Microsoft het recht, kosteloos, om je feedback op welke manier en voor welk doel dan ook te gebruiken, te delen en te commercialiseren. Je geeft ook aan derden, kosteloos, alle octrooirechten die nodig zijn voor hun producten, technologieën en diensten om gebruik te maken van of te communiceren met specifieke onderdelen van een Microsoft-software of -dienst die de feedback bevat. Je geeft geen feedback die onderworpen is aan een licentie die Microsoft verplicht zijn software of documentatie aan derden in licentie te geven omdat we je feedback daarin opnemen. Deze rechten blijven van kracht na beëindiging van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, MET INBEGRIP VAN ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, UITDRUKKELIJK, IMPLICIET OF WETTELIJK, GESCHIKTHEID VOOR EEN BEPAALD DOEL, TITEL EN NIET-INBREUK. MICROSOFT GEEFT GEEN TOEZEGGINGEN OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE OUTPUT DIE VOORTVLOEIT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR ENIG DOEL.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een gedeelte van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen veranderen in toekomstige versies van het product. In deze demo/dit lab leer je over enkele, maar niet alle, nieuwe functies.
