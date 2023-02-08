# Slutuppgift – Datasäkerhet med Fokus på Windows


Uppgift 2: Säkerhet i en virtualiserad servermiljö (Praktisk Uppgift)
I denna uppgift skall den studerande genomföra stegvisa tillämpningar på en virtualiserad 
miljö för att uppvisa att man har den praktiska kunskapen att applicera samtliga lärdomar 
som har presenterats utmed kursens gång.
Nedan följer det som skall utföras för att förbereda arbetsmiljön:

1.  Sätt upp en virtuell miljö i Hypervisor av valfritt val. Se bara till att enheterna som 
skapas skall kommer att ha möjlighet att kommunicera med varandra över det lokala 
nätverket.

2. Generera nu tre virtuella datorer:
- 2x Windows Datacenter 2022 Desktop Exeprience
- 1x Windows Datacenter 2022 Core

3.  Genomför installationsprocessen på samtliga av dessa tre enheter och se till att de är 
uppkopplade emot internet

4.  Kontrollera att ni har ett aktivt Azurekonto och att detta innehar en subscription för 
att kunna genomföra deployments.

När detta är förberett följer nu nedan den situation som ni skall konstruera en infrastruktur 
åt…


Situationsbeskrivning:

Ni står inför ett uppdrag att hjälpa företaget SIHC AB med att sätta upp en Windows-baserad miljö för att hantera sina dagliga tekniska utmaningar. I dagsläget har verksamheten tre server-baserade Windows-datorer i sin dagliga verksamhet. Företaget arbetar med produktion av konsumentprodukter vilket innebär att organisationen har ett par huvudsakliga behov:

- Identitetshantering då deras enheter behöver kommunicera och kunna användas av de 
olika arbetsskiften. (Olika användare vid samma dator)

- Datorerna behöver även vara sammankopplade under samma domän för att kunna
hanteras centralt gällande regler och policies. 

- Datorerna skall kunnas hanteras remote för översikt hemifrån av övriga medarbetare 
(Remote Desktop och Windows Admin Center)

- Datorerna skall klara av att virtualisera med Hyper-V för att snabbt spinna upp nya 
arbetsmiljöer vid tester och liknande. (Hyper-V)

Detta är idag verksamhetens grundbehov. Men efter ett samtal med de ansvariga så inser ni 
att även dessa funktioner skulle behöva implementeras:
- En virtuell Windows-server från Azure ansluten till arbetsnätet för att snabbt kunna 
expandera vid framtida behov (Azure VM)

- Ett virtuellt nätverk för att administrera molnenheterna (Azure vNet)
- Bättre hantering av lagringen på maskinerna (Storage Spaces)
- Bättre sync av datan som lagras (Azure File Sync)
När ni har samtliga lösningar implementerade bör ni ha en topologi som ser ut som följande:

![image](https://user-images.githubusercontent.com/42642927/217272926-4fea0c8b-ccba-4ce6-b89a-f2bd6f2ede54.png)

När detta sedan är på plats skall ni även addera följande grundläggande säkerhetsåtgärd för 
samtliga enheter, bortsett från de ni redan genomfört:
- Koppla ihop en infrastruktur med Microsoft Defender for Cloud via Admin Center


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

VSwitch.....


Jag börjar med att använda hypver-v. 
I hypper-v skappar jag upp tre nya servrar.
Två Windows Datacenter 2022 Desktop Exeprience & en Windows Datacenter 2022 Core.

Generation 2 servrar som använder sig utav 2048 i startminne, i konfigurera  nätver använder jag VSwitch, Virtuel hårdisk på 64 GB som sparas i en ny sdd disk jag inte anänder. opperativ systemet är en iso fil SERVER_EVAL_x64FRE_en-us.iso.   


