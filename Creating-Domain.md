
## 1. Setting up connection between VMs 

Starting on Win-Dc I first go to cmd to get the IP that has been set. In cmd I type ipconfig that returns:

![image](https://user-images.githubusercontent.com/42642927/227746794-7a452db9-b8ce-45c9-951a-42e1b13a2da5.png)

Then go to Server Manager\Local Server – Ethernet > assigned by DHCP. Right click on Ethernet and go to Propeties. In Propeties I disable IPv6 and change settings in Ipv4 using Propeties. Select “Use the following IP address” paste in the values: 

IP address: 10.0.100.56 
Subnet Mask: 255.255.255.0 

And save. 

Sing in on Win-DCC. In “Enter number to select an option: “I want to go to number eight for, 8) Network settings. Which directs me to this: 
![image](https://user-images.githubusercontent.com/42642927/227747114-06152bc2-de45-4bd4-a797-63ae9fe585e9.png)

In “Select network adapter index # (Blank=Cancel):” use index number 1.  It gives me a new page.

![image](https://user-images.githubusercontent.com/42642927/227747150-eb686719-44d8-4b9a-92da-ed4d5235da7c.png)

