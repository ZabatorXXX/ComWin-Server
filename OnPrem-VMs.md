
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

When ask in desktop experience to Select YES on question if I want to allow my network to discover other on the network.

![image](https://user-images.githubusercontent.com/42642927/217508597-a8497c95-3f64-436a-a55f-8bd6a694439f.png)


---

## Part 2 Visual changes

Now when we have set up the local VM it would be a good thing to nicening up them.  


1. Change Commuter Names 

To do this we will go to Server Manager\Local Server.  Click on the current name. 

![image](https://user-images.githubusercontent.com/42642927/227279012-8c568d1c-f513-4ee4-8483-1eeb1d72ac1e.png)

It will direct you to system propeties. 
![image](https://user-images.githubusercontent.com/42642927/227279375-9ca0efdf-e9b7-4cd4-8882-ac02f88e03e9.png)



