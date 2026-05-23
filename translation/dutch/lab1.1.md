# Microsoft Fabric - Fabric Analyst in a Day - Lab 1

# ![](../media/img2.png)

# Inhoudsopgave
- Documentstructuur
- Scenario / Probleemstelling
- Overzicht van het Power BI Desktop-rapport
   - Taak 1: Power BI Desktop instellen in de labomgeving
   - Taak 2: Het Power BI Desktop-rapport analyseren
   - Taak 3: Power Queries bekijken
- Referenties

# Documentstructuur
Het lab bevat stappen die de gebruiker dient te volgen, met bijbehorende schermafbeeldingen als visuele ondersteuning. In elke schermafbeelding zijn secties gemarkeerd met oranje kaders om het gebied aan te geven waarop de gebruiker zich moet richten.

# Scenario / Probleemstelling
Fabrikam, Inc. is een groothandel in nieuwigheidsgoederen. Als groothandel zijn Fabrikam's klanten voornamelijk bedrijven die doorverkopen aan particulieren. Fabrikam verkoopt aan retailklanten door de hele Verenigde Staten, waaronder speciaalzaken, supermarkten, computerwinkels en toeristische attractiewinkels. Fabrikam verkoopt ook aan andere groothandels via een netwerk van agenten die de producten namens Fabrikam promoten. Hoewel alle klanten van Fabrikam momenteel gevestigd zijn in de Verenigde Staten, is het bedrijf van plan uit te breiden naar andere landen/regio's.

U bent een Data Analyst in het salesteam. U verzamelt, reinigt en interpreteert datasets om zakelijke problemen op te lossen. U stelt ook visualisaties samen zoals grafieken en diagrammen, schrijft rapporten en presenteert deze aan de besluitvormers binnen de organisatie.

Om waardevolle inzichten uit de data te halen, haalt u gegevens op uit meerdere systemen, reinigt u deze en combineert u ze. U haalt gegevens op uit de volgende bronnen:
- **Salesdata:** afkomstig uit het ERP-systeem; de data is opgeslagen in een ADLS Gen2-database of Databricks. De data wordt elke dag bijgewerkt om 12:00 uur 's middags.
- **Leveranciersdata:** afkomstig van verschillende leveranciers; de data is opgeslagen in een Snowflake-database. De data wordt elke dag bijgewerkt om 12:00 uur 's nachts.
- **Klantdata:** afkomstig uit Customer Insights; de data is opgeslagen in Dataverse. De data is altijd actueel.
- **Werknemersdata:** afkomstig uit het HR-systeem; deze is opgeslagen als exportbestand in een SharePoint-map. De data wordt elke ochtend om 9:00 uur bijgewerkt.
 
   # ![](../media/img1.png)
U bouwt momenteel een dataset in Power BI Premium die de gegevens uit bovenstaande bronsystemen ophaalt om aan uw rapportagevereisten te voldoen en eindgebruikers de mogelijkheid te bieden om zelf te werken met de data. U gebruikt Power Query om uw model bij te werken.

**U wordt geconfronteerd met de volgende uitdagingen:**
  - U moet uw dataset minstens drie keer per dag vernieuwen om rekening te houden met de verschillende updatetijden van de verschillende databronnen.
  - Uw vernieuwingen duren lang omdat u elke keer een volledige vernieuwing moet uitvoeren om eventuele updates in de bronsystemen te verwerken.
  - Fouten in een van de databronnen waaruit u gegevens ophaalt, zullen ervoor zorgen dat de vernieuwing van uw dataset mislukt. Heel vaak wordt het werknemersbestand niet op tijd geüpload, waardoor de vernieuwing van uw dataset mislukt.
  - Het kost erg veel tijd om wijzigingen in uw datamodel aan te brengen, omdat Power Query lang nodig heeft om de previews te vernieuwen vanwege de grote datavolumes en complexe transformaties.
  - U heeft een Windows-pc nodig om Power BI Desktop te gebruiken, terwijl de bedrijfsstandaard Mac is.

U heeft gehoord over Microsoft Fabric en heeft besloten het uit te proberen om te zien of het uw uitdagingen aanpakt.

# Overzicht van het Power BI Desktop-rapport
Voordat we beginnen met Fabric, bekijken we het huidige rapport in Power BI Desktop om de transformaties en het model te begrijpen.

### Taak 1: Power BI Desktop instellen in de labomgeving

1. Open het bestand **FAIAD.pbix** in de map **Reports** op het **bureaublad**. Het bestand wordt geopend in Power BI Desktop.

   # ![](../media/L1T1S1.png)

2. U ziet het tabblad **Enter your email address**. Voer hier uw inloggegevens in en selecteer **Continue**:
 
   - **Email:** <inject key="AzureAdUserEmail"></inject>
 
    ![Enter Your Username](../media/faiadlab1-6.png)
 
3. U ziet het tabblad **Sign in**. Voer hier uw inloggegevens in en selecteer **Next**:
 
   - **Email/Username:** <inject key="AzureAdUserEmail"></inject>
 
    ![Enter Your Username](../media/faiadlab1-7.png)
 
4. Geef vervolgens uw wachtwoord op en selecteer **Sign in**:
 
   - **Password:** <inject key="AzureAdUserPassword"></inject>
 
   ![Enter Your Password](../media/faiadlab1-8.png)
 
5. Selecteer **No, sign in to this app only** in het volgende dialoogvenster. Power BI Desktop wordt nu geopend.

    # ![](../media/faiadlab1-9.png)

### Taak 2: Het Power BI Desktop-rapport analyseren
Het onderstaande rapport analyseert de sales van Fabrikam. KPI's staan linksboven op de pagina vermeld. De overige visuals tonen de sales over tijd, per Territory, Product Group en Reseller Company.

   # ![](../media/img8.png)
 
**Opmerking**: In deze training richten we ons op het ophalen, transformeren en modelleren van data met behulp van de tools die beschikbaar zijn in Fabric. We richten ons niet op rapportontwikkeling of navigatie. Laten we een paar minuten besteden aan het begrijpen van het rapport en dan verdergaan met de volgende stappen.

1. Laten we de data analyseren per Sales Territory. Selecteer **New England in het Sales Territory**-visual (spreidingsdiagram). U ziet in de sales over tijd dat Reseller Tailspin Toys meer sales heeft dan Wingtip Toys in New England. Als u kijkt naar het kolomdiagram Sales YoY%, ziet u dat de salesgroei van Wingtip Toys laag is geweest en kwartaal op kwartaal is gedaald in het afgelopen jaar. Na een klein herstel in Q3 daalde het opnieuw in Q4.

   # ![](../media/img9.png)
 
2. Laten we dit vergelijken met de Rocky Mountain territory. Selecteer **Rocky Mountain in het Sales Territory**-visual (spreidingsdiagram). U ziet in het kolomdiagram Sales YoY% dat de sales van Wingtip Toys dramatisch zijn gestegen in 2022 Q4, nadat ze de twee voorgaande kwartalen laag waren.

   # ![](../media/img10.png)
 
3. Selecteer **Rocky Mountain in het Sales Territory** om het filter te verwijderen.

4. Selecteer in het spreidingsdiagram onderin het midden van het scherm (Sales Orders by Sales) de uitbijter rechtsboven (4e kwadrant). U ziet dat het marge-% 52% is, wat boven het gemiddelde van 50% ligt. Ook is het Sales YoY% omhooggegaan in de laatste twee kwartalen van 2022.

   # ![](../media/img11.png)
 
5. Selecteer de uitbijter Reseller in het spreidingsdiagram om het **filter te verwijderen**.
6. Laten we de productdetails bekijken per Product Group en Reseller. Klik in het staafdiagram Sales by Product Group and Reseller Company met de **rechtermuisknop op de balk Packaging Materials voor Tailspin Toys** en selecteer in het dialoogvenster **Drill through -> Product Detail**.

   # ![](../media/img12.png)
 
   U wordt doorgeleid naar de pagina met de productdetails. U ziet dat er ook toekomstige orders zijn geplaatst.

7. Zodra u klaar bent met het bekijken van deze pagina, selecteert u de **Ctrl+back arrow** rechtsboven op de pagina om terug te navigeren naar het Sales-rapport.

   # ![](../media/img13.png)
  
8. U kunt het rapport verder analyseren naar eigen inzicht. Laten we daarna de modelweergave bekijken. Selecteer in het linkerdeelvenster het pictogram Model View. U ziet dat er twee feitentabellen zijn: Sales en PO.
      1. De granulariteit van de salesdata is op basis van Date, Reseller, Product en People. Date, Reseller, Product en People zijn gekoppeld aan Sales.
      2. De granulariteit van de PO-data is op basis van Date, Product en People. Date, Product en People zijn gekoppeld aan PO.
      3. We hebben Supplier-data per Product. Supplier is gekoppeld aan Product.
      4. We hebben locatiedata van Reseller per Geo. Geo is gekoppeld aan de Reseller.
      5. We hebben klantinformatie per Reseller. De Customer is gekoppeld aan de Reseller.

### Taak 3: Power Queries bekijken
1. Laten we Power Query bekijken om de databronnen te begrijpen. Selecteer in het lint Home -> Transform data -> Transform data.

   # ![](../media/faiadlab1-11.png)
 
2. Het Power Query-venster wordt geopend. Selecteer in het lint Home -> Data source settings. Het dialoogvenster voor databroninstelling wordt geopend. Terwijl u door de lijst scrollt, ziet u dat er vier databronnen zijn zoals vermeld in de probleemstelling:
      1. Snowflake
      2. SharePoint
      3. ADLS Gen2
      4. Dataverse

3. Selecteer **Close** om het dialoogvenster Data source settings te sluiten.

   # ![](../media/faiadlab1-12.png)
 
4. In het linker Queries-deelvenster ziet u dat de queries zijn gegroepeerd per databron.
5. U ziet dat de map **DataverseData** klantdata bevat die beschikbaar is in vier verschillende queries: BabyBoomer, GenX, GenY en GenZ. Deze vier queries worden samengevoegd om een Customer-query te maken.
6. U kunt de inloggegevens voor de Dataverse-databron invoeren door de **Username** en **Password** in te voeren die beschikbaar zijn op het tabblad **Environment Variables** (naast de Lab Guide). Selecteer de optie Microsoft account.

   # ![](../media/img16.png)
 
7. Gebruik voor de ADLS-databron de optie **Account Key** en voer de **Adls storage account Access key** in die beschikbaar is op het tabblad **Environment Variables** (naast de Lab Guide).
8. U ziet dat de map **ADLSData** meerdere dimensies bevat: Geo, Product, Reseller en Date. Het bevat ook Sales facts.
   1. De **Geo-dimensie** wordt gemaakt door data samen te voegen uit de queries Cities, Countries en States.
   2. De **Product-dimensie** wordt gemaakt door data samen te voegen uit de queries Product Groups en Product Item Group.
   3. De **Reseller-dimensie** wordt gefilterd met behulp van de BuyingGroup-query.
   4. Het **Sales fact** wordt gemaakt door InvoiceLineItems samen te voegen met de Invoice-query.
9. Gebruik voor de Snowflake-databron de Snowflake **Username** en Snowflake **Password** die beschikbaar zijn op het tabblad **Environment Variables** (naast de Lab Guide).
10. U ziet dat de map SnowflakeData de dimensie Supplier en het feit PO (Order / Spend) bevat.

   1. De **Supplier-dimensie** wordt gemaakt door de query Suppliers samen te voegen met de query SupplierCategories.
   2. Het **PO fact** wordt gemaakt door PO samen te voegen met de query PO Line Items.

11. Voer voor de SharePoint-databron de **Username** en **Password** in die beschikbaar zijn op het tabblad **Environment Variables** (naast de Lab Guide). Selecteer de optie Microsoft account.

12. U ziet dat de map SharepointData een dimensie People bevat.

    # ![](../media/img17.png) 

Nu weten we waarmee we te maken hebben. In de volgende labs maken we een vergelijkbare Power Query met behulp van Dataflow Gen2 en een model met behulp van Lakehouse.

# Referenties
Fabric Analyst in a Day (FAIAD) maakt u kennis met enkele van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service bevat de sectie Help (?) links naar uitstekende resources.

   # ![](../media/img18.png) 
 
Hieronder vindt u nog een aantal resources die u helpen bij uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [aankondiging van Microsoft Fabric GA](https://aka.ms/Fabric-Hero-Blog-Ignite23)
- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)
- Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)
- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)
- Leer nieuwe vaardigheden door de [Fabric Learning-modules](https://aka.ms/learn-fabric) te verkennen
- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)
- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om uw vragen te stellen, feedback te delen en van anderen te leren

Lees de meer diepgaande aankondigingsblogs over Fabric-ervaringen:

- [Blog over Data Factory-ervaring in Fabric](https://aka.ms/Fabric-Data-Factory-Blog) 
- [Blog over Synapse Data Engineering-ervaring in Fabric](https://aka.ms/Fabric-DE-Blog) 
- [Blog over Synapse Data Science-ervaring in Fabric](https://aka.ms/Fabric-DS-Blog) 
- [Blog over Synapse Data Warehousing-ervaring in Fabric](https://aka.ms/Fabric-DW-Blog) 
- [Blog over Synapse Real-Time Analytics-ervaring in Fabric](https://aka.ms/Fabric-RTA-Blog)
- [Blog over Power BI-aankondiging](https://aka.ms/Fabric-PBI-Blog)
- [Blog over Data Activator-ervaring in Fabric](https://aka.ms/Fabric-DA-Blog) 
- [Blog over beheer en governance in Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)
- [OneLake](https://aka.ms/Fabric-OneLake-Blog)[ in Fabric-blog](https://aka.ms/Fabric-OneLake-Blog)
- [Blog over Dataverse- en Microsoft Fabric-integratie](https://aka.ms/Dataverse-Fabric-Blog)

© 2023 Microsoft Corporation. Alle rechten voorbehouden.

Door gebruik te maken van deze demo/dit lab, gaat u akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met als doel uw feedback te verzamelen en u een leerervaring te bieden. U mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback aan Microsoft te geven. U mag het niet voor enig ander doel gebruiken. U mag deze demo/dit lab of een deel daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN DEEL DAARVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE TEN BEHOEVE VAN VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARETECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN GEPRESENTEERD, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DE MANIER WAAROP EEN DEFINITIEVE VERSIE KAN WERKEN. WIJ KUNNEN OOK GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UITBRENGEN. UW ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK AFWIJKEN.

**FEEDBACK**

Als u feedback geeft over de technologiefuncties, -functionaliteit en/of concepten die in deze demo/dit lab worden beschreven aan Microsoft, geeft u Microsoft, zonder enige vergoeding, het recht om uw feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, te delen en te commercialiseren. U geeft aan derden ook, zonder enige vergoeding, eventuele patentrechten die nodig zijn voor hun producten, technologieën en diensten om bepaalde onderdelen van een Microsoft-software of -dienst die de feedback bevat te gebruiken of ermee te communiceren. U geeft geen feedback die onderworpen is aan een licentie die vereist dat Microsoft zijn software of documentatie aan derden in licentie geeft omdat wij uw feedback daarin opnemen. Deze rechten blijven van kracht na beëindiging van deze overeenkomst.

_MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, INCLUSIEF ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, ONGEACHT OF DEZE UITDRUKKELIJK, IMPLICIET OF WETTELIJK ZIJN, GESCHIKTHEID VOOR EEN BEPAALD DOEL, TITEL EN NIET-INBREUK. MICROSOFT DOET GEEN TOEZEGGINGEN OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, OUTPUT DIE VOORTVLOEIT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR ENIG DOEL._

**DISCLAIMER**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen wijzigen in toekomstige releases van het product. In deze demo/dit lab leert u over enkele, maar niet alle, nieuwe functies.
