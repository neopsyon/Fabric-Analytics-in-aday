# Microsoft Fabric - Fabric Analyst in a Day - Lab 7

# ![](../media/new11.png)

# Inhoud
   * Introductie

   * Power BI

     * Task 1: Auto-Create Report
         
      * Task 2: Hide default (metrics) tables
         
      * Task 3: Configure background for New report
         
      * Task 4: Add Header to the report
         
      * Task 5: Add KPIs to the report
         
      * Task 6: Add Line chart to the report
         
      * Task 7: Configure Year column in Date table
         
      * Task 8: Configure Short_Month_Name column in Date table
         
      * Task 9: Format Line chart
         
      * Task 10: Add new data to simulate Direct Lake Mode
         
   * Labroomgeving opschonen

   * Referenties

#
# <a name="_toc152166234"></a>**Introductie** 

We hebben gegevens uit verschillende databronnen in de Lakehouse geladen, kennis gemaakt met Lakehouse, een datamodel aangemaakt en een verversingsschema ingesteld voor de databronnen. Nu gaan we een rapport aanmaken.

Aan het einde van dit lab heb je het volgende geleerd: 

- Hoe je automatisch een rapport aanmaakt
- Hoe je een rapport opbouwt vanuit een leeg canvas
- Hoe je Direct Lake mode ervaart, waarbij gegevens automatisch worden bijgewerkt

# <a name="_toc152166235"></a>**Power BI**

### <a name="_toc152166236"></a>Task 1: Auto-Create Report

Laten we beginnen met de auto-create report optie. Later in het lab zullen we het rapport dat we in Power BI hebben, opnieuw aanmaken.

1. Navigeer terug naar de **Fabric workspace** die je in het eerdere lab hebt aangemaakt.
1. Je bevindt je waarschijnlijk op de Data Factory-startpagina. Selecteer onderin het linkerdeelvenster het **Data Factory-pictogram**.
1. Het Fabric experience-dialoogvenster opent. Selecteer **Power BI**. Je wordt doorgestuurd naar de **Power BI Home page**.

      ![A screenshot of Microsoft Fabric experiences dialog](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.002.png)

1. Selecteer **+ New Report** in het bovenste menu.

      ![A screenshot of Power BI home](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.003.png)

1. Je wordt doorgestuurd naar het scherm **Build your first report**. Er zijn opties om handmatig gegevens in te voeren en een rapport te bouwen, of om een gepubliceerd semantisch model te kiezen. We hebben in de vorige labs een semantisch model aangemaakt. Laten we dat gebruiken. Selecteer de optie **Pick a published semantic model**.

      ![A screenshot of build first report screen](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.004.png)

1. De pagina Pick a dataset to use in your report opent. Let op dat er vier opties zijn. **Selecteer lh_FAIAD**:
   1. **lh_FAIAD:** Dit is de lakehouse met de dataset die we hebben aangemaakt en willen gebruiken voor het rapport.
   1. **Units by Supplier:** Dit is de dataset die we hebben aangemaakt met T-SQL.
   1. **DataflowsStagingWarehouse:** Dit is het staging warehouse dat standaard wordt aangemaakt omdat we dit niet hebben gebruikt, aangezien we geen data hebben gestaged.
   1. **DataflowsStagingLakehouse:** Dit is de staging lakehouse die standaard wordt aangemaakt omdat we dit niet hebben gebruikt, aangezien we geen data hebben gestaged.

1. Klik op de **pijl naast de Auto-create report knop**. Let op dat er twee opties zijn: Auto-create report en Create a blank report. Laten we automatisch aanmaken proberen; selecteer **Auto-create report**.

      ![A screenshot of a pick a dataset to use in your report screen](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.005.png)

1. Power BI begint het rapport automatisch aan te maken. Let op dat er een optie is om gegevens vooraf te selecteren via Pre-select data. Zodra het rapport gereed is, verschijnt er een dialoogvenster rechtsboven in het scherm. Selecteer **View report now**.

      ![A screenshot of auto-create ready success dialog](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.006.png)

      **Checkpoint:** Je hebt nu een rapport dat eruitziet zoals de onderstaande schermafbeelding. Er zijn een aantal KPI's en trendvisuals. Dit is een goed startpunt als je een nieuw model analyseert en snel op gang wilt komen.
      
      **Opmerking:** Let op dat je in het bovenste menu de mogelijkheid hebt om het rapport te bewerken via Edit of om een deel van de gegevens als tabellen te bekijken. Verken deze opties gerust.

1. Als je klaar bent, **vouw** je alle tabellen in de **Data** sectie rechts in. Let op dat er vijf nieuwe tabellen zijn die geen onderdeel zijn van het model dat we hebben aangemaakt. Dit zijn standaardtabellen die zijn toegevoegd om prestatie-analyse te ondersteunen. We verwijderen deze binnenkort uit de rapportweergave.
1. Laten we dit rapport opslaan. Selecteer **Save** in het bovenste menu.
1. Het dialoogvenster Save your report opent. Geef het rapport de naam **rpt\_Sales\_Auto\_Report**.

   >**Opmerking:** We gebruiken het voorvoegsel rpt voor de rapportnaam, wat een afkorting is voor report.

1. Zorg ervoor dat het rapport wordt opgeslagen in **Fabric_username.**
1. Selecteer **Save.**

      ![A screenshot of auto-created report](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.007.png)

### <a name="_toc152166237"></a>Task 2: Hide default (metrics) tables

Laten we een rapport aanmaken dat lijkt op het rapport dat we in Power BI Desktop hebben. We doen dit door te beginnen met een leeg canvas. Voordat we beginnen met het aanmaken van een rapport, verwijderen we de standaardtabellen (zie schermafbeelding hierboven) uit de rapportweergave. Dit wordt gedaan in de modelleringssectie van de Lakehouse.

1. Selecteer onderin het linkerdeelvenster het **Power BI-pictogram**. Het Fabric-dialoogvenster opent.
2. Selecteer **Data Engineering**. Je wordt doorgestuurd naar de Data Engineering-startpagina.

      ![A screenshot of Microsoft Fabric experiences dialog](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.008.png)

3. Scroll omlaag naar de sectie **Quick Access**.
4. Selecteer **lh_FAIAD -> SQL analytics endpoint**. Je bevindt je nu in de Data-weergave van de Lakehouse.
5. Selecteer onderin het **linkerdeelvenster** **Model** om naar de Model-weergave te navigeren.

    Let op het ontwerpcanvas; je vindt daar de standaardtabellen. (Mogelijk moet je naar rechts of omlaag scrollen om ze te zien.)

     ![A screenshot of Lakehouse model view](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.009.png)

6. Klik met de rechtermuisknop op de tabel **long_running_queries** en selecteer **Hide in report view**.

      ![A screenshot of Lakehouse model view showing hide in report view](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.010.png)

7. Selecteer op vergelijkbare wijze **Hide in report view** voor de volgende tabellen:
   
   1. exec_requests_history
   1. frequently_run_queries

### <a name="_toc152166238"></a>Task 3: Configure background for a New report

1. We kunnen een nieuw rapport aanmaken vanuit de modelweergave. Selecteer in het bovenste menu **Home -> New report**. Je wordt doorgestuurd naar het Power BI-rapportcanvas in een nieuw venster/tabblad in je browser.

      ![A screenshot showing selecting New Report](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.011.png)

1. Als je dit nog niet hebt gedaan, open dan **FAIAD.pbix** in de map **Report** op het **bureaublad** van je labomgeving. 

    We gaan dit rapport als referentie gebruiken. We beginnen met het toevoegen van de canvasachtergrond. We maken de rapportheader aan, voegen een aantal KPI's toe en maken de Sales over time-lijngrafiek. In het belang van de tijd en in de wetenschap dat je ervaring hebt met het bouwen van visuals in Power BI Desktop, zullen we niet alle visuals aanmaken. 
      
     ![A screenshot of a Power BI Desktop report](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.012.png)

1. Navigeer terug naar het **Power BI canvas** in je browser.
1. Selecteer het **Format page** **pictogram** in het Visualization-deelvenster.
1. Vouw de sectie **Canvas background** uit.
1. Selecteer **Browse** bij de optie **Image**. Het bestandsverkenner-dialoogvenster opent.
1. Navigeer naar de map **Report** op het **bureaublad** van je labomgeving. 
1. Selecteer **Summary Background.png.**
1. Stel de **Image fit**-vervolgkeuzelijst in op **Fit**.
1. Stel Transparency in op **0%**.

     ![A screenshot of new blank report](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.013.png)

### <a name="_toc152166239"></a><a name="_hlk152165928"></a>Task 4: Add Header to the report

1. Laten we de header toevoegen in de bovenste marge. Selecteer in het **menu** de optie **Text box**.
1. Voer **Fabrikam Company** in als de eerste regel in het tekstvak.
1. Voer **Sales Report** in als de tweede regel in het tekstvak.
1. Markeer **Fabrikam Company** en stel **Font** in op **Segoe UI** en **fontgrootte** op **18, bold**.
1. Markeer **Sales Report** en stel **Font** in op **Segoe UI** en **fontgrootte** op **14**.
1. Met het **tekstvak geselecteerd**, vouw je in het Format-deelvenster rechts **Effects** uit.
1. Gebruik de **Background**-schuifregelaar om deze in te stellen op **Off**.
1. Vergroot of verklein het **tekstvak zodat het in de bovenste marge past**.

     ![A screenshot Text box visual for Fabrikam](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.014.png)

### <a name="_toc152166240"></a>Task 5: Add KPIs to the report

1. Laten we de Sales-KPI toevoegen. Selecteer de **witte ruimte** op het canvas om de focus van het tekstvak weg te halen.
1. Selecteer in de sectie **Visualizations** de **Multi-row card visual**.
1. Vouw in de **Data section** de tabel **Sales** uit.
1. Selecteer de **Sales**-meting.

     ![A screenshot of multi-row card visual ](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.015.png)

1. Selecteer met de **multi-row card visual geselecteerd** het **Format visual** **pictogram** in de sectie Visualizations.
1. Vouw de sectie **Category labels** uit.
1. Vergroot de **fontgrootte** naar **14**.
1. Selecteer de **Color drop down**. Het kleurenpalet-dialoogvenster opent.
1. Stel de Hex-waarde in op **#004753**.

     ![A screenshot of multi-row card visual formatting](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.016.png)

1. Vouw de sectie **Cards** uit.
1. Gebruik de **Accent bar**-schuifregelaar om deze in te stellen op **Off**.

     ![A screenshot of multi-row card visual formatting](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.017.png)

1. Selecteer **General** in het Visualizations-deelvenster.
1. Vouw de sectie **Effects** uit.
1. Gebruik de **Background**-schuifregelaar om deze in te stellen op **Off**.
1. Vergroot of verklein de **visual** en verplaats deze naar de **linker box zoals weergegeven in de schermafbeelding**.

     ![A screenshot of multi-row card visual formatting](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.018.png)

1. Laten we nog een KPI toevoegen. Selecteer de **Sales multi-row card** die we zojuist hebben aangemaakt. **Kopieer** de visual door op **Ctrl+C** op je toetsenbord te drukken.
1. **Plak** de visual door op **Ctrl+V** op je toetsenbord te drukken. De visual wordt op het canvas geplakt.
1. Verwijder met de **nieuwe visual gemarkeerd** in het **Visualization-deelvenster -> Build visual -> Fields** sectie de **Sales**-meting.
1. Vouw in de sectie **Data** de tabel Sales uit en selecteer de meting **Units**.
1. Vergroot of verklein de **visual** en **plaats deze in de box onder de Sales-visual**.

     ![A screenshot of multi-row card visual copy and pasted for Units measure](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.019.png)

### <a name="_toc152166241"></a>Task 6: Add Line chart to the report

Laten we een lijngrafiek aanmaken om de Sales over tijd per Reseller Company te visualiseren.

1. Selecteer de **witte ruimte** op het canvas om de focus van de multi-row card visual weg te halen.
1. Selecteer in de sectie **Visualizations** de **Line chart**.
1. Vouw in de sectie **Data** de tabel **Date** uit.
1. Selecteer het veld **Year**. Let op dat Year standaard wordt opgeteld en aan de Y-axis wordt toegevoegd. Laten we dit corrigeren.

     ![A screenshot of line chart visual configuration](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.020.png) 

### <a name="_toc152166242"></a>Task 7: Configure Year column in Date table

1. Navigeer naar het browsertabblad met de **modelweergave van de Lakehouse**.
1. Vouw vanuit het linker Explorer pane **lhFAIAD -> Schemas -> dbo -> Tables -> Date** uit.
1. Selecteer de kolom **Year**.
1. Vouw in het **Properties**-deelvenster rechts de sectie **Advanced** uit.
1. Selecteer in de vervolgkeuzelijst **Summarize by** de optie **None**.

     ![A screenshot of modeling in Lakehouse](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.021.png)

1. Navigeer terug naar het browsertabblad met het **Power BI canvas**.
1. Selecteer **Refresh** in het bovenste menu. Let op dat Year nu geen optellingsveld meer is. 
1. Verwijder met de **Line chart visual geselecteerd** **Sum of Year** van de Y-axis.
1. Selecteer het veld **Year**; het wordt aan de **X-axis** toegevoegd.
1. Vouw de tabel **Sales** uit en selecteer de meting **Sales**.

     ![A screenshot of line chart visual configuration](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.022.png)

### <a name="_toc152166243"></a>Task 8: Configure Short_Month_Name column in Date table

1. Laten we een maand aan deze grafiek toevoegen. Sleep vanuit de Date-tabel het veld **Short_Month_Name** onder **Year** op de **X-axis**. Let op dat de visual gesorteerd is op Sales. Laten we sorteren op Short_Month_Name.
1. Selecteer de **ellipsis (…)** rechtsboven in de visual.
1. Selecteer **Sort axis -> Year Short_Month_Name**.
1. Selecteer de **ellipsis (…)** rechtsboven in de visual.
1. Selecteer **Sort axis -> Sort ascending**.

     ![A screenshot of line chart visual configuration](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.023.png)

     **Opmerking:** De maanden zijn alfabetisch gesorteerd. Laten we dit corrigeren.

      ![A screenshot of line chart visual ](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.024.png)

1. Navigeer naar het browsertabblad met de **modelweergave van de Lakehouse**.
1. Vouw vanuit het linker Explorer pane **lhFAIAD -> Schemas -> dbo -> Tables -> Date** uit.
1. Selecteer de kolom **Short_Month_Name**.
1. Vouw in het **Properties**-deelvenster rechts de sectie **Advanced** uit.
1. Selecteer in de vervolgkeuzelijst **Sort by column** de optie **Month**.

     ![A screenshot of Lakehouse modeling setting sort by column](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.025.png)

1. Navigeer terug naar het browsertabblad met het **Power BI canvas**.
1. Selecteer **Refresh** in het bovenste menu. Let op dat de maanden nu correct gesorteerd zijn.

     ![A screenshot of line chart visual ](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.026.png) 

### <a name="_toc152166244"></a>Task 9: Format Line chart

Let op hoe eenvoudig het is om het semantisch model bij te werken terwijl je rapporten bouwt. Dit biedt een naadloze interactie vergelijkbaar met Power BI Desktop.

1. Vouw met de **Line chart visual geselecteerd** in de sectie **Data** de tabel **Reseller** uit.
1. Sleep het veld **Reseller -> Reseller Company** naar de sectie **Legend**.

      ![A screenshot of adding Reseller Company field to Legend section](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.027.png)

1. Selecteer met de **Line chart visual geselecteerd** in de sectie **Visualization** het **Format visual pictogram -> General**.
1. Vouw de sectie **Title** uit.
1. Stel de tekst van **Title** in op **Sales over time**.
1. Vouw de sectie **Effects** uit.
1. Gebruik de **Background**-schuifregelaar om deze in te stellen op **Off**.

     ![A screenshot of Line chart visual formatting](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.028.png)

1. Selecteer in de sectie **Visualization** het **Format visual pictogram -> Visual**.
1. Vouw de sectie **X-axis** uit.
1. Gebruik de **Title**-schuifregelaar om deze in te stellen op **Off**.
1. Vouw de sectie **Lines** uit.
1. Vouw de sectie **Colors** uit.
1. Stel de kleur van **Wingtip Toys** in op **#004753**.
1. Stel de kleur van **Tailspin Toys** in op **#F17925**.
1. Vergroot of verklein de **visual** en verplaats deze naar de **rechter box bovenaan zoals weergegeven in de schermafbeelding**.
1. Scroll naar rechts op de visual en **let op dat we gegevens hebben tot en met april 2023**.

     ![A screenshot of Line chart visual formatting](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.029.png)

1. Laten we het rapport opslaan; selecteer in het menu **File -> Save**.
1. Het dialoogvenster Save your report opent. Geef het rapport de naam **rpt_Sales_Report**.

     **Opmerking:** We gebruiken het voorvoegsel rpt voor de rapportnaam, wat een afkorting is voor report.
   
1. Zorg ervoor dat het rapport is opgeslagen in **your workspace name**.
1. Selecteer **Save**.

     ![A screenshot of report saving](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.030.png)

Zoals eerder vermeld, zullen we in dit lab niet alle visuals bouwen. Bouw gerust meer visuals op een moment dat het jou uitkomt. 

### <a name="_toc152166245"></a>Task 10: Add new data to simulate Direct Lake Mode

Normaal gesproken moet in Import mode, nadat de gegevens in de bron zijn bijgewerkt, het Power BI-model worden vernieuwd, waarna de gegevens in het rapport worden bijgewerkt. In Direct Query mode zijn gegevens zodra ze in de bron zijn bijgewerkt beschikbaar in het Power BI-rapport. Direct query mode is echter doorgaans traag. Om dit probleem op te lossen heeft Microsoft Fabric Direct Lake mode geïntroduceerd. Direct Lake is een snelle route om gegevens rechtstreeks vanuit het lake in de Power BI-engine te laden, klaar voor analyse. Laten we dit verkennen.

In een realistische situatie worden gegevens bijgewerkt bij de bron. Omdat we in een trainingsomgeving werken, simuleren we dit door een verbinding te maken met een parquet-bestand met gegevens voor mei 2023. 

1. Navigeer naar het browsertabblad met de **modelweergave van de Lakehouse**.
1. Selecteer **your workspace name** in het linkerdeelvenster.
1. Selecteer **df_Sales_ADFS** zodat we de dataflow kunnen bewerken door het nieuwe Parquet-bestand toe te voegen.

     ![A screenshot of Data factory home](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.031.png)

1. Als je dit nog niet hebt gedaan, open dan **FAIAD.pbix** in de map **Report** op het **bureaublad** van je labomgeving. 
1. Selecteer in het lint **Home -> Transform data**. Het Power Query-venster opent.
1. Selecteer in het linkerdeelvenster, onder de map **DirectLake**, de query **MayInvoice**.
1. **Klik met de rechtermuisknop** en selecteer **Copy**. 

      ![A screenshot of Power BI Desktop, Power Query](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.032.png)

1. Navigeer terug naar het **Dataflow-scherm** in de browser.
1. Voer in het Dataflow-deelvenster **Ctrl+V** in (rechtermuisklik Paste wordt momenteel niet ondersteund).

   Laten we nu de verwijzing naar ADLS Base Folder (2) verwijderen en ADLS Base Folder gebruiken.

1. Selecteer de query **MayInvoice**.
1. Selecteer in het rechterdeelvenster onder **Applied Steps** de stap **Source**.
1. Wijzig in de formulebalk **#"ADLS Base Folder (2)"** naar **#"ADLS Base Folder"**
1. Selecteer het **vinkje** naast de formulebalk of druk op Enter.

     ![A screenshot of dataflow](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.033.png)

1. Klik in het linkerdeelvenster onder de sectie Queries **met de rechtermuisknop op de query ADLS Base Folder (2)** en selecteer **Delete**.
1. Het dialoogvenster Delete query verschijnt. Selecteer **Delete** ter bevestiging.

     ![A screenshot dataflow showing deletion of ADLS Base Folder (2)](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.034.png)

1. Laten we nu de factuurgegevens van mei toevoegen aan de Invoice-tabel. Selecteer de query **Invoice** in de Queries-sectie.
1. Selecteer in het lint **Home -> Append** queries.
1. Het dialoogvenster Append query verschijnt. Selecteer in de vervolgkeuzelijst **Table to append** de optie **MayInvoice**.
1. Selecteer **OK**.

     ![A screenshot of append query](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.035.png)

1. Selecteer **Publish** rechtsonder in de hoek om de wijzigingen op te slaan en te publiceren. 

     ![A screenshot of Publish dataflow](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.036.png)

   **Opmerking:** Zodra de dataflow is gepubliceerd, wordt deze vernieuwd. Dit kan enkele minuten duren.

1. Navigeer terug naar het browsertabblad met het **Power BI canvas**.
1. Selecteer **Refresh** in het bovenste menu. Let op dat er in de Line chart nu gegevens zijn voor mei 2023. Let ook op dat het Sales-bedrag is gestegen.

     ![A screenshot of data refreshed in the report](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.037.png)

Naarmate elke dataflow die we in eerdere labs hebben aangemaakt volgens schema wordt vernieuwd, worden gegevens in de Lakehouse geladen. Het datamodel in de Lakehouse wordt bijgewerkt en de rapporten worden vernieuwd. We hoeven het datamodel en het rapport niet handmatig te vernieuwen telkens wanneer een van de dataflows wordt vernieuwd. Dit is het voordeel van Direct Lake.

Laten we de uitdagingen bekijken die in de probleemstelling worden vermeld:

- **Je moet je dataset minimaal drie keer per dag vernieuwen om de verschillende updatetijden van de verschillende databronnen bij te houden**.

  We hebben dit opgelost met Direct Lake. Elke dataflow wordt vernieuwd volgens zijn eigen schema. De dataset en het rapport hoeven niet te worden vernieuwd.

- **Je vernieuwingen duren lang, omdat je elke keer een volledige vernieuwing moet uitvoeren om eventuele updates in de bronsystemen te verwerken**.

  Ook dit hebben we opgelost met Direct Lake. Elke dataflow wordt vernieuwd volgens zijn eigen schema. De dataset en het rapport hoeven niet te worden vernieuwd, dus we hoeven ons geen zorgen te maken over een volledige vernieuwing. 

- **Fouten in een van de databronnen waaruit je gegevens haalt, zorgen ervoor dat de vernieuwing van je dataset mislukt. Vaak wordt het medewerkersbestand niet op tijd geüpload, waardoor de vernieuwing van je dataset mislukt**. 

  Data Pipeline helpt dit probleem op te lossen door de mogelijkheid te bieden om vernieuwingen bij mislukking opnieuw te proberen en op verschillende intervallen.

- **Het kost erg veel tijd om wijzigingen in je datamodel aan te brengen, omdat Power Query lang nodig heeft om je previews te vernieuwen vanwege de grote hoeveelheid gegevens en complexe transformaties**. 

  We hebben gemerkt dat Data Flows efficiënt zijn en dat wijzigingen eenvoudig kunnen worden aangebracht. Doorgaans duurt het niet lang voordat previews in Data Flows worden geladen.

- **Je hebt een Windows-pc nodig om Power BI Desktop te gebruiken, terwijl de bedrijfsstandaard Mac is**.

  Microsoft Fabric is een SaaS-oplossing. We hebben alleen een browser nodig om de service te raadplegen. We hoeven geen software op onze desktops te installeren.

# <a name="_toc152166246"></a>**Labroomgeving opschonen**

Als je klaar bent om de labomgeving op te schonen, volg dan de onderstaande stappen.

1. Navigeer terug naar het browsertabblad met het **Power BI canvas**. **Sluit dit tabblad**.
1. Navigeer naar het tabblad met de **modelweergave van de** **Lakehouse**.
1. Selecteer **your workspace name** in het linkerdeelvenster om naar de startpagina te navigeren.

     ![A screenshot to select your workspace](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.038.png)

1. Selecteer in het bovenste menu de **ellipsis (…)** naast Manage access en selecteer **Workspace settings**.

     ![A screenshot to select Workspace settings](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.039.png)

1. Het dialoogvenster Workspace settings opent. Ga naar de sectie **General** in het linkermenu.
1. Scroll omlaag om de optie **Remove this workspace** te zien.
1. Het dialoogvenster Delete workspace opent. Selecteer **Delete**.

Hiermee wordt de workspace en alle items die daarin zijn opgeslagen verwijderd.

   ![A screenshot of Workspace settings dialog](../media/L7CleanupS5.png)

# <a name="_toc150777627"></a><a name="_toc150779083"></a><a name="_toc152166247"></a>**Referenties**

Fabric Analyst in a Day (FAIAD) maakt je vertrouwd met een aantal van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service bevat de Help-sectie (?) links naar een aantal uitstekende bronnen.

   ![A screenshot of help options](../media/Aspose.Words.e28fdc47-8e4b-4442-9628-9e34dc2360ff.041.png)

Hieronder vind je nog enkele aanvullende bronnen die je helpen bij je volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [Microsoft Fabric GA-aankondiging](https://aka.ms/Fabric-Hero-Blog-Ignite23)
- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)
- Meld je aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)
- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)
- Leer nieuwe vaardigheden door de [Fabric Learning-modules](https://aka.ms/learn-fabric) te verkennen
- Raadpleeg de [technische documentatie van Fabric](https://aka.ms/fabric-docs)
- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om vragen te stellen, feedback te delen en van anderen te leren

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

© 2023 Microsoft Corporation. All rights reserved.

Door gebruik te maken van deze demo/dit lab ga je akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met als doel feedback van je te ontvangen en je een leerervaring te bieden. Je mag de demo/het lab uitsluitend gebruiken om dergelijke technologische functies en functionaliteit te evalueren en feedback aan Microsoft te geven. Je mag de demo/het lab niet voor enig ander doel gebruiken. Je mag deze demo/dit lab of een deel daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, licentiëren, er afgeleide werken van maken, overdragen of verkopen.

KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN DEEL DAARVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE TEN BEHOEVE VAN VERDERE REPRODUCTIE OF VERSPREIDING IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARE-TECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, WAARONDER MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF INRICHTING VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN GEPRESENTEERD, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DE MANIER WAAROP EEN DEFINITIEVE VERSIE ZAL WERKEN. HET IS OOK MOGELIJK DAT WIJ GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UITBRENGEN. JE ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK ANDERS ZIJN.

**FEEDBACK**. Als je feedback geeft over de technologische functies, functionaliteit en/of concepten die in deze demo/dit lab worden beschreven aan Microsoft, geef je Microsoft kosteloos het recht om je feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, te delen en te commercialiseren. Je geeft ook aan derden kosteloos alle octrooirechten die nodig zijn voor hun producten, technologieën en diensten om gebruik te maken van of een interface te bieden met specifieke onderdelen van Microsoft-software of -diensten die de feedback bevatten. Je geeft geen feedback die onderworpen is aan een licentie die Microsoft verplicht zijn software of documentatie aan derden in licentie te geven omdat wij je feedback daarin opnemen. Deze rechten blijven van kracht na beëindiging van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN AF MET BETREKKING TOT DE DEMO/HET LAB, INCLUSIEF ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, HETZIJ UITDRUKKELIJK, IMPLICIET OF WETTELIJK, GESCHIKTHEID VOOR EEN BEPAALD DOEL, TITEL EN NIET-INBREUK. MICROSOFT GEEFT GEEN GARANTIES OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE UITVOER DIE VOORTVLOEIT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR WELK DOEL DAN OOK.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen veranderen in toekomstige versies van het product. In deze demo/dit lab leer je over een aantal, maar niet alle, nieuwe functies.
Version: 11.15.2023                                Copyright 2023 Microsoft   	                                                         29|Page 

Maintained by:  Microsoft Corporation 
