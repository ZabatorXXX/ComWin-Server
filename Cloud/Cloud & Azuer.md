
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

8. Go back on Azuer > select sync groupe > add server endpoint
