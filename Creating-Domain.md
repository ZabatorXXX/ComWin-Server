
## 1. Setting up DNS configuration 

### Win-DC:

Starting on Win-Dc I first go to cmd to get the IP that has been set. In cmd I type ipconfig that returns:

![image](https://user-images.githubusercontent.com/42642927/227746794-7a452db9-b8ce-45c9-951a-42e1b13a2da5.png)

Then go to Server Manager\Local Server – Ethernet > assigned by DHCP. Right click on Ethernet and go to Propeties. In Propeties I disable IPv6 and change settings in Ipv4 using Propeties. Select “Use the following IP address” paste in the values: 

* IP address: 10.0.100.56 
* Subnet Mask: 255.255.255.0 

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

# 2. Adding Server roles and features 
