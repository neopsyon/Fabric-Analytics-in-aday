# Microsoft Fabric - Fabric Analyst in a Day - Lab 2

# ![](../media/2-1.png)

# Inhoudsopgave

  * Introductie

  * Fabric-licentie

      * Taak 1: Een Microsoft Fabric-proeflicentie inschakelen

  * Overzicht van Fabric Experiences:

      * Taak 2: Data Factory Experience
  
      * Taak 3: Data Activator Experience
     
      * Taak 4: Industry Solutions Experience

      * Taak 5: Synapse Data Engineering Experience
  
      * Taak 6: Synapse Data Science Experience
  
      * Taak 7: Synapse Data Warehouse Experience
  
      * Taak 8: Real-Time Analytics Experience

  * Fabric Workspace

      * Taak 9: Een Fabric Workspace aanmaken
  
      * Taak 10: Een Lakehouse aanmaken

  * Referenties

# Introductie
Vandaag leert u over diverse belangrijke functies van Microsoft Fabric. Dit is een inleidende workshop die bedoeld is om u kennis te laten maken met de verschillende product experiences en items die beschikbaar zijn in Fabric. Aan het einde van deze workshop weet u hoe u Lakehouse, Dataflow Gen2, Data Pipeline en DirectLake gebruikt.

Aan het einde van dit lab heeft u het volgende geleerd: 

  - Hoe u een Fabric workspace aanmaakt
  - Hoe u een Lakehouse aanmaakt  

# Fabric-licentie
### Taak 1: Een Microsoft Fabric-proeflicentie inschakelen

1. Open de **browser** en navigeer naar https://app.powerbi.com/. U wordt doorgestuurd naar de inlogpagina.

    >**Opmerking:** Als u geen gebruik maakt van de lab-omgeving en al een bestaand Power BI-account heeft, kunt u de browser in privé- of incognitomodus gebruiken.
    
1. Voer de **Gebruikersnaam** in die beschikbaar is op het tabblad **Environment Variables** (naast de Lab Guide) als e-mailadres en klik op **Submit**.  

    ![](../media/2-2.png)

1. U wordt doorgestuurd naar het scherm **Wachtwoord**. Voer het **Wachtwoord** in dat beschikbaar is op het tabblad **Environment Variables** (naast de Lab Guide) en dat door de instructeur met u is gedeeld. 

1. Klik op **Sign in** en volg de aanwijzingen om in te loggen bij Fabric.

   ![](../media/2-3.png)

1. U wordt doorgestuurd naar de bekende **Power BI Service Home page**.
1. We gaan ervan uit dat u bekend bent met de indeling van Power BI Service. Als u vragen heeft, aarzel dan niet om de instructeur te raadplegen.

    Op dit moment bevindt u zich in **My Workspace**. Om met Fabric-items te werken, heeft u een proeflicentie en een workspace met een Fabric-licentie nodig. Laten we dit instellen.

1. Selecteer in de rechterbovenhoek van het scherm het **gebruikerspictogram**.

1. Selecteer **Start trial**.

    ![](../media/2-4.png)
  
1. Het dialoogvenster Upgrade to a free Microsoft Fabric trial wordt geopend. Selecteer **Start trial**.

    ![](../media/2-5.png)

1. Selecteer de **"X"** in de rechterbovenhoek van het dialoogvenster **Just one last step** om het te sluiten. We zullen deze gegevens niet invullen, omdat dit een lab-omgeving betreft.

    ![](../media/2-6.png)

1. Het dialoogvenster Successfully upgraded to a free Microsoft Fabric trial wordt geopend. Selecteer **Fabric Home Page**. 

    ![](../media/2-7.png)

1. U wordt doorgestuurd naar de **Microsoft Fabric Home page**.

    ![](../media/2-8.png)

# Overzicht van Fabric Experiences:

### Taak 2: Data Factory Experience

1. Selecteer het pictogram **Microsoft Fabric** (fabric experience selector) linksonder op uw scherm. Er wordt een dialoogvenster geopend met de lijst van Fabric experiences. Merk op dat Power BI, Data Factory, Data Activator en Industry Solutions onafhankelijke experiences zijn. Data Engineering, Data Science, Data Warehouse en Real-Time Analytics zijn Synapse experiences en deze vier experiences worden aangedreven door Synapse. Laten we dit verkennen.

1. Selecteer **Data Factory**.
 
    ![](../media/2-9.png)

1. U wordt doorgestuurd naar de **Data Factory Home page**. De pagina bevat drie hoofdsecties.
   
    1. **New:** Hier staan de items die beschikbaar zijn in Data Factory – Dataflow Gen2 en Data pipeline.

         1. Dataflow Gen2 is de volgende generatie van Dataflow.

         1. Een data pipeline wordt gebruikt voor data-orkestratie.
            
    2. **Recommended**: Deze sectie biedt toegang tot snelstartdocumentatie.
       
    3. **Quick Access**: In deze sectie staan de recent gebruikte of favoriete items.

        ![](../media/2-10.png)

### Taak 3: Data Activator Experience

1. Selecteer **Data Factory** linksonder op uw scherm. Het dialoogvenster Fabric experience wordt geopend.

    ![](../media/2-11.png)

2. Selecteer **Data Activator** in het dialoogvenster. U wordt doorgestuurd naar de **Data Activator Home page**. Data Activator is een no-code experience in Microsoft Fabric voor het automatisch uitvoeren van acties wanneer patronen of condities worden gedetecteerd in veranderende data. Merk op dat de drie secties vergelijkbaar zijn met de Data Factory experience. In de sectie New ziet u de volgende items:
    
    1. **Reflex:** Gebruikt om datasets, queries en event streams te monitoren op patronen.
    
    1. **Reflex sample:** Voorbeeldoplossing.

        ![](../media/2-12.png)

### Taak 4: Industry Solutions Experience
1. Selecteer het pictogram Fabric Experience selector (momenteel ingesteld op Data Activator) linksonder op uw scherm. Het dialoogvenster Fabric experience wordt geopend.

2. Selecteer Industry Solutions in het dialoogvenster. U wordt doorgestuurd naar de Industry Solutions Home page. Microsoft Fabric biedt branchespecifieke data-oplossingen die een robuust platform vormen voor gegevensbeheer, analytics en besluitvorming. Deze data-oplossingen spelen in op de unieke uitdagingen van verschillende branches, waardoor bedrijven hun activiteiten kunnen optimaliseren, data uit verschillende bronnen kunnen integreren en uitgebreide analytics kunnen gebruiken. Merk op dat de drie secties vergelijkbaar zijn met de voorgaande experiences. In de sectie New ziet u de volgende items:
    
    1. **Sustainability solutions:** ondersteunt de opname, standaardisatie en analyse van Environmental, Social, and Governance (ESG)-data.
    
    1. **Retail solutions:** helpt bij het beheren van grote hoeveelheden data, het integreren van data uit verschillende bronnen en het bieden van real-time analytics voor snelle besluitvorming. Retailers kunnen deze oplossingen gebruiken voor voorraadbeheeroptimalisatie, klantsegmentatie, verkoopprognoses, dynamische prijsstelling en fraudedetectie.

       ![](../media/2-13.png)

### Taak 5: Synapse Data Engineering Experience

1. Selecteer **Industry Solutions** linksonder op uw scherm. Het dialoogvenster Fabric experience wordt geopend.

2. Selecteer **Data Engineering**. U wordt doorgestuurd naar de **Synapse Data Engineering Home page**. De pagina bevat wederom drie hoofdsecties. In de sectie New ziet u de volgende items: 
   
   1. **Lakehouse:** Gebruikt om big data op te slaan voor opschoning, querying, rapportage en delen.
   
   1. **Notebook:** Gebruikt voor data-opname, -voorbereiding, -analyse en andere datagerelateerde taken met behulp van verschillende talen zoals Python, R en Scala.
   
   1. **Environment:** Gebruikt om gedeelde bibliotheken, spark compute-instellingen en resources voor notebooks en spark job definitions in te stellen.
   
   1. **Spark Job Definition:** Gebruikt om Apache-jobs te definiëren, plannen en beheren.
   
   1. **Data pipeline:** Gebruikt om data-oplossingen te orkestreren.
   
   1. **Import notebook:** Gebruikt om notebooks van een lokale machine te importeren.
   
   1. **Use a sample:** Gebruikt om een voorbeeld aan te maken.

      ![](../media/2-14.png)

### Taak 6: Synapse Data Science Experience

1. Selecteer het pictogram **Fabric experience selector** (momenteel ingesteld op Data Engineering) linksonder op uw scherm. Het dialoogvenster Fabric experience wordt geopend.

2. Selecteer **Data Science**. U wordt doorgestuurd naar de **Data Science Home page**. Er zijn wederom drie secties. In de sectie New ziet u de volgende items:
    
    1. **ML model:** Gebruikt om machine learning-modellen te maken.
    
    1. **Experiment:** Gebruikt om de ontwikkeling van meerdere modellen te maken, uit te voeren en bij te houden.
    
    1. **Notebook**: Gebruikt om data te verkennen en machine learning-oplossingen te bouwen.
    
    1. **Environment(Preview)**: Gebruikt om gedeelde bibliotheken, spark compute-instellingen en resources voor notebooks en spark job definitions in te stellen.
    
    1. **Import Notebook:** Gebruikt om notebooks van een lokale machine te importeren.
    
    1. **Use a Sample:** Voorbeeldoplossing.

   >**Opmerking**: Items zoals Notebook, Environment, Data pipeline, enzovoort zijn beschikbaar in meerdere experiences, omdat ze relevant zijn in elk van deze experiences.

    # ![](../media/2-15.png)

### Taak 7: Synapse Data Warehouse Experience

1. Selecteer het pictogram **Fabric experience selector** (momenteel ingesteld op Data Science) linksonder op uw scherm. Het dialoogvenster Fabric experience wordt geopend.

2. Selecteer **Data Warehouse**. U wordt doorgestuurd naar de **Synapse Data Warehouse Home page**. Er zijn wederom drie secties. In de sectie New ziet u de items. Merk op dat Data Pipeline en Dataflow Gen2 hier ook beschikbaar zijn.

   1. **Warehouse:** Gebruikt om strategische inzichten te bieden vanuit meerdere bronnen.
   
   1. **Data pipeline:** Gebruikt om data-oplossingen te orkestreren.

      ![](../media/2-16.png)

### Taak 8: Real-Time Analytics Experience

1. Selecteer het pictogram **Fabric experience selector** (momenteel ingesteld op Data Warehouse) linksonder op uw scherm. Het dialoogvenster Fabric experience wordt geopend.

2. Selecteer **Real-Time Analytics**. U wordt doorgestuurd naar de **Real-Time Analytics Home page**. Er zijn wederom drie secties. In de sectie New ziet u de volgende items:
   
   1. **Eventhouse(Preview):** Gebruikt om een workspace van de database aan te maken die over projecten heen gedeeld kan worden.
   
   1. **KQL Database:** Gebruikt om gestructureerde, ongestructureerde en streamingdata snel te laden voor querying.
   
   1. **KQL Queryset:** Gebruikt om queries op de data uit te voeren en deelbare tabellen en visuals te produceren.
   
   1. **Eventstream:** Gebruikt om real-time event streams vast te leggen, te transformeren en te routeren.
   
   1. **Use a sample:** Gebruikt om een voorbeeld aan te maken.

      ![](../media/2-17.png)

# Fabric Workspace

### Taak 9: Een Fabric Workspace aanmaken

1. Laten we nu een workspace aanmaken met een Fabric-licentie. Selecteer **Workspaces** in de linkernavigatiebalk. Er wordt een dialoogvenster geopend.
2. Selecteer **+ New workspace**.

    # ![](../media/2-18.png)

3. Het dialoogvenster **Create a workspace** wordt aan de rechterkant van de browser geopend.
4. Voer in het veld **Name** de naam **FAIAD_username** in.

    >**Opmerking:** De naam van de workspace moet uniek zijn. In dit document gebruiken we FAIAD als workspacenaam. Uw workspacenaam moet echter anders zijn. Controleer of er een groen vinkje met de tekst **This name is available** wordt weergegeven onder het veld Name.
   
6. Als u wilt, kunt u een **Description** voor de workspace invoeren. Dit is een optioneel veld.
7. Klik op **Advanced** om de sectie uit te vouwen.

    # ![](../media/2-19.png)

8. Zorg er onder **License mode** voor dat **Trial** is geselecteerd. (Dit is standaard geselecteerd.)
9. Selecteer **Apply** om een nieuwe workspace aan te maken.

   # ![](../media/2-20.png)

    Er wordt een nieuwe workspace aangemaakt en u wordt naar deze workspace doorgestuurd. We brengen data uit de verschillende databronnen in de Lakehouse en gebruiken de data vanuit de Lakehouse om ons model te bouwen en er rapporten over te maken. De eerste stap is het aanmaken van een Lakehouse.

### Taak 10: Een Lakehouse aanmaken

1. Selecteer het pictogram **Fabric experience selector** (momenteel ingesteld op Real-Time Analytics) linksonder op uw scherm. Het dialoogvenster Fabric experience wordt geopend.

    # ![](../media/2-21.png)

1. Selecteer **Data Engineering** om naar de Data Engineering Home page te navigeren.
1. Selecteer **Lakehouse**.

    # ![](../media/2-22.png)

1. Het dialoogvenster New lakehouse wordt geopend. Typ **lh_FAIAD** in het tekstvak Name.
 
    >**Opmerking:** lh verwijst hier naar Lakehouse. We gebruiken het voorvoegsel lh zodat het gemakkelijk te herkennen en te zoeken is.
    
1. Selecteer **Create**.

   # ![](../media/2-23.png)

      Binnen enkele ogenblikken wordt er een Lakehouse aangemaakt en wordt u doorgestuurd naar de Lakehouse-interface. Op het **linker paneel** ziet u dat onder uw workspace het Lakehouse-pictogram wordt weergegeven. U kunt op elk moment eenvoudig naar de Lakehouse navigeren door op dit pictogram te klikken.

      In de Lakehouse Explorer ziet u **Tables** en **Files**. De Lakehouse kan Azure Data Lake Storage Gen2-bestanden beschikbaar stellen via de sectie Files, of een dataflow kan data laden naar Lakehouse-tabellen. Er zijn diverse opties beschikbaar. In de volgende labs laten we u een aantal van de opties zien.

    # ![](../media/2-24.png)

      In dit lab hebben we de Fabric-interface verkend en een Fabric workspace en een Lakehouse aangemaakt. In het volgende lab leren we hoe u Dataflow Gen2 gebruikt om verbinding te maken met ADLS Gen2 om data te extraheren, transformeren en in de Lakehouse te laden.

# Referenties
Fabric Analyst in a Day (FAIAD) introduceert u in een aantal van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service bevat de sectie Help (?) links naar uitstekende resources.

   # ![](../media/img18.png)

Hier zijn nog enkele resources die u helpen bij uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [Microsoft Fabric GA-aankondiging](https://aka.ms/Fabric-Hero-Blog-Ignite23)
- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)
- Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)
- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)
- Leer nieuwe vaardigheden door de [Fabric Learning-modules](https://aka.ms/learn-fabric) te verkennen
- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)
- Lees het [gratis e-book over het aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om uw vragen te stellen, feedback te delen en van anderen te leren

Lees de uitgebreidere aankondigingsblogs per Fabric experience:

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

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met het doel uw feedback te verzamelen en u een leerervaring te bieden. U mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback te geven aan Microsoft. U mag het niet voor enig ander doel gebruiken. U mag deze demo/dit lab of een deel daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN DEEL DAARVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE TEN BEHOEVE VAN VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.
DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARETECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN GEPRESENTEERD, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DEZELFDE MANIER ALS EEN DEFINITIEVE VERSIE. WIJ KUNNEN OOK BESLUITEN GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UIT TE BRENGEN. UW ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK VERSCHILLEN.

**FEEDBACK**

Als u feedback geeft over de technologiefuncties, -functionaliteit en/of -concepten die in deze demo/dit lab worden beschreven aan Microsoft, verleent u Microsoft kosteloos het recht om uw feedback op welke wijze en voor welk doel dan ook te gebruiken, te delen en commercieel te exploiteren. U verleent ook aan derden, kosteloos, eventuele octrooirechten die nodig zijn voor hun producten, technologieën en diensten om specifieke onderdelen van een Microsoft-software of -service te gebruiken of te koppelen die de feedback bevat. U geeft geen feedback die onderworpen is aan een licentie die Microsoft verplicht zijn software of documentatie aan derden in licentie te geven omdat wij uw feedback daarin opnemen. Deze rechten blijven van kracht na beëindiging van deze overeenkomst.

_MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, INCLUSIEF ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, UITDRUKKELIJK, IMPLICIET OF WETTELIJK, GESCHIKTHEID VOOR EEN BEPAALD DOEL, TITEL EN NIET-INBREUK. MICROSOFT GEEFT GEEN VERZEKERINGEN OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE OUTPUT DIE VOORTVLOEIT UIT HET GEBRUIK VAN DEMO/LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR ENIG DOEL._

**DISCLAIMER**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen veranderen in toekomstige versies van het product. In deze demo/dit lab leert u over enkele, maar niet alle, nieuwe functies.
