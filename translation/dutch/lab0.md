# Microsoft Fabric - Fabric Analyst in a Day

![tesb](../media/Aspose.Words.2ed70cc0-be12-4074-8ce5-48f6b0305ec4.001.png)

Lab Vereisten 

# Inhoudsopgave
[Documentstructuur](#DocumentStructure)

[Scenario / Probleemstelling](###Scenario/ProblemStatement)

[Overzicht van het Power BI Desktop-rapport](#OverviewofPowerBIDesktopReport)

[Referenties](#References)

# Documentstructuur {#DocumentStructure}

De lab bevat stappen die de gebruiker samen kan volgen, aangevuld met bijbehorende screenshots die visuele ondersteuning bieden. In de screenshots zijn secties gemarkeerd met rode of oranje kaders om het gebied aan te duiden waarop de gebruiker zich moet richten.

### Scenario / Probleemstelling {#Scenario/ProblemStatement}

Fabrikam, Inc. is een groothandel in nieuwigheidsgoederen. Als groothandel zijn Fabrikam's klanten voornamelijk bedrijven die doorverkopen aan particulieren. Fabrikam verkoopt aan retailklanten door de gehele Verenigde Staten, waaronder speciaalzaken, supermarkten, computerwinkels en toeristische attractiewinkels. Fabrikam verkoopt ook aan andere groothandelaren via een netwerk van agenten die de producten namens Fabrikam promoten. Hoewel alle klanten van Fabrikam momenteel gevestigd zijn in de Verenigde Staten, is het bedrijf van plan om uit te breiden naar andere landen/regio's.

U bent een Data Analyst in het Sales-team. U verzamelt, schoont en interpreteert datasets om zakelijke problemen op te lossen. Daarnaast maakt u visualisaties zoals grafieken en diagrammen, schrijft u rapporten en presenteert u deze aan de besluitvormers in de organisatie.

Om waardevolle inzichten uit de data te halen, haalt u gegevens op uit meerdere systemen, schoont u deze op en combineert u ze. U haalt data op uit de volgende bronnen:

- Sales Data: Deze data is afkomstig uit het ERP-systeem en is opgeslagen in een ADLS Gen 2-database of Databricks. De gegevens worden elke dag om 12:00 uur bijgewerkt.
- Supplier Data: Deze data is afkomstig van de verschillende leveranciers en is opgeslagen in een Snowflake-database. De gegevens worden elke dag om middernacht bijgewerkt.
- Customer data: deze data is afkomstig uit Customer Insights en is opgeslagen in Dataverse. De gegevens zijn altijd up-to-date.
- Employees Data: Deze data is afkomstig uit het HR-systeem en is opgeslagen als exportbestand in een SharePoint-map. De gegevens worden elke ochtend om 9:00 uur bijgewerkt.   

   ![A diagram of data flow](../media/Picture3.png)

U bouwt momenteel een dataset in Power BI premium die de data ophaalt uit de bovenstaande bronsystemen om te voldoen aan uw rapportagebehoeften en eindgebruikers de mogelijkheid te bieden voor self-service. U gebruikt Power Query om uw dataset bij te werken. 

U wordt geconfronteerd met de volgende uitdagingen:

- U moet uw dataset minstens 3 keer per dag vernieuwen om rekening te houden met de verschillende bijwerktijden van de verschillende databronnen.
- Uw vernieuwingen duren lang omdat u elke keer een volledige refresh moet uitvoeren om wijzigingen in de bronsystemen te verwerken.
- Fouten in een van de databronnen waaruit u gegevens ophaalt, zorgen ervoor dat de refresh van uw dataset mislukt. Het medewerkerbestand wordt regelmatig niet op tijd geüpload, waardoor de refresh van uw dataset mislukt. 
- Het duurt erg lang om wijzigingen in uw datamodel aan te brengen, omdat Power Query er lang over doet om voorbeeldweergaven te vernieuwen vanwege de grote dataomvang en complexe transformaties. 
- U heeft een Windows-pc nodig om Power BI Desktop te gebruiken, terwijl de bedrijfsstandaard Mac is. 



U heeft gehoord over Fabric en heeft besloten Fabric te proberen om te zien of het de uitdagingen waarmee u te maken heeft kan oplossen.

## Overzicht van het Power BI Desktop-rapport {#OverviewofPowerBIDesktopReport}

Voordat we beginnen met Fabric, bekijken we het huidige rapport in Power BI Desktop om de transformaties en het model te begrijpen.

1. Open het bestand **FAIAD.pbix** in de map **reports/FAIAD.pbix** van het labmateriaal. Het bestand wordt geopend in Power BI Desktop.

   Het rapport analyseert de Sales voor Fabrikam. KPI's worden linksboven op de pagina weergegeven. De overige visuals tonen Sales over de tijd, per Territory, per Product Group en per Resellers. 

    ![A screenshot of Power BI Desktop report](../media/Picture4.png)

1. **Opmerking:** In deze training richten we ons op de data-acquisitie, transformatie en modellering met behulp van tools die beschikbaar zijn in Fabric. We richten ons niet op rapportontwikkeling of navigatie. Laten we een paar minuten de tijd nemen om het rapport te begrijpen en daarna verdergaan met de volgende stappen.
1. Laten we de data analyseren per Sales Territory. Selecteer New England in de visual Sales Territory (Scatter plot).

      Let op dat in de Sales over Time, Reseller Tailspin Toys meer sales heeft dan Wingtip Toys in New England. Als u kijkt naar de kolomgrafiek Sales YoY%, zult u opmerken dat de verkoopgroei van Wingtip laag was en kwartaal over kwartaal is gedaald gedurende het afgelopen jaar. Na een klein herstel in Q3 daalde het opnieuw in Q4. 

      ![A screenshot of Power BI Desktop report with New England selected](../media/Picture5.png)
1. Laten we dit vergelijken met het gebied Rocky Mountain. Selecteer Rocky Mountain in de visual Sales Territory (Scatter plot).

      Let op dat in de kolomgrafiek Sales YoY% de sales van Wingtip Toys in 2022 Q4 sterk zijn gestegen na een periode van twee kwartalen met lage verkopen.

      ![A screenshot of Power BI Desktop report with Rocky Mountain selected](../media/Picture6.png)
1. Selecteer **Rocky Mountain in Sales Territory** om het filter te verwijderen.
1. Selecteer in de Scatter plot onderaan het midden van het scherm (Sales Orders by Sales) de uitbijter rechtsboven (4e kwadrant).

      Let op dat de margin % 52% is, wat boven het gemiddelde van 50% ligt. Ook is de Sales YoY% gestegen in de laatste 2 kwartalen van 2022.

      ![A screenshot of Power BI Desktop with Scatter plot selection](../media/Picture7.png)

1. Selecteer de uitbijter Reseller in de scatter plot om het filter te verwijderen.
1. Laten we de productdetails bekijken per Product Group en Reseller. Klik in de staafgrafiek Sales by Product Group and Reseller Company met de rechtermuisknop op de **Packaging Materials-balk voor Tailspin Toys** en selecteer in het dialoogvenster Drill through -> Product Details.
      ![A screenshot of Power BI Desktop with Drill through selection](../media/Picture8.png)
   
1. U wordt doorgestuurd naar de pagina met de Product Details. Let op dat er ook een aantal toekomstige orders zijn geplaatst.
1. Wanneer u klaar bent met het bekijken van deze pagina, selecteert u de Ctrl+pijl-terug rechtsboven op de pagina om terug te navigeren naar het Sales Report.

    ![A screenshot of Power BI Desktop Product Details page](../media/Picture9.png)

1. U kunt het rapport verder analyseren. Wanneer u klaar bent, bekijken we de modelweergave. Selecteer in het linkerpaneel het **Model view icon**. Let op dat er twee fact-tabellen zijn: Sales en PO. 
   1. De granulariteit van de Sales-data is per Date, per Reseller, per Product en People. Date, Reseller, Product en People zijn gekoppeld aan Sales.
   1. De granulariteit van de PO-data is per Date, per Product en People. Date, Product en People zijn gekoppeld aan PO.
   1. We hebben Supplier-data per Product. Supplier is gekoppeld aan Product.
   1. We hebben de locatie van de Reseller. Geo is gekoppeld aan Reseller.
   1. We hebben Customer-informatie per Reseller. Customer is gekoppeld aan Reseller. 
1. Laten we Power Query bekijken om de databronnen te begrijpen. Selecteer in het lint **Home -> Transform data.**

    ![A screenshot of data model](../media/Picture10.png)

1. Het Power Query-venster wordt geopend. Selecteer in het lint **Home -> Data** source settings. Het dialoogvenster Data source settings wordt geopend. Let op dat we 4 databronnen hebben zoals vermeld in de probleemstelling.
   1. Snowflake
   1. Sharepoint
   1. Azure Data Lake Gen2
   1. Dataverse
1. Selecteer **Close** om het dialoogvenster Data source settings te sluiten.

    ![A screenshot of Datasour](../media/Picture11.png)

1. In het linker Queries-paneel ziet u dat de queries zijn gegroepeerd per databron. 
1. Let op dat de map **DataverseData** CustomerData bevat, beschikbaar in 4 verschillende queries: BabyBoomer, GenX, GenY en GenZ. Deze 4 queries worden samengevoegd om de Customer-query te maken.

    ![A screenshot of queries](../media/Picture12.png)

   Let op dat de map **ADLSData** meerdere dimensies bevat: Geo, Product, Reseller en Date. Ook bevat de map het Sales fact.
   1. De Geo-dimensie wordt gemaakt door data samen te voegen uit de queries Cities, Countries en States. 
   1. De Product-dimensie wordt gemaakt door data samen te voegen uit de queries Product Groups en Product Item Group.
   1. De Reseller-dimensie wordt gefilterd met behulp van de BuyingGroup-query.
   1. Het Sales fact wordt gemaakt door InvoiceLineItems samen te voegen met de Invoice-query.
1. Let op dat de map Snowflake**Data** de Supplier-dimensie en het PO (Order/Spend) fact bevat.
   1. De Supplier-dimensie wordt gemaakt door de Suppliers-query samen te voegen met de SupplierCategories-query.
   1. Het PO fact wordt gemaakt door PO samen te voegen met de PO Line Items-query.
1. Let op dat de map SharepointData de People-dimensie bevat.

Nu weten we waarmee we te maken hebben. In de volgende labs zullen we een vergelijkbare Power Query maken met Dataflow Gen2 en een model bouwen met Lakehouse.

# Referenties {#References}
Fabric Analyst in a Day introduceert u in enkele van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service bevat de sectie Help links naar uitstekende bronnen.

   ![A screenshot of help options](../media/Picture13.png)

Hieronder vindt u nog enkele aanvullende bronnen die u zullen helpen bij uw volgende stappen met Microsoft Fabric.

Lees de blogpost voor de volledige [Microsoft Fabric GA-aankondiging](https://aka.ms/build2023-fabricblog)

- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)

Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)

Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)

- Leer nieuwe vaardigheden door de [Fabric Learning modules](https://aka.ms/learn-fabric) te verkennen

- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)

Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook) (https://info.microsoft.com/ww-landing-introduction-to-microsoft-fabric-webinar-series.html?lcid=en-us)

Lees de uitgebreidere aankondigingsblogs per Fabric-ervaring:

[Data Factory experience in Fabric blog](https://aka.ms/Fabric-Data-Factory-Blog) 

[Synapse Data Engineering experience in Fabric blog](https://aka.ms/Fabric-DE-Blog) 

[Synapse Data Science experience in Fabric blog](https://aka.ms/Fabric-DS-Blog) 

[Synapse Data Warehousing experience in Fabric blog](https://aka.ms/Fabric-DW-Blog) 

[Synapse Real-Time Analytics experience in Fabric blog](https://aka.ms/Fabric-RTA-Blog)

[Power BI announcement blog](https://aka.ms/Fabric-PBI-Blog)

[Data Activator experience in Fabric blog](https://aka.ms/Fabric-DA-Blog) 

[Administration and governance in Fabric blog](https://aka.ms/Fabric-Admin-Gov-Blog)

[OneLake](https://aka.ms/Fabric-OneLake-Blog)[ in Fabric blog](https://aka.ms/Fabric-OneLake-Blog)

[Dataverse and Microsoft Fabric integration blog](https://aka.ms/Dataverse-Fabric-Blog)

© 2023 Microsoft Corporation. Alle rechten voorbehouden.
