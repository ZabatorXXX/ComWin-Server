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


