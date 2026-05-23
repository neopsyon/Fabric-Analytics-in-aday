# Microsoft Fabric - Fabric Analyst in a Day - Lab 2

# ![](../media/new4.png)

# Inhoudsopgave

  * Inleiding

  * Fabric-licentie

      * Taak 1: Een Microsoft Fabric-proeflicentie activeren

  * Overzicht van Fabric-ervaringen:

      * Taak 2: Data Factory Experience
  
      * Taak 3: Data Activator Experience
  
      * Taak 4: Synapse Data Engineering Experience
  
      * Taak 5: Synapse Data Science Experience
  
      * Taak 6: Synapse Data Warehouse Experience
  
      * Taak 7: Real-Time Analytics Experience

  * Fabric Workspace

      * Taak 8: Een Fabric Workspace aanmaken
  
      * Taak 9: Een Lakehouse aanmaken

  * Referenties

# Inleiding
Vandaag leert u over diverse belangrijke functies van Microsoft Fabric. Dit is een inleidende workshop bedoeld om u kennis te laten maken met de verschillende product-ervaringen en items die beschikbaar zijn in Fabric. Aan het einde van deze workshop leert u hoe u de functies Lakehouse, Dataflow Gen2, Data Pipeline en DirectLake gebruikt.

Aan het einde van dit lab hebt u geleerd:

  - Hoe u een Fabric workspace aanmaakt
  - Hoe u een Lakehouse aanmaakt

# Fabric-licentie
### Taak 1: Een Microsoft Fabric-proeflicentie activeren

1. Open de **browser** en navigeer naar https://app.powerbi.com/. U wordt doorgestuurd naar de inlogpagina.

    >**Opmerking:** Als u al een bestaand Power BI-account hebt, kunt u de browser in privé- of incognitomodus gebruiken.
    
1. Voer het **e-mailadres** in dat door de instructeur is verstrekt en klik op **Submit**.

   ![Picture17](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/3995afaf-cf69-4541-894e-b2b06ee8caf5)


1. U wordt doorgestuurd naar het scherm **Password**. Voer het wachtwoord in dat de instructeur met u heeft gedeeld.
1. Klik op **Sign in** en volg de instructies om in te loggen bij Fabric.

      ![Picture18](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/5428ffb9-7039-4fcc-818c-42fb5cf2b4f5)

1. U wordt doorgestuurd naar de vertrouwde **Power BI Service Home page**.
1. We gaan ervan uit dat u bekend bent met de indeling van Power BI Service. Als u vragen hebt, aarzel dan niet om de instructeur te raadplegen.

    Op dit moment bevindt u zich in **My Workspace**. Om met Fabric-items te kunnen werken, hebt u een proeflicentie en een workspace met een Fabric-licentie nodig. Laten we dat nu instellen.

1. Selecteer rechtsboven in het scherm het **gebruikerspictogram**.
1. Selecteer **Start trial**.

      ![Picture19](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/9f2a3001-5e81-4bed-8408-ec4287467842)
  
1. Het dialoogvenster "Upgrade to a free Microsoft Fabric trial" wordt geopend. Selecteer **Start trial**.

      ![Picture20](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/c910b821-9662-42a4-91f2-501ec2f81828)

1. Het dialoogvenster "Successfully upgraded to a free Microsoft Fabric trial" wordt geopend. Selecteer **Fabric Home Page**.

      ![Picture21](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/709b1a4e-5a75-4b40-b2ab-8d010e2a8dd4)

1. U wordt doorgestuurd naar de **Microsoft Fabric Home page**.

      ![Picture22](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/dc8dcdc9-8b10-4e09-8c70-67f22a47a7b3)

# Overzicht van Fabric-ervaringen:

### Taak 2: Data Factory Experience

1. Selecteer het pictogram **Microsoft Fabric** linksonder in uw scherm. Er wordt een dialoogvenster geopend met de lijst van Fabric-ervaringen. U ziet dat Power BI, Data Factory en Data Activator onafhankelijke ervaringen zijn. Data Engineering, Data Science, Data Warehouse en Real-Time Analytics zijn Synapse-ervaringen en deze vier ervaringen worden aangedreven door Synapse. Laten we verkennen.
  
3. Selecteer **Data Factory**.
 
      ![Picture23](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/793c431e-6942-4e80-9bc2-774f95e60eba)

4. U wordt doorgestuurd naar de **Data Factory Home page**. De pagina bevat drie hoofdsecties.
   
    1. **New:** Hier worden de beschikbare items in Data Factory weergegeven – Dataflow Gen2 en Data pipeline.

         1. Dataflow Gen2 is de volgende generatie van Dataflow.

         1. Een data pipeline wordt gebruikt voor data-orkestratie.
            
    2. **Recommended**: Deze sectie biedt toegang tot snelstartdocumentatie.
       
    3. **Quick Access**: Deze sectie toont de recent gebruikte of favoriete items.

   ![Picture24](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/4cfa0615-359d-47ad-b4f3-a5432201c44b)

### Taak 3: Data Activator Experience

1. Selecteer **Data Factory** linksonder in uw scherm. Het dialoogvenster voor Fabric-ervaringen wordt geopend.

   ![Picture25](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/98c00246-ad57-4b6a-873d-7e3527ad30df)

2. Selecteer **Data Activator** in het dialoogvenster. U wordt doorgestuurd naar de **Data Activator Home page**. Data Activator is een no-code-ervaring in Microsoft Fabric voor het automatisch uitvoeren van acties wanneer patronen of condities worden gedetecteerd in veranderende data. U ziet dat de drie secties vergelijkbaar zijn met de Data Factory-ervaring. In de sectie New ziet u de volgende items:
    1. **Reflex:** Gebruikt om datasets, queries en event streams op patronen te monitoren.
    1. **Reflex sample:** Voorbeeldoplossing.

        ![Picture26](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/b517d1b3-8fda-4df2-9a7a-8db844fb33c6)

### Taak 4: Synapse Data Engineering Experience

1. Selecteer **Data Activator** linksonder in uw scherm. Het dialoogvenster voor Fabric-ervaringen wordt geopend.
2. Selecteer **Data Engineering**. U wordt doorgestuurd naar de **Data Engineering Home page**. Ook hier bevat de pagina drie hoofdsecties. In de sectie New ziet u de volgende items:
   1. **Lakehouse:** Gebruikt voor het opslaan van big data ten behoeve van opschoning, querying, rapportage en delen.
   1. **Notebook:** Gebruikt voor het uitvoeren van queries op de data om deelbare tabellen en visuals te produceren.
   1. **Spark Job Definition:** Gebruikt voor het definiëren, plannen en beheren van Apache-jobs.
   1. **Data pipeline:** Gebruikt voor het orkestreren van data-oplossingen.
   1. **Import notebook:** Gebruikt voor het importeren van notebooks vanaf een lokale machine.
   1. **Use a sample:** Gebruikt voor het aanmaken van een voorbeeld.

   ![Picture27](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/19abeee2-ff05-49fd-8c93-974ede877f61)

### Taak 5: Synapse Data Science Experience

1. Selecteer **Data Engineering** linksonder in uw scherm. Het dialoogvenster voor Fabric-ervaringen wordt geopend.
2. Selecteer **Data Science**. U wordt doorgestuurd naar de **Data Science Home page**. Ook hier zijn drie secties aanwezig. In de sectie New ziet u de volgende items:
    1. **ML model:** Gebruikt voor het aanmaken van machine learning-modellen.
    1. **Experiment:** Gebruikt voor het aanmaken, uitvoeren en bijhouden van de ontwikkeling van meerdere modellen.
    1. **Notebook**: Gebruikt voor het verkennen van data en het bouwen van machine learning-oplossingen.
    1. **Import Notebook:** Gebruikt voor het importeren van notebooks vanaf een lokale machine.
    1. **Sample:** Voorbeeldoplossing.

      ![Picture28](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/ad8c4969-b773-4729-ac6f-b051f6f0568d)

### Taak 6: Synapse Data Warehouse Experience

1. Selecteer **Data Science** linksonder in uw scherm. Het dialoogvenster voor Fabric-ervaringen wordt geopend.
2. Selecteer **Data Warehouse**. U wordt doorgestuurd naar de **Data Warehouse Home page**. Ook hier zijn drie secties aanwezig. In de sectie New ziet u de beschikbare items. U ziet dat Data Pipeline en Dataflow Gen2 hier ook beschikbaar zijn.

   1. **Warehouse:** Gebruikt voor het bieden van strategische inzichten vanuit meerdere bronnen.
   1. **Sample warehouse:** Voorbeeldoplossing voor een warehouse.
   1. **Data pipeline:** Gebruikt voor het orkestreren van data-oplossingen.

        ![Picture29](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/fd991d84-d9ba-45df-867d-0b4f3ce00174)

### Taak 7: Real-Time Analytics Experience

1. Selecteer **Data Warehouse** linksonder in uw scherm. Het dialoogvenster voor Fabric-ervaringen wordt geopend.
2. Selecteer **Real-Time Analytics**. U wordt doorgestuurd naar de **Real-Time Analytics Home page**. Ook hier zijn drie secties aanwezig. In de sectie New ziet u de volgende items:

   1. **KQL Database:** Gebruikt voor het snel laden van gestructureerde, ongestructureerde en streaming data voor querying.
   1. **KQL Queryset:** Gebruikt voor het uitvoeren van queries op de data om deelbare tabellen en visuals te produceren.
   1. **Eventstream:** Gebruikt voor het vastleggen, transformeren en routeren van real-time event streams.
   1. **Use a sample:** Gebruikt voor het aanmaken van een voorbeeld.

      ![Picture30](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/69f664d3-c1b7-429f-b539-f3a7c5f3ff58)

# Fabric Workspace

### Taak 8: Een Fabric Workspace aanmaken

1. Laten we nu een workspace aanmaken met een Fabric-licentie. Selecteer **Workspaces** in de linker navigatiebalk. Er wordt een dialoogvenster geopend.
2. Selecteer **+ New workspace**.

      ![Picture31](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/1abb5726-062b-4e6f-b31d-7e64154e9a08)

3. Het dialoogvenster **Create a workspace** wordt aan de rechterkant van de browser geopend.
4. Voer in het veld **Name** de waarde **FAIAD_username** in.

    >**Opmerking:** De naam van de workspace moet uniek zijn. In dit document gebruiken we FAIAD als workspacenaam. Uw workspacenaam moet echter anders zijn. Zorg ervoor dat er een groen vinkje met **This name is available** wordt weergegeven onder het veld Name.
   
6. Als u dat wilt, kunt u een **Description** voor de workspace invoeren. Dit is een optioneel veld.
7. Klik op **Advanced** om de sectie uit te vouwen.

     ![Picture32](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/7753b82d-3e75-44ae-ade7-922d7ce6aa82)

8. Controleer onder **License mode** of **Trial** is geselecteerd. (Dit zou standaard geselecteerd moeten zijn.)
9. Selecteer **Apply** om een nieuwe workspace aan te maken.

      ![Picture33](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/53c16aaa-f5aa-40e1-ae81-6b3419b8320d)

    Er wordt een nieuwe workspace aangemaakt en u wordt doorgestuurd naar deze workspace. We halen data op uit de verschillende databronnen, brengen deze naar de Lakehouse en gebruiken de data uit de Lakehouse om ons model te bouwen en daarover te rapporteren. De eerste stap is het aanmaken van een Lakehouse.

### Taak 9: Een Lakehouse aanmaken

1. Het Fabric Experience-pictogram linksonder in uw scherm is momenteel ingesteld op **Real-Time Analytics**; klik erop om het dialoogvenster voor Fabric-ervaringen te openen.

2. Selecteer **Data Engineering** om naar de Data Engineering Home page te navigeren.

      ![Picture34](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/5d99fdea-b065-4fe7-af9c-c3e7fee8a0c2)

3. Selecteer **Lakehouse**.

     ![Picture35](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/3ee5be4a-be9b-4cce-bf4b-9587895bfa1c)

4. Het dialoogvenster voor een nieuwe Lakehouse wordt geopend. Typ **lh_FAIAD** in het tekstveld Name.
 
    >**Opmerking:** lh verwijst hier naar Lakehouse. We gebruiken het voorvoegsel lh zodat het item eenvoudig te herkennen en te vinden is.
    
5. Selecteer **Create**.

      ![Picture36](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/13961927-fea2-485f-8d53-ca04a496915f)

      Binnen enkele ogenblikken wordt een Lakehouse aangemaakt en wordt u doorgestuurd naar de Lakehouse-interface. In het **linker paneel** ziet u dat u onder uw workspace het Lakehouse-pictogram vindt. U kunt op elk moment eenvoudig naar de Lakehouse navigeren door op dit pictogram te klikken.

      In de Lakehouse Explorer ziet u **Tables** en **Files**. De Lakehouse kan Azure Data Lake Storage Gen2-bestanden weergeven in de sectie Files, of een dataflow kan data laden naar Lakehouse-tabellen. Er zijn diverse opties beschikbaar. In de volgende labs laten we u een aantal van deze opties zien.

      ![Picture37](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/c610b936-304c-431c-87ed-72def4c4ba1d)

      In dit lab hebben we de Fabric-interface verkend en een Fabric workspace en een Lakehouse aangemaakt. In het volgende lab leren we hoe u Dataflow Gen2 gebruikt om verbinding te maken met ADLS Gen2 voor het extraheren, transformeren en inladen van data in de Lakehouse.

# Referenties
Fabric Analyst in a Day (FAIAD) maakt u vertrouwd met een aantal van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service vindt u in de sectie Help (?) links naar uitstekende bronnen.

   ![Picture38](https://github.com/CloudLabsAI-Azure/Fabric-Analytics-in-aday/assets/121504071/a1caeee4-9c00-4538-b506-aedbe4b62445)

Hieronder vindt u nog enkele aanvullende bronnen die u helpen bij uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [Microsoft Fabric GA-aankondiging](https://aka.ms/Fabric-Hero-Blog-Ignite23)
- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)
- Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)
- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)
- Leer nieuwe vaardigheden door de [Fabric Learning-modules](https://aka.ms/learn-fabric) te verkennen
- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)
- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)
- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om uw vragen te stellen, feedback te delen en te leren van anderen

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

Door gebruik te maken van deze demo/dit lab gaat u akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met als doel uw feedback te verkrijgen en u een leerervaring te bieden. U mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback aan Microsoft te geven. U mag het niet voor enig ander doel gebruiken. U mag deze demo/dit lab of een deel daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, licentiëren, er afgeleide werken van maken, overdragen of verkopen.

KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN DEEL DAARVAN) NAAR EEN ANDERE SERVER OF LOCATIE TEN BEHOEVE VAN VERDERE REPRODUCTIE OF VERSPREIDING IS UITDRUKKELIJK VERBODEN.
DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARETECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN GEPRESENTEERD, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DE MANIER WAAROP EEN DEFINITIEVE VERSIE ZOU WERKEN. WE KUNNEN OOK BESLUITEN GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UIT TE BRENGEN. UW ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK ANDERS ZIJN.

**FEEDBACK**. Als u feedback geeft over de technologiefuncties, functionaliteit en/of concepten die in deze demo/dit lab worden beschreven aan Microsoft, verleent u Microsoft kosteloos het recht om uw feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, te delen en te commercialiseren. U verleent ook aan derden, kosteloos, alle octrooirechten die nodig zijn voor hun producten, technologieën en diensten om gebruik te maken van of een interface te hebben met specifieke onderdelen van een Microsoft-software of -service die de feedback bevat. U geeft geen feedback die onderworpen is aan een licentie die Microsoft verplicht haar software of documentatie aan derden te licentiëren omdat wij uw feedback daarin opnemen. Deze rechten blijven van kracht na afloop van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, INCLUSIEF ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, ONGEACHT OF DEZE UITDRUKKELIJK, IMPLICIET OF WETTELIJK ZIJN, GESCHIKTHEID VOOR EEN BEPAALD DOEL, EIGENDOM EN NIET-INBREUK. MICROSOFT GEEFT GEEN TOEZEGGINGEN OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE OUTPUT DIE VOORTVLOEIT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR ENIG DOEL.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen veranderen in toekomstige versies van het product. In deze demo/dit lab leert u over een aantal, maar niet alle, nieuwe functies.
