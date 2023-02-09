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


-----------------------------------------------------------------------------------------------------------------------------------------

VSwitch.....


Jag börjar med att använda hypver-v. 
I hypper-v skappar jag upp tre nya servrar.
Två Windows Datacenter 2022 Desktop Exeprience & en Windows Datacenter 2022 Core.

Generation 2 servrar som använder sig utav 2048 i startminne, i konfigurera  nätver använder jag VSwitch, Virtuel hårdisk på 64 GB som sparas i en ny sdd disk jag inte anänder. opperativ systemet är en iso fil SERVER_EVAL_x64FRE_en-us.iso.   

När jag startar upp alla servrar trycker man enter när den frågar om ordisk bios. 
När de frågar om språk för instalationen väljer jag. Svenska som tid och valuta format. Snabbar till med att trycka in (sw) för att snabbare ta sig till sweden. När det har blivit valt väljer den svenska som tagentbord. 

![image](https://user-images.githubusercontent.com/42642927/217502697-38408719-9a89-41ba-a856-94bcb0720ebe.png)

Efter det väljer jag vilken typ av servrar vi ska ha.  2x Windows Datacenter 2022 Desktop Exeprience  & 1x Windows Datacenter 2022 Core.

![image](https://user-images.githubusercontent.com/42642927/217504280-6685e642-b32c-4d28-bcc6-1d7b4651f814.png)

Sen när vi kommer till vilken typ av  instalation väljer vi. Custom:Install...... och next i nästa steg.

![image](https://user-images.githubusercontent.com/42642927/217505229-2876c20b-96e8-41f3-bfa1-f34f02690181.png)

Repeterar stegen för att få totalt två Windows Datacenter 2022 Desktop Exeprience och em Windows Datacenter 2022 Core.

![image](https://user-images.githubusercontent.com/42642927/217505846-c5964280-3803-4fd0-9474-245b98bcecc6.png)

Sen komme de fråga om lössenord.
* Win-DC - Password123!
* Win-DCC - Password1234!
* Win-2x-DC - Password12345!

När de frågar om man vill tillåta nätverket bli sed utav andtraa tar jag YES.

![image](https://user-images.githubusercontent.com/42642927/217508597-a8497c95-3f64-436a-a55f-8bd6a694439f.png)

När jag väll är inlogag i datorerna gör jag några somå kofigueringar för att snygga upp miljön.

1. Bytter namn på enheterna. 

Gå till local server computer name och i trycker jag på change. Namnen på servrarna blir:
* Win-DC = Win DC
* Win-2x-DC = Win-2x-DC

När namnm är vall startar serven om och välj anslute igen.

På DC servrarna ser det ut så här:
![image](https://user-images.githubusercontent.com/42642927/217512017-8481645a-f170-43df-a151-989204060803.png)

På DCC serven ska vi få namn Win-DCC:

Enter number to select an opption: skriver vi 2 för 2)Computer name: .
Väljer att skriva i ett namn  (blank=Cancel): Win-DCC
Frågar om restart now? (Y)es or (N)o: Srkiver vi in Y och enter.
Och välj anslute igen.


STEG två i processen. Se till att enheterna som skapade kan kommunicera med varandra över det lokala med egne ip på nätverket.

I server Win-DC går jag till Local server > ethernet > network connections > ethernet >  Ethernet satus > propeties > tar bort ipv6 > går till ipv4 > dubelklikar på ipv4 > Use following ip address:

* Ip address: 192.168.1.250
* Subnet mask: 255.255.255.0

Use the following DNS server addres:
* Preferd DNS Server: 192.168.1.250

OK

![image](https://user-images.githubusercontent.com/42642927/217515642-4a143b88-20fb-411c-9ed3-33a2fba9c63b.png)

Win -2x-DC:
* Ip address: 192.168.1.254
* Subnet mask: 255.255.255.0
* Preferd DNS Server: 192.168.1.250


I Win-DCC går vi till nr.8. "8) Network settings"
Select network adapter index # (Blank=Cancel): nr1. för index 1
Väljer 1 för: 1) Set network adapter address och för selection skiver vi S -> (S)tatic IP address, för statis ip. 
De frågar om  Enter static IP address (Blank=Cancel): som blir, 192.168.1.252 enter två gonger för vi vill ha sunbetmasken  som recomenderas. 
Vi blir tvungna att skriva i gateway om vi bara tar enter blir det Cancel som blank. Värdet för gatewayn blir 0.0.0.0 och enter enter.
Gör om så vi kommer till network adapter settings. 8 > 1
Nu väljer vi två, 2) Set DNS servers. vilket blir 192.168.1.250 från tidigare. Enter wnter för vi vill inte ha någon alternet dns. 

#### Active Directory Domain Service
 
 
I Win-DC > Server Manager > går jag till Manage. Add roles and Features > Role-based or feature-based instalation > Win DC som server selection > Server Roles [X] i Active Directory Domain Services > Add Features > Next, Next, Next > Install

Vi kommer vara tvungna att uppdatera serven till Domain Controller.
Finns två tillväga gång sätt. Antingen ta den första promot som kommer upp. eller tar vi oss upp till flaggan och väljer där.
![image](https://user-images.githubusercontent.com/42642927/217545148-b8183dc6-c411-428f-b7e9-d0736b61dc93.png)

Har Add new forest, Root domain name blir SimonHomeLab.com > Domain Controller Oprions skriver vi in lösenord Password123! samma som Win-DC. Ingen Create DNCS delegation tar bara next. NetBIOS blir SIMONHOMELAB auto genererat, paths och next, next på Revew options och i chek tar vi Install

![image](https://user-images.githubusercontent.com/42642927/217560673-c32d9b0d-4083-4583-ad67-133e379f294f.png)

Gör instalationen utav Admin Center.

![image](https://user-images.githubusercontent.com/42642927/217562363-41e790f4-dcf2-4b2e-ae56-e142ae14e32d.png)

####### Vi vill inte ha singel pont off failer så jag väller att i Win-2x-DC att repetera stegen ovan med en förändring.  ########

Acceptera villkor, oblikatorriska diagnostikdata, välljer att inte använda microsoft update, Välj port 1030 och instalera. 

Lägger in Win-DCC i domänen genom att skriva 1 för att ta min till "1)Domain/Workgroup" D för Join workgroup. Och skriver in SimonHomeLab.com  och logar in med administrator konto.
Lägger in Win-2x-DC i Domain. Settings, system about, advanced system settings, computer name, change, meber of... Domain: SimonHomeLab.com .

Märkte att jag var tvungen att änrda minna internet inställningar eftersom min Lokala  gatewy på hemnetet var anorlunda en de på serverrarna och skappade något problem att komma ut på internte. Så jag ändrar ip till DHCP ser till att ip adresserna fungera under samma DNS  10.0.100.48. IP på DCC är 10.0.100.52, Win-2x-DC 10.0.100.56.

Anledning var 1. internet och 2. närst kommande steg.

![image](https://user-images.githubusercontent.com/42642927/217864281-41f8df24-c093-41d3-a717-d3044754e391.png)

Gör servrarna tillgägnliga på Win-DC Genom, All server > höger click och add server till Win-DCC och Win-2x-DC.

![image](https://user-images.githubusercontent.com/42642927/217864745-73e62221-cdb1-4fbc-881d-ec2296599925.png)

Skappar upp användare och användings grupp. I active directory users and computers. 

![image](https://user-images.githubusercontent.com/42642927/217865806-ab6e7563-b735-4824-b575-6018a8b17562.png)

- Simon Major och lössenord. WordPass123! och bytt lösenord nästa inlog.

Går till domänen. Använder create new organizational unit in the current container. Namnger till HomeLab ORG och bockar av accidental deletion. 

![image](https://user-images.githubusercontent.com/42642927/217867360-612916b3-012a-434d-9a84-c906cf7b367f.png)

Flyttar användaren till organisationen. Och flyttar Win-DCC och Win-2x-DC dit.Skappar upp en grup som nämnder til Lab-Department till organisationen. 

![image](https://user-images.githubusercontent.com/42642927/217889911-5d3cc6cb-c7df-4a96-95fd-424c09a315b8.png)

Lägger till Simon in i gruppen,

![image](https://user-images.githubusercontent.com/42642927/217890141-2719b801-9676-4d55-a11f-c6e6a00c09f1.png)

Gör att alla i gruppen blir admin. 

![image](https://user-images.githubusercontent.com/42642927/217890624-f3d7f4e6-8b1a-4933-b468-e923635dec63.png)

Ser till att Win-DC är med i den globbala controlen. 

Och lägger till gruppen i Win-DC 

![image](https://user-images.githubusercontent.com/42642927/217891786-622e6e2a-2ff3-4dd3-bc4d-7da2d37d18bf.png)

Går in i pwoershell och skriver in gpupdate

![image](https://user-images.githubusercontent.com/42642927/217892632-f50b15ed-7682-460f-8bc7-e4d5d6d9b2a9.png)


Lägger till Simon för remote dektop till Win DC, Win-2x-DC

![image](https://user-images.githubusercontent.com/42642927/217895424-87bf7217-05da-447d-a568-c2c6ff16c17d.png)
