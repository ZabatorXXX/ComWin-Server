
Create V Net

### 1. Create New Resource Group 

![image](https://user-images.githubusercontent.com/42642927/227194038-637f2c41-a6f9-4720-baf1-0d315f3986bf.png)

### 2. Name the Vnet 

![image](https://user-images.githubusercontent.com/42642927/227194484-fc0087de-7fe1-4f94-ba47-82b2b6f70fbf.png)

### 3. Choose location
![image](https://user-images.githubusercontent.com/42642927/227194683-8e04bea6-63e8-46d2-bdc2-e788849a85ef.png)


### 4.Strat with Ip configuration
![image](https://user-images.githubusercontent.com/42642927/227195927-bba5e9d0-2895-43b1-a0b4-082df4d5997d.png)

### 5. Create subnet
![image](https://user-images.githubusercontent.com/42642927/227196651-f991f34a-7ed1-4c8e-86b5-ff7452f338c9.png)

### 6. Review + create
![image](https://user-images.githubusercontent.com/42642927/227198050-914c5399-7a78-4008-8d86-804e0b07c2e4.png)

### 7. Create a Gateway Subnet 
![image](https://user-images.githubusercontent.com/42642927/227204663-c927ebae-3716-4de7-8c4f-1c3c32538df1.png)

### 8. Create Virtual Network Gateway 

![image](https://user-images.githubusercontent.com/42642927/227206961-9e3e536d-4cd5-4a5b-9089-500d15a6604b.png)


 

### 9. Change SKU 
![image](https://user-images.githubusercontent.com/42642927/227207479-dc6cb783-4875-4357-9206-2058028856e2.png)

 

 

### 10. Name you're Public Ip address 
![image](https://user-images.githubusercontent.com/42642927/227207658-77dbc891-05a6-48f2-9560-8c81fde1c396.png)




### 11. Review + create 
![image](https://user-images.githubusercontent.com/42642927/227211187-97c7a8f6-082c-4188-a1c1-15e11ce5cece.png)

### 12. Open PowerShell and create Self-sign root - client certificate 

'''  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature -Subject "CN=WinSec" -KeyExportPolicy Exportable -HashAlgorithm sha256 -KeyLength 2048 -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign '''

 

AzuerUser

Password12345!

https://techcommunity.microsoft.com/t5/itops-talk-blog/step-by-step-creating-an-azure-point-to-site-vpn/ba-p/326264

https://www.youtube.com/watch?v=Gb3YE-0gBWQ&t=911s
