
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


# Create VM in Cloud


1. ![image](https://user-images.githubusercontent.com/42642927/229638741-58ce317f-4d5d-43d9-82ae-07b854e69f47.png)

2. ![image](https://user-images.githubusercontent.com/42642927/229638983-ce09157d-e8f5-43ca-906c-b61caa97eb46.png)

3. ![image](https://user-images.githubusercontent.com/42642927/229639180-99b33bec-e113-430b-b8ec-1a8c110f048d.png)

4. ![image](https://user-images.githubusercontent.com/42642927/229639286-cbaa4ae5-0e75-47aa-9ff6-d2a2f0789539.png)

5. ![image](https://user-images.githubusercontent.com/42642927/229639533-3a061223-8523-4849-b4dc-94df294e95ee.png)

6. ![image](https://user-images.githubusercontent.com/42642927/229639575-f18bb9b9-6927-43a7-8257-b02b70616fa6.png)

AzuerUser

Password12345!

7. ![image](https://user-images.githubusercontent.com/42642927/229639656-ea18d99f-6393-4eff-b019-44f86fc7439e.png)

8. Networkin





Sorce: - For VPN/Gatway

https://techcommunity.microsoft.com/t5/itops-talk-blog/step-by-step-creating-an-azure-point-to-site-vpn/ba-p/326264

https://www.youtube.com/watch?v=Gb3YE-0gBWQ&t=911s

https://www.youtube.com/watch?v=MorG47BTttU&t=597s 
 
https://www.youtube.com/watch?v=K0hgCWIbC1A
