# Description  "Slutuppgift – Datasäkerhet med Fokus på Windows"



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




# Part 1 Locally

## Part 1 Creating the VMS

Start with opening Hyper-V on my local computer. In Hyper-V I created three new servers. Two Windows Datacenter 2022 Desktop Desktop Experience and one Windows Datacenter 2022 Core. 
 
All three are generation 2 servers with 2048 memory, a virtual switch, and virtual hard drive that stores 64 GB. Witch I decide to save on a new local SSD hard drive using an iso file as operative system - SERVER_EVAL_x64FRE_en-us.iso. 

On bootup I press enter so I get correctly booted. When asked for langued I select Swedish for keyboard and time. I press down “sw” to scroll down to Swedish easier.

![image](https://user-images.githubusercontent.com/42642927/217502697-38408719-9a89-41ba-a856-94bcb0720ebe.png)

For two off the server, I select Windows Datacenter 2022 Desktop Experience and one Windows Datacenter 2022 Core.  

![image](https://user-images.githubusercontent.com/42642927/217504280-6685e642-b32c-4d28-bcc6-1d7b4651f814.png)

Type off installation is Custom installation and select next.

![image](https://user-images.githubusercontent.com/42642927/227269220-8a23872e-d986-4f8e-8cce-83d6b9ede402.png)

Repeated the possess to have in total: 

Two Windows Datacenter 2022 Desktop Experience 
One Windows Datacenter 2022 Core 

![image](https://user-images.githubusercontent.com/42642927/217505846-c5964280-3803-4fd0-9474-245b98bcecc6.png)

When asked to create password, I choose to have a simple password, but they should vary. The first password was for Win-DC = Password123! then on Win-DCC = Password1234! and on Win-2x-DC = Password12345! . 

Select Yes when ask in desktop experience if I want to allow my network to discover other on the network.

![image](https://user-images.githubusercontent.com/42642927/217508597-a8497c95-3f64-436a-a55f-8bd6a694439f.png)


---

## Visual changes to the VM

Now when we have set up the local VM it would be a good thing to nicening up them.  


1. Change Commuter Names 

To do this we will go to Server Manager\Local Server.  Click on the current name. 

![image](https://user-images.githubusercontent.com/42642927/227279012-8c568d1c-f513-4ee4-8483-1eeb1d72ac1e.png)

It will direct you to system properties. Here we press “Change” type in each name. The server names given to the VMs is Win-DC, Win-2x-DC and Win-DCC. Example on Desktop Experience: 
![image](https://user-images.githubusercontent.com/42642927/227279375-9ca0efdf-e9b7-4cd4-8882-ac02f88e03e9.png)

We can all so rename the server directly settings about.  

![image](https://user-images.githubusercontent.com/42642927/227324540-fb1397bb-2137-4c8a-a063-7c7a666f3c2a.png)

and

![image](https://user-images.githubusercontent.com/42642927/227324924-bd4b9bef-39e7-4009-8410-3d0153fe0d48.png)




On Windows Datacenter Core the following has to be done to change server name.  

On line "Enter number to select an option:" we type number 2, two for "Computer name:". Type Win-DCC and enter and Y for restart now.
![image](https://user-images.githubusercontent.com/42642927/227312271-f55ccc37-0c5c-4454-a6f5-fc546bb9b965.png)

On Windows Datacenter Core the following has to be done to change server name.  After restarting it should look something like:

![image](https://user-images.githubusercontent.com/42642927/227316136-14d50ced-c173-4ed7-b0d7-8d3e69da9c9c.png)


## 2. Part Two Networking

## 1. Setting up DNS configuration 

### Win-DC:

Starting on Win-Dc I first go to cmd to get the IP that has been set. In cmd I type ipconfig that returns:

![image](https://user-images.githubusercontent.com/42642927/227746794-7a452db9-b8ce-45c9-951a-42e1b13a2da5.png)

Then go to Server Manager\Local Server – Ethernet > assigned by DHCP. Right click on Ethernet and go to Propeties. In Propeties I disable IPv6 and change settings in Ipv4 using Propeties. Select “Use the following IP address” paste in the values: 

* IP address: 10.0.100.56 
* Subnet Mask: 255.255.255.0 
* Default gateway: 10.0.100.1 

For "Use the following DNS server addresses:" I use the Ip address - 10.0.100.56.

And save. 

### Win-DCC:

Sing in on Win-DCC. In “Enter number to select an option: “I want to go to number eight for, 8) Network settings. Which directs me to this: 
![image](https://user-images.githubusercontent.com/42642927/227775636-d6bdb197-accc-46bb-9f63-938f46d062f5.png)

In “Select network adapter index # (Blank=Cancel):” use index number 1.  It gives me a new page.

![image](https://user-images.githubusercontent.com/42642927/227775721-ffa9492e-261e-45b1-be90-c266cf777737.png)

At line “Enter selection (Blank=Cancel):” use one to go to 1) Set network adapter address. Asks “Select (D)HCP or (S)tatic IP address (Blank=Cancel):” Were we type S for static IP. In “Enter static IP address (Blank=Cancel):” I type the Ip: 10.0.100.57 and enter twice as we want to use 255.255.255.0 which= to 255.255.255.0. When asked “Enter default gateway (Blank=Cancel):” we want to skip this, but we must type in value: 0.0.0.0

In "Enter selection (Blank=Cancel):" I type the value 2, for" 2) Set DNS servers". "Enter new preferred DNS server (Blank=Cancel):" I use 10.0.100.56 for DNS and use blank for "Enter alternate DNS server (Blank=None):". 

### Win-2x-DC

For win-2x-DC I use the same method but changing the setting from a different part of the server settings. I go to Windows Settings > Network & Internet > In “Status” Select change adapter settings. Repeat previous steps - Right click on Ethernet and go to Propeties. In Propeties I disable IPv6 and change settings in Ipv4 using Propeties. 

Get the Ip form ipconfig in cmd. 

![image](https://user-images.githubusercontent.com/42642927/227775158-be2a2371-175f-47d8-909a-4083abe70c64.png)

Select “Use the following IP address” paste in the values: 

* IP address: changing 10.0.100.59 > 10.0.100.58 
* Subnet Mask: 255.255.255.0 

For "Use the following DNS server addresses:" I use the Ip address - 10.0.100.56. 

# 2. Adding Server roles and features (Active Directory Domain Service)

In Win-DC go to Server Manager then “Manage” button. Add roles and Features > Role-based or feature-based installation > Win DC as server selection > Server Roles [v] Active Directory Domain Services > Add Features > Next, Next, Next > Install 

![image](https://user-images.githubusercontent.com/42642927/217545148-b8183dc6-c411-428f-b7e9-d0736b61dc93.png)

```
. Domain controller options:  
├── Deployment configuration 
│   └── First select deployment operation “Add a new forest” and Root domain name to be SimonHomeLab.com 
│
├── Domain controller options 
│ └── Use standard values and add a password. The password I am going to be using is: Password123! .
│
├── DNS option 
│   └── We do not create DNS delegation 
│
├── Additional option 
│   └── NetBIOS domain name is SIMONHOMELAB. 
│
├── Paths 
│   └── In paths we use standard values 
│
├── Review Options 
│   └── Just Next. 
│
├── Prerequisites Chek  
    └── Wait for it to verify and install. 
```

Server will restart 

Sign back in as Administrator – Password123! 

## 3. Joining the domain / workgroup

For the desktop version it can be done in server manager or through the settings. I will show you how to do both. Let us start by going through the server manager. 

In the server manager goes to Local Server. Press on Workgroup it will take me to system properties, click change and change from workgroup to domain type in SimonHomeLab.com . 

![image](https://user-images.githubusercontent.com/42642927/227806463-5f4004bb-5a2e-4c52-a2d1-9bd6203a5b28.png)

Logg in with the administrator 
We can all get domain from settings > about then system protection or advanced system settings then computer name. We should be in system Propeties. And change for domain could all so change name.  

 ![image](https://user-images.githubusercontent.com/42642927/227808319-d047b1aa-9750-4b1b-b93e-8722d8c14288.png)

I download Active Directory Domain Services on Win-2x-DC 

Win-DCC

n win-dcc “Enter number to select an option:” I type number 1 for “1) Domain/workgroup: “. Right now, the Workgroup is: WORKGROUP. We get asked “Join (D)omain or (W)orkgroup? (Blank=Cancel):” Were we type D for joining domain. 

In line “Name of domain to join (Blank=Cancel):” we type out: SimonHomeLab.com 
Specify an authorized domain\user (Blank=Cancel): admin 
  Password for administator: ************ 
  Joining SimonHomeLab.com... 
  
![image](https://user-images.githubusercontent.com/42642927/227938319-cc74119a-c382-42ae-8d08-af40bb3226d9.png)

  Then restart. 

And sign back in as:  .\administrator and password: Password1234! 

Result:

![image](https://user-images.githubusercontent.com/42642927/227949821-893b491e-de7d-4e70-be2a-7804930df7bd.png)

## 4. Creating users for the domain

In win-DC we go under tools in server manager. In tools we select active directory users and computers. Oppen up the domain – SimonHomeLab.com, right click on folder users and select new > user. 

![image](https://user-images.githubusercontent.com/42642927/217865806-ab6e7563-b735-4824-b575-6018a8b17562.png)

Next for password where I'm using: WordPass123! .
And select never expire so we don’t have to change password when we sign in for the first time. 
This user will be a domain admin, so we don’t have to sign in with server administrator user. So, move the user to groupe: Domain Admins.
Click on Domain Admins so it is selected. Go to members and press “Add...” Enter the name Sim, and check names until Simon Major user is selected then ok then hit apply if you happy with the changes.  

![image](https://user-images.githubusercontent.com/42642927/228508907-c90c4588-e01b-4499-9cd2-9bba96019b96.png)
 
 Goes to the domain in active directory users and computers. Using the new organization button looks like a map with a sun on to create new organizational unit in the current container. Gives the name HomeLab, I right click on Simon Major user that was saved/created in users and right click “move” to HomeLab. From the folder computer I moved both domains “Win-DCC and Win-2x-DC" to our new organization.   

Create a new group for the organization I named Lab-Department.  
![image](https://user-images.githubusercontent.com/42642927/217889911-5d3cc6cb-c7df-4a96-95fd-424c09a315b8.png)
Adds Simon Major user to group.

Turns Lab-Department into administrative group by adding administrators in member of part in Lab-Department properties. 

![image](https://user-images.githubusercontent.com/42642927/217890624-f3d7f4e6-8b1a-4933-b468-e923635dec63.png)

Go to cmd and type gpupdate to update group polices and updating changes we have done.

![image](https://user-images.githubusercontent.com/42642927/228570440-420cc146-4911-49ea-be80-bbae39bfbca3.png)

I make it possible for Simon user to be able to use remote desktop to the VM by adding it in remote desktop: 

Press, “Select user that can remotely access the pc”. Then add, type Simon and check name then press ok.  

![image](https://user-images.githubusercontent.com/42642927/228573878-61f54549-5966-4628-ab6e-1107a16e7cb4.png)

## 5. Configuring DHCP 

 

Download DHCP from server manager “add roles and features” select role-based installation type, then server now server role DHCP next on features. In DCHP Server select next then install.  

 

Complete DHCP config.

Next, have SIMONHOMELAB\administrator as selected user and commit. Result in:

![image](https://user-images.githubusercontent.com/42642927/228664545-f5d1bc3d-a6f0-45a1-90ae-6a5914bd945a.png)

Now I set up a new scope from tools DHCP. Right click on Ipv4 inside the DHCP tool. Name it Lab and next. 

![image](https://user-images.githubusercontent.com/42642927/228809611-a3386b29-e3d9-4ef3-8876-16063ea6fb4c.png)

Enter IP addresses range, Start IP 10.0.100.65 addresses: End IP address: 10.0.100.70. Skip exclusion, next, next, next and 10.0.100.1 as Default Gateway. Next, next and yes activate scope then finish.  

![image](https://user-images.githubusercontent.com/42642927/228809263-35997819-9e4e-4b56-b700-cd8c21135cc1.png)

## 6. New user - Sharing file between users

Go to active directory users and computers. Create a new user, give first name: “Extra”, last name: “Extra” and full name is “Extra User1”.
The logon name will be “Extra-User1”.  

![image](https://user-images.githubusercontent.com/42642927/228812765-4d80ea73-849a-443b-91ba-326c8e0c4385.png)


The password I'm giving the user is: WordPass1234!  
Adds the user to administrator “member”.  

Adds the user to administrator “member”. Now we have the second user it is time to create a folder that we will share between users. I create the folder that will be stored on the desktop. Name it to shared-folder. Right click on the map to access map properties. Go to the security part and to be extra sure the user has access we will add the user and gives full access.  

![image](https://user-images.githubusercontent.com/42642927/228832326-4b2ed209-7121-47c8-a9b8-169c26541cdf.png)

Go to sharing, press advanced sharing use the check mark in “share this folder” and hit apply/ok. When done should look something like this: 

![image](https://user-images.githubusercontent.com/42642927/228832897-c5b40928-2234-46cd-89e3-4799ecbe7192.png)

I copy the network path: \\WIN-DC\shared-folder and sign out from the administrative account to sign in with the new user.  When signed in as new user go to file explorer, quick access and type in \\WIN-DC\shared-folder to then see the shared folder when selected.  

![image](https://user-images.githubusercontent.com/42642927/228838543-0d971d88-bd31-4775-8d59-724525fa59cc.png)
![image](https://user-images.githubusercontent.com/42642927/228838745-266a91a8-4948-4647-a28c-691c1b7cb941.png)


# 3. Tools // access 

## 1. Windows Admin Center 

First download the software from the internet. Oppen up downloaded file.
The installation guide will open, first accept terms and condition,
I select send obligatory data, have not use Microsoft update, next, port 1030 and have 1 and 4 selected and installed.
Open application when installation is done and finished. It will open a certificate we accept.  

And it will open
![image](https://user-images.githubusercontent.com/42642927/227974488-aee65b16-429c-4508-bb3d-0ea5817433fc.png)

We can see se the Vms under Tools virtual machines.  

![image](https://user-images.githubusercontent.com/42642927/227977454-d48abbcd-3e99-4d53-9d7e-ad3810b82a75.png)

And if we click on the we can see under Computer name:

* Win-DC = Win-DC.SimonHomeLab.com
* Win-2x-DC = Win-2x-DC.SimonHomeLab.com
* Win-DCC = Win-DCC.SimonHomeLab.com

## 2. Remote access

* Win-DC and Win-2x-DC

 

Win-DC I will show how to enable from server manager.
In server manager we go to Server Manager\Local Server. In the page we can see remote desktop is disabled.

![image](https://user-images.githubusercontent.com/42642927/228087031-c4092906-e7c9-4706-aba3-fc8955e00d02.png)

Click on disabled and select the second option to enable it then press ok/apply. 

![image](https://user-images.githubusercontent.com/42642927/228087544-768cbde4-36c9-4e08-b857-49aa2b467047.png)

On Win-2x-DC I'm setting up remote desktop true “settings about” page.  
![image](https://user-images.githubusercontent.com/42642927/228092119-b4c63641-a469-4394-8124-a4dbbb08366e.png)

Switching from off to on and apply to enable. 

![image](https://user-images.githubusercontent.com/42642927/228093537-557826f0-a8bc-49e0-a46e-6540a2e0e93d.png)


* Win-DCC
On Win-DCC in “Enter number to select an option:” we type 7. Seven for “7) Remote desktop:” it says “Disabled” so let's activate it.  We get asked “(E)nable or (D)isable Remote Desktop? (Blank=Cancel):” So type E. Then we get asked:   

![image](https://user-images.githubusercontent.com/42642927/227983583-c4ec95b6-8d70-4cc5-a01e-34d543e3f358.png)

Were we select number one which is more secure. Now it says on nr.7:

![image](https://user-images.githubusercontent.com/42642927/227983706-3944e3c5-e622-4045-b0bc-4eabee0fa6d4.png)



## 3. Connect to domain to Azuer AD connect

On Win-DC I search for Azure AD connect on edge. Select Microsoft download page: 

![image](https://user-images.githubusercontent.com/42642927/228100415-33d04d1d-0774-425e-8018-93b174ae0cd7.png)

On the page I select the orange download button to download the application.   

![image](https://user-images.githubusercontent.com/42642927/228237987-42b31f52-f565-44fd-b2d5-caf86a083a09.png)

![image](https://user-images.githubusercontent.com/42642927/228240097-e6cb9d08-39a2-43f6-a959-b27d59dd3422.png)

AZ AD connect new user

![image](https://user-images.githubusercontent.com/42642927/229614319-d6b12cc0-3c55-4ec6-96e8-047942eb2037.png)

Sign in:

![image](https://user-images.githubusercontent.com/42642927/229614618-1dbd71e4-9cde-4dcf-bbfa-616ff6afa8da.png)

Add setting security:

![image](https://user-images.githubusercontent.com/42642927/229615056-aeb02fc5-e492-4ff9-9546-d564fe3b7a07.png)

azuer account:

![image](https://user-images.githubusercontent.com/42642927/229615137-0eda7095-5240-44ae-8f54-f914162736c5.png)
![image](https://user-images.githubusercontent.com/42642927/229619269-dc0e80bb-b234-4807-a744-235b1e94f889.png)


udate new password



![image](https://user-images.githubusercontent.com/42642927/229620428-84ae25ca-d1e2-4328-9ae3-cd1ae0b0a34f.png)

![image](https://user-images.githubusercontent.com/42642927/229620521-5ab6ae2d-b5d3-4911-8575-00ac8f67a71c.png)

and install


![image](https://user-images.githubusercontent.com/42642927/229621392-386d0602-ae10-499e-a5e8-4546232a969a.png)


# 3. Cloud

Create V Net

### 1. Create New Resource Group 

![image](https://user-images.githubusercontent.com/42642927/227194038-637f2c41-a6f9-4720-baf1-0d315f3986bf.png)

### 2. Name the Vnet 

![image](https://user-images.githubusercontent.com/42642927/227194484-fc0087de-7fe1-4f94-ba47-82b2b6f70fbf.png)

### 3. Choose location
![image](https://user-images.githubusercontent.com/42642927/227194683-8e04bea6-63e8-46d2-bdc2-e788849a85ef.png)


### 4.Strat with Ip configuration
![image](https://user-images.githubusercontent.com/42642927/227195927-bba5e9d0-2895-43b1-a0b4-082df4d5997d.png)

New:

![image](https://user-images.githubusercontent.com/42642927/229466500-788df255-297c-445c-b0c4-9770fd89851c.png)


### 5. Create subnet
![image](https://user-images.githubusercontent.com/42642927/227196651-f991f34a-7ed1-4c8e-86b5-ff7452f338c9.png)

New:

![image](https://user-images.githubusercontent.com/42642927/229466949-9c3bcfea-6369-4d74-afab-be3046b9162b.png)


### 6. Review + create
![image](https://user-images.githubusercontent.com/42642927/227198050-914c5399-7a78-4008-8d86-804e0b07c2e4.png)

New:

![image](https://user-images.githubusercontent.com/42642927/229467283-f063c058-c1a2-4e6f-b81b-8d715dfb5345.png)


### 7. Create a Gateway Subnet 
![image](https://user-images.githubusercontent.com/42642927/227204663-c927ebae-3716-4de7-8c4f-1c3c32538df1.png)

New:

1. ![image](https://user-images.githubusercontent.com/42642927/229468145-729e3016-8d0c-4835-bdd1-74e52d344c6f.png)

2. ![image](https://user-images.githubusercontent.com/42642927/229468554-2881fca9-763d-41eb-8125-aae2c87e5392.png)


### 8. Create Virtual Network Gateway 

![image](https://user-images.githubusercontent.com/42642927/227206961-9e3e536d-4cd5-4a5b-9089-500d15a6604b.png)


 

### 9. Change SKU 
![image](https://user-images.githubusercontent.com/42642927/227207479-dc6cb783-4875-4357-9206-2058028856e2.png)

 

 

### 10. Name you're Public Ip address 
![image](https://user-images.githubusercontent.com/42642927/227207658-77dbc891-05a6-48f2-9560-8c81fde1c396.png)




### 11. Review + create 
![image](https://user-images.githubusercontent.com/42642927/227211187-97c7a8f6-082c-4188-a1c1-15e11ce5cece.png)

New:

![image](https://user-images.githubusercontent.com/42642927/229470617-48d7556f-f833-4066-be19-350d5c401dec.png)


### 12. Open PowerShell and create Self-sign root - client certificate 

Root cert: 
```
$cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature -Subject "CN=WinSec-Root" -KeyExportPolicy Exportable -HashAlgorithm sha256 -KeyLength 2048 -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign 
 
```

Client certificate: 
```
New-SelfSignedCertificate -Type Custom -DnsName SIMONHOMELAB -KeySpec Signature -Subject "CN= WinSec-CLIENT " -KeyExportPolicy Exportable -HashAlgorithm sha256 -KeyLength 2048 -CertStoreLocation "Cert:\CurrentUser\My" -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2") 
```

![image](https://user-images.githubusercontent.com/42642927/227248838-9a1da3fc-01a5-431b-a5a6-b68bf1926249.png)

New:
```

PS C:\Users\simon> $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature -Subject "CN=WinSec-Root" -KeyExportPolicy Exportable -HashAlgorithm sha256 -KeyLength 2048 -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
PS C:\Users\simon> New-SelfSignedCertificate -Type Custom -DnsName SIMONHOMELAB -KeySpec Signature -Subject "CN= WinSec-CLIENT " -KeyExportPolicy Exportable -HashAlgorithm sha256 -KeyLength 2048 -CertStoreLocation "Cert:\CurrentUser\My" -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")


   PSParentPath: Microsoft.PowerShell.Security\Certificate::CurrentUser\My

Thumbprint                                Subject
----------                                -------
5B2B9D9848665699DB2C66ABA9910C68D6246575  CN=WinSec-CLIENT


```
### 13. Type Certmgr in PowerShell and go to personal user certificats 
![image](https://user-images.githubusercontent.com/42642927/227248746-cf0676d4-58ec-4bd8-a003-9a4a7e2bcabc.png)


Azuer... Configure Point-to-Site Connection 


![image](https://user-images.githubusercontent.com/42642927/229499514-8a54707b-d28a-4062-b137-4e74f1f632c1.png)


Network Rule to allow ping:

```
 New-NetFirewallRule -DisplayName "Allow-Ping" -Protocol icmpv4
```
![image](https://user-images.githubusercontent.com/42642927/229912962-c565c55b-815f-474e-8d0b-b3e13c150db5.png)


# Create VM in Cloud

1. Creating the VM
 
![image](https://user-images.githubusercontent.com/42642927/229821525-b2cad283-2d13-4e15-8fc6-1a5227ca29c6.png)

2. Adding network to VM

![image](https://user-images.githubusercontent.com/42642927/229822090-3ec2c044-9cea-42d0-83b4-c35e6bfb1a92.png)

4. And create 

![image](https://user-images.githubusercontent.com/42642927/229827025-d0fc5f6a-7a20-410a-a516-fab52c5ae15d.png)

AzuerUser

Password12345!



8. Networkin





Sorce: - For VPN/Gatway

https://techcommunity.microsoft.com/t5/itops-talk-blog/step-by-step-creating-an-azure-point-to-site-vpn/ba-p/326264

https://www.youtube.com/watch?v=Gb3YE-0gBWQ&t=911s

https://www.youtube.com/watch?v=MorG47BTttU&t=597s 
 
https://www.youtube.com/watch?v=K0hgCWIbC1A


9. Storage,

1. Create storage space

![image](https://user-images.githubusercontent.com/42642927/230078875-90d0a59c-232c-4525-b085-d9073e64caef.png)
![image](https://user-images.githubusercontent.com/42642927/230079266-a0be9c83-824d-437f-861f-8a1a452b22e4.png)
![image](https://user-images.githubusercontent.com/42642927/230079678-a3d4a030-c0cf-4cc0-8fbf-8c1e85ee866a.png)

2. Go to resorse > Data storage "File share"
3. New file share:

![image](https://user-images.githubusercontent.com/42642927/230080583-a17268ce-2bbb-4bec-a363-62ca57cbddf9.png)

4. create
5. Go to deploy azure file sync

![image](https://user-images.githubusercontent.com/42642927/230081170-b3ec3886-11f5-4453-9bcc-33425ccaaa6b.png)

6. Create

7.Go yo resorce

8. New sync groupe

![image](https://user-images.githubusercontent.com/42642927/230081819-46a04f9a-cbfd-4c59-993e-bd891bfe647a.png)


Deploy Azure File Sync

1. Logg in to Server in cloud
2. Dowload server agent "https://www.microsoft.com/en-us/download/details.aspx?id=57159" 
3. ![image](https://user-images.githubusercontent.com/42642927/230083578-c6210f8a-5a4b-4725-8dc1-30b75d0897c6.png)
4. Go thought the instalation steps and install
5. When every thing is finished I sign in with Azuer User in Azuer file sync on server. 
6. And register:
![image](https://user-images.githubusercontent.com/42642927/230085649-cdd4e87b-50d8-4828-b9dd-a4fa434ea2fb.png)
7. Prese close:

![image](https://user-images.githubusercontent.com/42642927/230085949-0b90e2a0-dbb2-4a07-9b0e-7b87e0c85f3b.png)


8. Go back on Azuer > Get connect script form file sare and choos driver letter
9. Run script in powershell on server in cloud:

```
$connectTestResult = Test-NetConnection -ComputerName winsec.file.core.windows.net -Port 445
if ($connectTestResult.TcpTestSucceeded) {
    # Save the password so the drive will persist on reboot
    cmd.exe /C "cmdkey /add:`"winsec.file.core.windows.net`" /user:`"localhost\winsec`" /pass:`"iWuRfdkW7LiS22db1hwXQtVgiGe+c3rN4fCiziy8zuGyTOUQepvbt28Ms6JzHWbq+nNY2+1chaBd+AStGY2zBg==`""
    # Mount the drive
    New-PSDrive -Name S -PSProvider FileSystem -Root "\\winsec.file.core.windows.net\clode-share" -Persist
} else {
    Write-Error -Message "Unable to reach the Azure storage account via port 445. Check to make sure your organization or ISP is not blocking port 445, or use Azure P2S VPN, Azure S2S VPN, or Express Route to tunnel SMB traffic over a different port."
}
```
![image](https://user-images.githubusercontent.com/42642927/230107643-3aa0cfd7-3038-435a-8c83-ffae78d1e0a6.png)


11. select sync groupe > add server endpoint

![image](https://user-images.githubusercontent.com/42642927/230108486-33b5bae9-298d-486d-bee3-04966d4cc681.png)

12. 
https://learn.microsoft.com/en-us/training/modules/implement-hybrid-file-server-infrastructure/7-deploy-azure-file-synchronization
https://learn.microsoft.com/en-us/training/modules/implement-hybrid-file-server-infrastructure/8-deploy-azure-file-synchronization-2
https://www.youtube.com/watch?v=BCzeb0IAy2k

