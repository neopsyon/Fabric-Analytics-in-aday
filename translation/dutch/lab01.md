# Microsoft Fabric - Fabric Analyst in a Day - Lab 1

# ![](../media/new1.png)

# Inhoudsopgave
- Documentstructuur
- Scenario / Probleemstelling
- Overzicht van het Power BI Desktop-rapport
   - Taak 1: Power BI Desktop instellen in de labomgeving
   - Taak 2: Het Power BI Desktop-rapport analyseren
   - Taak 3: Power Queries bekijken
- Referenties

# Documentstructuur
Het lab bevat stappen die de gebruiker kan volgen, aangevuld met bijbehorende schermafbeeldingen als visuele ondersteuning. In elke schermafbeelding zijn secties gemarkeerd met oranje kaders om aan te geven op welk gebied of welke gebieden de gebruiker zich moet richten.

# Scenario / Probleemstelling
Fabrikam, Inc. is een groothandelaar in novelty-artikelen. Als groothandelaar zijn Fabrikam's klanten voornamelijk bedrijven die doorverkopen aan particulieren. Fabrikam verkoopt aan retailklanten door heel de Verenigde Staten, waaronder speciaalzaken, supermarkten, computerwinkels en souvenirwinkels bij toeristische attracties. Fabrikam verkoopt ook aan andere groothandelaren via een netwerk van agenten die de producten namens Fabrikam promoten. Hoewel alle klanten van Fabrikam momenteel in de Verenigde Staten zijn gevestigd, is het bedrijf van plan om uit te breiden naar andere landen/regio's.

U bent een Data Analyst in het salesteam. U verzamelt, schoont en interpreteert datasets om bedrijfsproblemen op te lossen. U maakt ook visualisaties zoals grafieken en diagrammen, schrijft rapporten en presenteert deze aan de besluitvormers binnen de organisatie.

Om waardevolle inzichten uit de data te halen, haalt u gegevens op uit meerdere systemen, schoont u deze op en combineert u ze. U haalt gegevens op uit de volgende bronnen:

- **Verkoopdata:** afkomstig uit het ERP-systeem; de data is opgeslagen in een ADLS Gen2-database of Databricks. Deze wordt elke dag om 12:00 uur bijgewerkt.
- **Leveranciersdata:** afkomstig van verschillende leveranciers; de data is opgeslagen in een Snowflake-database. Deze wordt elke dag om middernacht / 00:00 uur bijgewerkt.
- **Klantdata:** afkomstig uit Customer Insights; de data is opgeslagen in Dataverse. De data is altijd actueel.
- **Medewerkerdata:** afkomstig uit het HR-systeem; opgeslagen als exportbestand in een SharePoint-map. Deze wordt elke ochtend om 09:00 uur bijgewerkt.

     ![Picture1FAID](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/e236d8ac-890d-4f7b-93f5-e8d163e3b878)
  
U bouwt momenteel een dataset in Power BI Premium die de gegevens uit de bovenstaande bronsystemen ophaalt om te voldoen aan uw rapportagebehoeften en om eindgebruikers de mogelijkheid te bieden zelf analyses uit te voeren. U gebruikt Power Query om uw model bij te werken.

**U staat voor de volgende uitdagingen:**
   - U moet uw dataset minimaal drie keer per dag vernieuwen om rekening te houden met de verschillende bijwerktijden van de verschillende databronnen.
   - Uw vernieuwingen nemen veel tijd in beslag, omdat u elke keer een volledige vernieuwing moet uitvoeren om eventuele wijzigingen in de bronsystemen te registreren.
   - Fouten in een van de databronnen waaruit u gegevens ophaalt, zorgen ervoor dat de vernieuwing van uw dataset mislukt. Vaak wordt het medewerkersbestand niet op tijd geüpload, waardoor de vernieuwing van uw dataset mislukt.
   - Het duurt erg lang om wijzigingen in uw datamodel aan te brengen, omdat Power Query veel tijd nodig heeft om de previews te vernieuwen vanwege de grote datavolumes en complexe transformaties.
   - U heeft een Windows-pc nodig om Power BI Desktop te gebruiken, terwijl de bedrijfsstandaard Mac is.

U heeft gehoord over Microsoft Fabric en besloten het uit te proberen om te zien of het uw uitdagingen aanpakt.

# Overzicht van het Power BI Desktop-rapport
Voordat we beginnen met Fabric, bekijken we het huidige rapport in Power BI Desktop om de transformaties en het model te begrijpen.
### Taak 1: Power BI Desktop instellen in de labomgeving
1. Open het **FAIAD.pbix**-bestand in de map **Report** op het **bureaublad** van uw labomgeving. Het bestand wordt geopend in Power BI Desktop.

      ![Picture2FAID](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/ce64a7c3-6bb5-45d0-8ced-fc923145805c)

3. Het dialoogvenster voor het invoeren van uw e-mailadres wordt geopend. Navigeer naar het tabblad **Environment Details** in het rechterpaneel van de labomgeving.
4. Kopieer de **Username Credentials** en plak deze in het tekstvak E-mail van het dialoogvenster.
5. Selecteer **Continue**.
 
      ![Picture3FAID](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/ab7ccb1c-d41b-41c3-86e6-baccf6506361)
   
7. Het dialoogvenster om u aan te melden wordt geopend. Selecteer **Work or school account**.
8. Selecteer **Continue**.

      ![Picture4FAID](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/d1908a37-3197-4c08-9fe6-73dfcb91f997)
   
10. Het aanmeldingsvenster wordt geopend. Voer de **Username Credentials** opnieuw in door deze te kopiëren uit het tabblad **Environment Details**.
11. Selecteer **Next**.
    
       ![Picture5FAID](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/a3931a21-f2a9-48bd-8807-306f300a4c45)

12. Voer in het volgende dialoogvenster de **Password Credentials** opnieuw in door deze te kopiëren uit het tabblad **Environment Details**.
13. Selecteer **Sign in**.
14. Het dialoogvenster Actie vereist wordt geopend met het verzoek multifactorauthenticatie in te stellen. Dit hoeven we niet in te stellen, aangezien dit een labomgeving is. Selecteer **Ask Later**.
    
     ![Picture6FAID](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/999ecb8b-4854-4a3a-84f3-bd85e3daa77b)
    
15. Selecteer **No, sign in the app** only in het volgende dialoogvenster. Power BI Desktop wordt nu geopend.

### Taak 2: Het Power BI Desktop-rapport analyseren
   Het onderstaande rapport analyseert de verkoop voor Fabrikam. KPI's staan linksboven op de pagina vermeld. De overige visuals tonen de verkoop over tijd, per Territory, Product Group en Reseller Company.
   
   ![Picture7FAID](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/1ad8a0d4-5f3b-4dd4-ab15-9b6212a92de8)
     
   **Opmerking:** In deze training richten we ons op gegevensverzameling, transformatie en modellering met behulp van tools die beschikbaar zijn in Fabric. We richten ons niet op rapportontwikkeling of navigatie. Laten we een paar minuten de tijd nemen om het rapport te begrijpen en daarna verdergaan met de volgende stappen.

1. Laten we de data analyseren per Sales Territory. Selecteer **New England in het Sales Territory**-visual (spreidingsdiagram).
Merk op in het visual Sales over time dat Reseller Tailspin Toys meer verkopen heeft dan Wingtip Toys in New England. Als u kijkt naar het kolomdiagram Sales YoY% zult u zien dat de omzetgroei van Wingtip Toys laag is geweest en kwartaal na kwartaal is gedaald gedurende het afgelopen jaar. Na een klein herstel in Q3 daalde het opnieuw in Q4.

    ![Picture8FAID](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/b3f38036-16cb-4896-a851-7ff0aefc7c0d)
   
3. Laten we dit vergelijken met het territorium Rocky Mountain. Selecteer **Rocky Mountain in het Sales Territory**-visual (spreidingsdiagram).
Merk op in het kolomdiagram Sales YoY% dat de verkopen van Wingtip Toys dramatisch zijn gestegen in 2022 Q4, na een lage periode in de twee voorafgaande kwartalen.

      ![Picture9FAID](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/ac85d3d3-3aff-4229-aaf3-302c0dc07506)
   
4. Selecteer **Rocky Mountain in het Sales Territory** om het filter te verwijderen.
5. Selecteer in het spreidingsdiagramvisual onderaan het midden van het scherm (Sales Orders by Sales) de outlier rechtsboven (4e kwadrant).
Merk op dat het marge-% 52% is, wat boven het gemiddelde van 50% ligt. Ook is de Sales YoY% gestegen in de laatste twee kwartalen van 2022.

      ![Picture10FAID](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/f0fc3e03-dcd3-47c6-9a34-a5bbd5d196b8)

5. Selecteer de outlier Reseller in het spreidingsdiagramvisual om **het filter te verwijderen**.
6. Laten we de productdetails bekijken per Product Group en Reseller. Klik in het staafdiagramvisual Sales by Product Group and Reseller Company met de **rechtermuisknop op de balk Packaging Materials voor Tailspin Toys** en selecteer in het dialoogvenster **Drill through -> Product Detail**.

      ![Picture11FAID](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/6b27ccc9-bc40-43b1-a447-0ded3660642c)

   U wordt doorgestuurd naar de pagina met de productdetails. Merk op dat er ook toekomstige orders zijn geplaatst.
7. Wanneer u klaar bent met het bekijken van deze pagina, selecteert u de **Ctrl+pijl-terug** rechtsboven op de pagina om terug te navigeren naar het Sales-rapport.
      
    ![Picture12FAID](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/6ff10b89-9d8f-4b2b-bf76-be3d2c1608ab)

8. Analyseer het rapport gerust verder. Als u klaar bent, bekijken we de modelweergave. Selecteer in het linkerpaneel het **Model view icon**. U ziet dat er twee feitentabellen zijn: Sales en PO.

      1. De granulariteit van de Sales-data is op Date, Reseller, Product en People. Date, Reseller, Product en People zijn gekoppeld aan Sales.
      2. De granulariteit van de PO-data is op Date, Product en People. Date, Product en People zijn gekoppeld aan PO.
      3. We hebben Supplier-data per Product. Supplier is gekoppeld aan Product.
      4. We hebben locatiedata van Resellers per Geo. Geo is gekoppeld aan Reseller.
      5. We hebben klantinformatie per Reseller. De klant is gekoppeld aan Reseller.

### Taak 3: Power Queries bekijken
1. Laten we Power Query bekijken om de databronnen te begrijpen. Selecteer in het lint **Home -> Transform data**.

      ![Picture13FAID](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/fbfb74a2-d328-4a18-bb6a-7e6fec6d2f82)

2. Het Power Query-venster wordt geopend. Selecteer in het lint **Home -> Data source settings**. Het dialoogvenster voor gegevensbronsinstellingen wordt geopend. Terwijl u door de lijst scrolt, ziet u dat er vier hoofdbronnen zijn zoals vermeld in de probleemstelling:

      1. Snowflake
      2. SharePoint
      3. ADLS Gen2
      4. Dataverse

4. Selecteer **Close** om het dialoogvenster Data source settings te sluiten.

    ![](../media/new12.png)

5. In het linker Queries-paneel ziet u dat de queries zijn gegroepeerd per databron.
6. Merk op dat de map **DataverseData** klantdata bevat in vier verschillende queries: BabyBoomer, GenX, GenY en GenZ. Deze vier queries worden samengevoegd om een Customer-query te maken.

    ![Picture15](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/7b261b69-164a-4ed1-9cba-bf0839969f77)

1. U kunt de inloggegevens voor de Dataverse-databron invoeren door de **Username** en **Password** in te voeren die beschikbaar zijn op het tabblad **Environment Variables** (naast de Lab Guide). Selecteer de Microsoft account-optie.

      ![](../media/new2.png)

1. Gebruik voor de ADLS-databron de optie **Account Key** en voer de **Adls storage account Access key** in die beschikbaar is op het tabblad **Environment Variables** (naast de Lab Guide).

1. Merk op dat de map **ADLSData** meerdere dimensies bevat: Geo, Product, Reseller en Date. Het bevat ook Sales-feiten.
   
   1. De **Geo-dimensie** is gemaakt door data samen te voegen uit de queries Cities, Countries en States.
   2. De **Product-dimensie** is gemaakt door data samen te voegen uit de queries Product Groups en Product Item Group.
   3. De **Reseller-dimensie** wordt gefilterd met behulp van de BuyingGroup-query.
   4. Het **Sales-feit** is gemaakt door InvoiceLineItems samen te voegen met de Invoice-query.

1. Gebruik voor de ADLS-databron de optie **Account Key** en voer de **Adls storage account Access key** in die beschikbaar is op het tabblad **Environment Variables** (naast de Lab Guide).

1. Merk op dat de map **SnowflakeData** een Supplier-dimensie en een PO-feit (Order / Besteding) bevat.

   1. De **Supplier-dimensie** is gemaakt door de Suppliers-query samen te voegen met de SupplierCategories-query.
   2. Het **PO-feit** is gemaakt door PO samen te voegen met de query PO Line Items.

1. Voer voor de SharePoint-databron de **Username** en **Password** in die beschikbaar zijn op het tabblad **Environment Variables** (naast de Lab Guide). Selecteer de Microsoft account-optie.

1. Merk op dat de map **SharepointData** een People-dimensie bevat.

   ![](../media/new3.png)

Nu weten we waar we mee te maken hebben. In de volgende labs maken we een vergelijkbare Power Query met Dataflow Gen2 en een model met Lakehouse.

# Referenties
Fabric Analyst in a Day (FAIAD) maakt u kennis met enkele van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service vindt u in de Help (?)-sectie links naar een aantal uitstekende resources.

   ![Picture16](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/13178b86-b21e-4cd1-b34f-4ce4682d1de8)

Hier zijn nog een aantal resources die u helpen bij uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [aankondiging van Microsoft Fabric GA](https://aka.ms/Fabric-Hero-Blog-Ignite23)
- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)
- Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)
- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)
- Leer nieuwe vaardigheden door de [Fabric Learning modules](https://aka.ms/learn-fabric) te verkennen
- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)
- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om uw vragen te stellen, uw feedback te delen en van anderen te leren

Lees de meer gedetailleerde aankondigingsblogs over de Fabric-ervaringen:

- [Blog over de Data Factory-ervaring in Fabric](https://aka.ms/Fabric-Data-Factory-Blog) 
- [Blog over de Synapse Data Engineering-ervaring in Fabric](https://aka.ms/Fabric-DE-Blog) 
- [Blog over de Synapse Data Science-ervaring in Fabric](https://aka.ms/Fabric-DS-Blog) 
- [Blog over de Synapse Data Warehousing-ervaring in Fabric](https://aka.ms/Fabric-DW-Blog) 
- [Blog over de Synapse Real-Time Analytics-ervaring in Fabric](https://aka.ms/Fabric-RTA-Blog)
- [Aankondigingsblog van Power BI](https://aka.ms/Fabric-PBI-Blog)
- [Blog over de Data Activator-ervaring in Fabric](https://aka.ms/Fabric-DA-Blog) 
- [Blog over beheer en governance in Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)
- [OneLake](https://aka.ms/Fabric-OneLake-Blog)[ in Fabric blog](https://aka.ms/Fabric-OneLake-Blog)
- [Blog over de integratie van Dataverse en Microsoft Fabric](https://aka.ms/Dataverse-Fabric-Blog)

© 2023 Microsoft Corporation. Alle rechten voorbehouden.

Door gebruik te maken van deze demo/dit lab stemt u in met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met als doel uw feedback te verkrijgen en u een leerervaring te bieden. U mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback te geven aan Microsoft. U mag het niet voor enig ander doel gebruiken. U mag deze demo/dit lab of een deel daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, er afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN DEEL DAARVAN) NAAR EEN ANDERE SERVER OF LOCATIE VOOR VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARE-TECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN WEERGEGEVEN, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DE MANIER WAAROP EEN DEFINITIEVE VERSIE ZAL WERKEN. WE KUNNEN OOK BESLUITEN GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UIT TE BRENGEN. UW ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK ANDERS ZIJN.

**FEEDBACK**. Als u feedback geeft over de technologiefuncties, functionaliteit en/of concepten die in deze demo/dit lab worden beschreven aan Microsoft, geeft u Microsoft, kosteloos, het recht om uw feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, te delen en te commercialiseren. U geeft ook aan derden, kosteloos, alle patentrechten die nodig zijn voor hun producten, technologieën en diensten om bepaalde onderdelen van een Microsoft-software of -service die de feedback bevat, te gebruiken of te koppelen. U geeft geen feedback die onderworpen is aan een licentie die Microsoft verplicht zijn software of documentatie in licentie te geven aan derden omdat we uw feedback daarin opnemen. Deze rechten blijven van kracht na beëindiging van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN AF MET BETREKKING TOT DE DEMO/HET LAB, INCLUSIEF ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, ONGEACHT OF DEZE UITDRUKKELIJK, IMPLICIET OF WETTELIJK ZIJN, GESCHIKTHEID VOOR EEN BEPAALD DOEL, TITEL EN NIET-INBREUK. MICROSOFT GEEFT GEEN VERZEKERINGEN OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE OUTPUT DIE VOORTKOMT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR ENIG DOEL.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen wijzigen in toekomstige versies van het product. In deze demo/dit lab leert u over enkele, maar niet alle, nieuwe functies.
