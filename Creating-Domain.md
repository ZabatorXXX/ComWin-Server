
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
 
