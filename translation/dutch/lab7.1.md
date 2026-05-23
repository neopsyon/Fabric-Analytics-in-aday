# Microsoft Fabric - Fabric Analyst in a Day - Lab 7

# ![](../media/Lab_7.1.png)


# Inhoud
* Introductie

* Power BI

    * Task 1: Auto-Create Report

    * Task 2: Configure background for a New report

    * Task 3: Add Header to the report	

    * Task 4: Add KPIs to the report	

    * Task 5: Add Line chart to the report

    * Task 6: Save the report	

    * Task 7: Configure Year column in Date table

    * Task 8: Configure Short_Month_Name column in Date table

    * Task 9: Format Line chart	

    * Task 10: Add new data to simulate Direct Lake Mode

* Labopdracht opschonen

* Referenties

#
# <a name="_toc152166234"></a>**Introductie** 

We hebben data uit verschillende databronnen in de Lakehouse geladen, kennisgemaakt met Lakehouse, een vernieuwingsschema voor de databronnen ingesteld en een datamodel aangemaakt. Nu gaan we een rapport maken.

Aan het einde van dit lab heb je geleerd:
-	Hoe je automatisch een rapport kunt laten aanmaken
-	Hoe je een rapport opbouwt vanuit een leeg canvas
-	Hoe je Direct Lake mode ervaart, waarbij data automatisch wordt vernieuwd

# <a name="_toc152166235"></a>**Power BI**

### <a name="_toc152166236"></a>Task 1: Auto-Create Report

Laten we beginnen met de optie om het rapport automatisch te laten aanmaken. Later in het lab zullen we het rapport dat we in Power BI hebben opnieuw aanmaken.

1. Navigeer terug naar de **Fabric workspace** die je in het eerdere lab hebt aangemaakt.
2. Selecteer onderaan het linkerdeelvenster het pictogram **Fabric experience selector**.
3. Het dialoogvenster Fabric experience opent. Selecteer **Power BI**. Je wordt doorgestuurd naar de **Power BI Home page**.

    ![](../media/Lab_7.2.png)
 
4. Selecteer **New Report** in het bovenste menu.

    ![](../media/Lab_7.3.png)

5. Je wordt doorgestuurd naar het scherm **Build your first report**. Er zijn opties om handmatig data in te voeren en een rapport te maken, of om een gepubliceerd semantisch model te kiezen. We hebben in de vorige labs een semantisch model aangemaakt. Laten we dat gebruiken. Selecteer de optie **Pick a published semantic model**.

    ![](../media/faiadlab2-7.png)
 
6. De pagina Pick a dataset to use in your report opent. Let op: we hebben vier opties. **Selecteer lh_FAIAD:**
a.	**lh_FAIAD:** Dit is de lakehouse met de dataset die we hebben aangemaakt en willen gebruiken voor het rapport.
b.	**Units by Supplier:** Dit is de dataset die we hebben aangemaakt met T-SQL.
c.	**DataflowsStagingWarehouse:** Dit is het staging warehouse dat standaard wordt aangemaakt. We hebben dit niet gebruikt omdat we geen data hebben gestaged.
d.	**DataflowsStagingLakehouse:** Dit is de staging lakehouse die standaard wordt aangemaakt. We hebben dit niet gebruikt omdat we geen data hebben gestaged.
7. Klik op de **pijl naast de Auto-create report-knop**. Let op: er zijn twee opties, Auto-create report en Create a blank report. Laten we het automatisch aanmaken proberen, dus selecteer **Auto-create report**.

    ![](../media/Lab_7.5.png)

8. Power BI zal beginnen met het automatisch aanmaken van het rapport. Let op: er is een optie om data vooraf te selecteren als we dat willen (Pre-select data). Zodra het rapport klaar is, verschijnt er een dialoogvenster rechtsboven in het scherm. Selecteer **View report now**.

    ![](../media/Lab_7.6.png)
 
   >**Controlepunt:** Je hebt een rapport dat eruitziet zoals de onderstaande schermafbeelding. Er zijn een aantal KPI's en enkele trendvisualisaties. Dit is een goed startpunt als je een nieuw model analyseert en snel op gang wilt komen.
   >**Opmerking:** Let op het bovenste menu: je hebt de optie om het rapport te bewerken (Edit) of om een deel van de data als tabellen te bekijken. Neem gerust de tijd om deze opties te verkennen.

9. Laten we dit rapport opslaan. Selecteer in het bovenste menu **Save**.
10. Het dialoogvenster Save your report opent. Geef het rapport de naam **rpt_Sales_Auto_Report**
    >**Opmerking:** We gebruiken het voorvoegsel rpt voor de rapportnaam, wat een afkorting is voor report.
11. Zorg ervoor dat het rapport wordt opgeslagen in je workspace, **FAIAD_<username>**.
12. Selecteer **Save**.

    ![](../media/Lab_7.7.png)
 
    >**Opmerking:** Het automatisch gegenereerde rapport kan er bij jou anders uitzien, omdat het "automatisch aangemaakt" is. Het hangt ook af van de relaties en measures die je in het vorige lab hebt aangemaakt (Lab 6).
    De bovenstaande schermafbeelding toont hoe het automatisch gegenereerde rapport **mogelijk** eruitziet als je alle relaties en measures hebt aangemaakt, inclusief de optionele relaties (Lab 6).
    De onderstaande schermafbeelding toont hoe het automatisch gegenereerde rapport **mogelijk** eruitziet als je het aanmaken van de optionele relaties en measures hebt overgeslagen (Lab 6).

    ![](../media/Lab_7.8.png)
 
### <a name="_toc152166237"></a>Task 2: Configure background for a New report

Laten we een nieuw rapport aanmaken met een leeg canvas.

1. Selecteer in het **linkerdeelvenster** de naam van je workspace, **FAIAD_<username>**, om naar de workspace te navigeren.

   ![](../media/Lab_7.9.png)

2. Selecteer in het bovenste menu **New -> Report**. Je wordt doorgestuurd naar de pagina Build your first report.
 
3. Selecteer **Pick a published semantic model** zodat we het model kunnen kiezen dat we hebben aangemaakt.

   ![](../media/Lab_7.10.png)
 
4. Het dialoogvenster Pick a semantic model to use in your report opent. Selecteer **lh_FAIAD**.
5. Klik op de **pijl naast de Auto-create report-knop**. Selecteer **Create a blank report**.

    ![](../media/Lab_7.11.png)
 
6. Als je dit nog niet hebt gedaan, open dan **FAIAD.pbix** in de map **C:\FAIAD\Reports** van je labomgeving.

    We gaan dit rapport als referentie gebruiken. We beginnen met het toevoegen van de canvasachtergrond. We maken de rapportkoptekst aan, voegen een aantal KPI's toe en maken een lijngrafiek voor Sales over een bepaalde periode. Vanwege tijdsbeperkingen en in de veronderstelling dat je ervaring hebt met het bouwen van visualisaties in Power BI Desktop, zullen we niet alle visualisaties aanmaken.

    ![](../media/Lab_7.12.png)
 
7. Navigeer terug naar het **Power BI**-canvas in je browser.

8. Selecteer het **Format page icon** in het Visualizations-deelvenster.

9. Vouw de sectie **Canvas background** uit.

10. Selecteer **Browse** bij de optie **Image**. Het dialoogvenster van de bestandsverkenner opent.

11. Navigeer naar de map **C:\FAIAD\Reports** van je labomgeving.

12. Selecteer **Summary Background.png**.

13. Stel de vervolgkeuzelijst **Image fit** in op Fit.

14. Stel Transparency in op **0%**.

    ![](../media/Lab_7.13.png)
 
### <a name="_toc152166238"></a>Task 3: Add Header to the report

1. Laten we de koptekst in de bovenste marge toevoegen. Selecteer in het **menu** de optie **Text box**.

2. Voer **Fabrikam Company** in als de eerste regel in het tekstvak.

3. Voer **Sales Report** in als de tweede regel in het tekstvak.

4. Markeer **Fabrikam Company** en stel **Font** in op **Segoe UI** en **font size** op **18, bold**.

5. Markeer **Sales Report** en stel **Font** in op **Segoe UI** en **font size** op **14**.

6. Met het **tekstvak geselecteerd**, vouw in het deelvenster Format text box aan de rechterkant **Effects** uit.

7. Gebruik de schuifregelaar **Background** om dit op **Off** te zetten.

8. Pas de grootte van het **tekstvak aan zodat het in de bovenste marge past**.
 
    ![](../media/Lab_7.14.png)

### <a name="_toc152166239"></a><a name="_hlk152165928"></a>Task 4: Add KPIs to the report

1. Laten we de Sales KPI toevoegen. Selecteer de **witruimte** op het canvas om de focus van het tekstvak weg te nemen.

2. Selecteer in de **Visualizations section** de **Multi-row card visual**.

3. Vouw in de **Data section** de tabel **Sales** uit.

4. Selecteer de measure **Sales**.

    ![](../media/Lab_7.15.png)
 
5. Met de **multi-row card visual geselecteerd**, selecteer het **Format visual icon** in de Visualizations section.

6. Vouw de sectie **Category labels** uit.

7. Vergroot de **font size** naar **14**.

8. Selecteer de **Color drop down**. Het dialoogvenster Color palette opent.

9. Stel de Hex-waarde in op **004753**.

    ![](../media/Lab_7.16.png)
 
10. Vouw de sectie **Cards** uit.

11. Gebruik de schuifregelaar **Accent bar** om dit op **Off** te zetten.

    ![](../media/Lab_7.17.png)
 
12. Selecteer **General** in het Visualizations-deelvenster.

13. Vouw de sectie **Effects** uit.

14. Gebruik de schuifregelaar **Background** om dit op **Off** te zetten.

15. Pas de grootte van de **visual** aan en verplaats deze naar **het linker vak zoals weergegeven in de schermafbeelding**.

    ![](../media/Lab_7.18.png)
 
16. Laten we nog een KPI toevoegen. Selecteer de **Sales multi-row card** die we zojuist hebben aangemaakt. **Kopieer** de visual door **Ctrl+C** op je toetsenbord te selecteren.

17. **Plak** de visual door **Ctrl+V** op je toetsenbord te selecteren. De visual wordt op het canvas geplakt.

18. Met de **nieuwe visual gemarkeerd**, verwijder in de sectie **Visualization pane -> Build visual -> Fields** de measure Sales.

19. Vouw in de sectie **Data** de tabel **Sales** uit en selecteer de measure **Units**.

20. Pas de grootte van de **visual** aan en **plaats deze in het vak onder de Sales visual**.

    ![](../media/Lab_7.19.png)
 
### <a name="_toc152166240"></a>Task 5: Add Line chart to the report
Laten we een lijngrafiek aanmaken om Sales over de tijd per Reseller Company te visualiseren.
1. Selecteer de **witruimte** op het canvas om de focus van de multi-row card visual weg te nemen.

2. Selecteer in de **Visualizations section** de **Line chart**.

3. Vouw in de **Data section** de tabel **Date** uit.

4. Selecteer het veld **Year**. Let op: Year wordt standaard opgeteld en toegevoegd aan de Y-axis. Laten we dit corrigeren.

    ![](../media/Lab_7.20.png)
 
### <a name="_toc152166241"></a>Task 6: Save the report

Laten we het rapport opslaan voordat we ervan weggaan om wijzigingen aan het model aan te brengen.
1. Selecteer in het menu **File -> Save**.

2. Het dialoogvenster Save your report opent. Geef het rapport de naam **rpt_Sales_Report**.

    >**Opmerking:** We gebruiken het voorvoegsel rpt voor de rapportnaam, wat een afkorting is voor report.

3. Zorg ervoor dat het rapport wordt opgeslagen in de workspace **FAIAD_<username>**.

4. Selecteer **Save**.

    ![](../media/Lab_7.21.png)


### <a name="_toc152166242"></a>Task 7: Configure Year column in Date table

1. Selecteer in de **linker menubalk** **lh_FAIAD** om naar de lakehouse te navigeren.

2. Vouw in het linker Explorer pane **lhFAIAD -> Schemas -> dbo -> Tables -> Date** uit.

3. Selecteer de kolom **Year**.

4. Vouw in het deelvenster **Properties** aan de rechterkant de sectie **Advanced** uit.

5. Selecteer in de vervolgkeuzelijst Summarize by de optie **None**.

    ![](../media/Lab_7.22.png)
 
6. Navigeer terug naar het rapport door **rpt_Sales_Report** te selecteren in de linker menubalk.

7. Selecteer **Edit** in het bovenste menu.

8. Selecteer in het bovenste menu **Refresh**. Let op: in het Data-paneel is Year nu geen sommatieveld meer.

9. Met de **Line chart visual geselecteerd, verwijder Sum of Year** van de Y-axis.

10. Selecteer het veld **Year**, dat wordt toegevoegd aan de **X-axis**.

11. Vouw de tabel **Sales** uit en selecteer de measure **Sales**.
 
### <a name="_toc152166243"></a>Task 8: Configure Short_Month_Name column in Date table

1. Laten we een Month aan dit diagram toevoegen. Sleep vanuit de Date-tabel het veld **Short_Month_Name** onder **Year** in de **X-axis**. De visual is nu gesorteerd op Sales. Laten we sorteren op Short_Month_Name.

2. Selecteer de **ellipsis (…)** rechtsboven in de visual.

3. Selecteer **Sort axis -> Year Short_Month_Name**.

4. Selecteer de **ellipsis (…)** rechtsboven in de visual.

5. Selecteer **Sort axis -> Sort ascending**.

    ![](../media/Lab_7.24.png)
 
    >**Opmerking**: De maanden zijn alfabetisch gesorteerd. Laten we dit oplossen.

    ![](../media/Lab_7.25.png)
 
6. Selecteer in de **linker menubalk** **lh_FAIAD** om naar de lakehouse te navigeren.

7. Het dialoogvenster **Unsaved changes** opent. Selecteer **Save** om de wijzigingen in het rapport op te slaan.

    ![](../media/Lab_7.26.png)
 
8. Je wordt doorgestuurd naar de lh_FAIAD lakehouse. Vouw in het linker Explorer pane **lhFAIAD -> Schemas -> dbo -> Tables -> Date** uit.

9. Selecteer de kolom **Short_Month_Name**.

10. Vouw in het deelvenster **Properties** aan de rechterkant de sectie **Advanced** uit.

11. Selecteer in de vervolgkeuzelijst **Sort by column** de optie **Month**.

    ![](../media/Lab_7.27.png)
 
12. Navigeer terug naar het rapport door **rpt_Sales_Report** te selecteren in de linker menubalk.

13. Selecteer **Edit** in het bovenste menu.

14. Selecteer in het bovenste menu **Refresh**. De maanden zijn nu correct gesorteerd.

    ![](../media/Lab_7.28.png)
 
### <a name="_toc152166244"></a>Task 9: Format Line chart

Merk op hoe eenvoudig het is om het semantische model bij te werken terwijl je rapporten bouwt. Dit geeft een naadloze interactie vergelijkbaar met Power BI Desktop.

1. Met de **Line chart visual geselecteerd**, vouw in de **Data section** de tabel **Reseller** uit.
2. Sleep het veld **Reseller -> Reseller Company** naar de sectie **Legend**.

    ![](../media/Lab_7.29.png)
 
3. Met de **Line chart visual geselecteerd**, selecteer in de sectie **Visualization** het **Format visual icon -> General**.
4. Vouw de sectie **Title** uit.
5. Stel de tekst van **Title** in op **Sales over time**.
6. Vouw de sectie **Effects** uit.
7. Gebruik de schuifregelaar **Background** om dit op **Off** te zetten.

    ![](../media/Lab_7.30.png)
 
8. Selecteer in de sectie **Visualization** het **Format visual icon -> Visual**.
9. Vouw de sectie **Lines** uit.
10. Vouw de sectie **Colors** uit.
11. Stel de kleur van **Wingtip Toys** in op **#004753**.
12. Stel de kleur van **Tailspin Toys** in op **#F17925**.
13. Pas de grootte van de **visual** aan en verplaats deze naar **het vak rechtsboven zoals weergegeven in de schermafbeelding**.
14. Scroll naar rechts in de visual en **merk op dat we data hebben tot en met april 2023**.

    ![](../media/Lab_7.31.png)
 
15. Laten we het rapport opslaan: selecteer in het menu **File -> Save**.
Zoals eerder vermeld, zullen we niet alle visualisaties in dit lab bouwen. Neem gerust de tijd om meer visualisaties aan te maken.

### <a name="_toc152166245"></a>Task 10: Add new data to simulate Direct Lake Mode

In Import mode moet het Power BI-model worden vernieuwd nadat de data in de bron is vernieuwd, waarna de data in het rapport wordt bijgewerkt. In Direct Query mode is de data direct beschikbaar in het Power BI-rapport zodra de data in de bron wordt vernieuwd. Direct Query mode is echter doorgaans traag. Om dit probleem op te lossen heeft Microsoft Fabric Direct Lake mode geïntroduceerd. Direct Lake is een snelle methode om data vanuit het lake rechtstreeks in de Power BI-engine te laden, klaar voor analyse. Laten we dit verkennen.
In een echte situatie wordt de data bijgewerkt bij de bron. Omdat we ons in een trainingsomgeving bevinden, simuleren we dit door verbinding te maken met een parquet-bestand met data voor mei 2023.

1. Selecteer **FAIAD_<username>** in de linker menubalk om naar de workspace home te navigeren.
2. Selecteer **df_Sales_ADFS** zodat we de dataflow kunnen bewerken door het nieuwe Parquet-bestand toe te voegen.

   ![](../media/Lab_7.32.png)

3. Selecteer in het lint **Home -> Get data -> Blank query**.
4. Het dialoogvenster Connect to data source opent. **Selecteer alle regels in de editor en verwijder deze**.
5. Kopieer de onderstaande code en plak deze in de editor.

    ```
    let
       Source = #"ADLS Base Folder",
       #"Filtered Rows" = Table.SelectRows(Source, each Text.Contains([Folder Path], "Sales.Invoices_May")),
       #"https://stvnextblobstorage dfs core windows net/fabrikam-sales/Delta-Parquet-Format/Sales Invoices_May/_0-0ee085a3-716f-4833-a792-c3162c1de300-0 parquet" = #"Filtered Rows"{[#"Folder Path"="https://stvnextblobstorage.dfs.core.windows.net/fabrikam-sales/Delta-Parquet-Format/Sales.Invoices_May/",Name="0-0ee085a3-716f-4833-a792-c3162c1de300-0.parquet"]}[Content],
       #"Imported Parquet" = Parquet.Document(#"https://stvnextblobstorage dfs core windows net/fabrikam-sales/Delta-Parquet-Format/Sales Invoices_May/_0-0ee085a3-716f-4833-a792-c3162c1de300-0 parquet")
    in
       #"Imported Parquet"
    ```

7. Selecteer **Next**.

   ![](../media/Lab_7.33.png)
 
8. Er wordt een nieuwe query aangemaakt. Laten we deze **hernoemen**. Hernoem de query naar **MayInvoice** in het rechterdeelvenster, onder **Query settings -> Properties -> Name**.

9. Laten we staging uitschakelen voor de nieuwe query. **Klik met de rechtermuisknop** op de MayInvoice-query en **verwijder het vinkje bij Enable staging**.

   ![](../media/Lab_7.34.png)
 
10. Laten we nu de **invoice**-data van mei toevoegen aan de Invoice-tabel. Selecteer de Invoice-query in de Queries section.
11. Selecteer in het lint **Home -> Append** queries.
12. Het dialoogvenster Append query verschijnt. Selecteer in de vervolgkeuzelijst **Table to append** de optie **MayInvoice**.
13. Selecteer **OK**.

    ![](../media/Lab_7.35.png)
 
14. Selecteer **Publish** in de rechterbenedenhoek om de updates op te slaan en te publiceren.

    ![](../media/Lab_7.36.png)
 
>**Opmerking:** Nadat de dataflow is gepubliceerd, wordt deze vernieuwd. Dit kan enkele minuten duren.

14. Selecteer **rpt_Sales_Report** in de linker menubalk om terug te navigeren naar het rapport.
15. Selecteer in het bovenste menu **Refresh**. Merk op dat de Line chart nu data bevat voor mei 2023. Ook de Sales-bedragen en Units zijn toegenomen.

    ![](../media/Lab_7.37.png)
 
De Dataflows die we in eerdere labs hebben aangemaakt, worden vernieuwd volgens een schema, data wordt in de Lakehouse geladen. Het datamodel in de Lakehouse wordt bijgewerkt en de rapporten worden vernieuwd. We hoeven het datamodel en het rapport niet te vernieuwen elke keer dat een van de Dataflows wordt vernieuwd. Dit is het voordeel van Direct Lake.
Laten we de uitdagingen opnieuw bekijken die in de probleemstelling worden vermeld:

- **Je moet je dataset minimaal drie keer per dag vernieuwen om de verschillende updatetijden van de verschillende databronnen bij te houden.**
Dit hebben we opgelost met Direct Lake. Elke afzonderlijke data flow wordt vernieuwd volgens zijn eigen schema. De dataset en het rapport hoeven niet te worden vernieuwd.
- **Je vernieuwingen duren lang omdat je elke keer een volledige vernieuwing moet uitvoeren om eventuele updates van de bronsystemen vast te leggen.**
Ook dit hebben we opgelost met Direct Lake. Elke afzonderlijke data flow wordt vernieuwd volgens zijn eigen schema. De dataset en het rapport hoeven niet te worden vernieuwd, dus hoeven we ons geen zorgen te maken over volledige vernieuwing.
- **Fouten in een van de databronnen waaruit je data haalt, zorgen ervoor dat de vernieuwing van je dataset mislukt. Vaak wordt het medewerkersbestand niet op tijd geüpload, waardoor de vernieuwing van je dataset mislukt.**
Data Pipeline helpt dit probleem op te lossen door de mogelijkheid te bieden om vernieuwingen bij een fout opnieuw te proberen en op verschillende intervallen.
- **Het kost erg veel tijd om wijzigingen in je datamodel aan te brengen, omdat Power Query lang doet over het vernieuwen van de previews vanwege de grote datavolumes en complexe transformaties.**
We merkten dat Dataflows efficiënt zijn en dat wijzigingen eenvoudig kunnen worden aangebracht. Doorgaans duurt het laden van previews in Dataflows niet lang.
- **Je hebt een Windows-pc nodig om Power BI Desktop te gebruiken, terwijl de bedrijfsstandaard Mac is.**
Microsoft Fabric is een SaaS-aanbod. We hebben alleen een browser nodig om toegang te krijgen tot de service. We hoeven geen software op onze desktops te installeren.

# <a name="_toc152166246"></a>Labopdracht opschonen

Volg de onderstaande stappen zodra je klaar bent om de labomgeving op te schonen.

1. Selecteer de workspace **FAIAD_<username>** in het linkerdeelvenster om naar de workspace home te navigeren.
2. Selecteer in het bovenste menu de **ellipsis (…)** naast Manage access en selecteer **Workspace settings**.

   ![](../media/Lab_7.38.png)
 
3. Het dialoogvenster Workspace settings opent. Selecteer **Other** in het linkermenu.
4. Selecteer **Remove this workspace**.
5. Het dialoogvenster Delete workspace opent. Selecteer **Delete**.
Dit verwijdert de workspace en alle items die daarin waren opgenomen.

   ![](../media/Lab_7.39.png)
 
# <a name="_toc150777627"></a><a name="_toc150779083"></a><a name="_toc152166247"></a>Referenties

Fabric Analyst in a Day (FAIAD) introduceert je bij enkele van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service bevat de sectie Help (?) koppelingen naar een aantal uitstekende bronnen.

   ![](../media/img18.png) 
 
Hieronder volgen nog enkele bronnen die je helpen bij je volgende stappen met Microsoft Fabric.

-	Lees de blogpost voor de volledige [Microsoft Fabric GA-aankondiging](https://www.microsoft.com/en-us/microsoft-fabric/blog/2023/11/15/prepare-your-data-for-ai-innovation-with-microsoft-fabric-now-generally-available/)
-	Verken Fabric via de [Guided Tour](https://guidedtour.microsoft.com/en-us/guidedtour/microsoft-fabric/microsoft-fabric/1/1)
-	Meld je aan voor de [gratis proefversie van Microsoft Fabric](https://app.powerbi.com/home?experience=power-bi)
-	Bezoek de [Microsoft Fabric-website](https://www.microsoft.com/en-in/microsoft-fabric)
-	Leer nieuwe vaardigheden door de [Fabric Learning modules](https://aka.ms/learn-fabric) te verkennen
-	Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)
-	Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
-	Word lid van de [Fabric-community](https://aka.ms/fabric-community) om vragen te stellen, feedback te delen en van anderen te leren

Lees de uitgebreidere aankondigingsblogs over de Fabric-ervaringen:

-	[Data Factory experience in Fabric blog](https://aka.ms/Fabric-Data-Factory-Blog)
-	[Synapse Data Engineering experience in Fabric blog](https://aka.ms/Fabric-DE-Blog) 
-	[Synapse Data Science experience in Fabric blog](https://aka.ms/Fabric-DS-Blog) 
-	[Synapse Data Warehousing experience in Fabric blog](https://aka.ms/Fabric-DW-Blog) 
-	[Synapse Real-Time Analytics experience in Fabric blog](https://aka.ms/Fabric-RTA-Blog)
-	[Power BI announcement blog](https://aka.ms/Fabric-PBI-Blog)
-	[Data Activator experience in Fabric blog](https://aka.ms/Fabric-DA-Blog)
-	[Administration and governance in Fabric blog](https://aka.ms/Fabric-Admin-Gov-Blog)
-	[OneLake in Fabric blog](https://aka.ms/Fabric-OneLake-Blog)
-	[Dataverse and Microsoft Fabric integration blog](https://aka.ms/Dataverse-Fabric-Blog)

© 2023 Microsoft Corporation. Alle rechten voorbehouden.

Door gebruik te maken van deze demo/dit lab, ga je akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met als doel feedback van je te ontvangen en je een leerervaring te bieden. Je mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback te geven aan Microsoft. Je mag het niet voor enig ander doel gebruiken. Je mag deze demo/dit lab of enig deel daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN DEEL DAARVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE VOOR VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARE-TECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN GEPRESENTEERD, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DEZELFDE MANIER ALS EEN DEFINITIEVE VERSIE. WE KUNNEN OOK BESLUITEN GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UIT TE BRENGEN. JE ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK ANDERS ZIJN.

**FEEDBACK**. Als je feedback geeft over de technologiefuncties, functionaliteit en/of concepten die in deze demo/dit lab worden beschreven aan Microsoft, geef je Microsoft, zonder enige vergoeding, het recht om je feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, te delen en te commercialiseren. Je geeft ook aan derden, zonder enige vergoeding, alle octrooirechten die nodig zijn voor hun producten, technologieën en diensten om gebruik te maken van of te koppelen aan specifieke onderdelen van Microsoft-software of -diensten die de feedback bevatten. Je zult geen feedback geven die onderworpen is aan een licentie die vereist dat Microsoft zijn software of documentatie aan derden in licentie geeft omdat we je feedback daarin opnemen. Deze rechten blijven van kracht na beëindiging van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, MET INBEGRIP VAN ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, HETZIJ UITDRUKKELIJK, IMPLICIET OF WETTELIJK, GESCHIKTHEID VOOR EEN BEPAALD DOEL, TITEL EN NIET-INBREUK. MICROSOFT GEEFT GEEN TOEZEGGINGEN OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE UITVOER DIE VOORTKOMT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR ENIG DOEL.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen veranderen in toekomstige versies van het product. In deze demo/dit lab leer je over enkele, maar niet alle, nieuwe functies.
