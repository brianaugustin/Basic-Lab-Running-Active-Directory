# Basic-Home-Lab-Running-Active-Directory
### Basic home lab running Active Directory with a domain controller and users.

I built a home lab by deploying Windows Server 2025 as a Domain Controller for the brian.local forest, configuring it with a static IP of 192.168.204.131. I installed and verified essential roles including Active Directory Domain Services (AD DS) and DNS, then configured Windows 11 client machines to point to the server for name resolution. After confirming connectivity via nslookup and successful pings, I joined the client machines to the domain to enable centralized user management and group policy testing.

---

![0Capture - Listed Installed Roles   Features](https://github.com/user-attachments/assets/4a04378d-e204-41e9-b3d4-6c742a7f1edb)
![1Capture-Windows Server IpConfig](https://github.com/user-attachments/assets/3e71423a-c289-417f-a5f7-b76dba132ff5)
![2Capture-Ip Static IP Server](https://github.com/user-attachments/assets/d756b4f4-3b47-4fc8-98cb-438357ed78f1)
![3Capture-DNS Server](https://github.com/user-attachments/assets/c4abc372-6fdf-43a5-bc29-d7c136872c8c)
![4Capture-MARK DNS IPv4 Config](https://github.com/user-attachments/assets/515090aa-bd27-4c60-9a71-b6e17b8e2f91)
![5Capture-TIM DNS IPv4 Config](https://github.com/user-attachments/assets/1dab1fe9-7668-4fb8-bec9-bff9bde32a63)
![6Capture-Mark Ipconfig All](https://github.com/user-attachments/assets/ca94e809-6d36-4c18-a023-c5acc11be871)
![6Capture-Brian Ipconfig All](https://github.com/user-attachments/assets/897fe696-c8b0-4f73-a95a-2bee3d23addf)
![7  ping brian local on server from brian pc](https://github.com/user-attachments/assets/f61cff54-a928-49c3-9988-0ac4965470dc)
![8  domain page](https://github.com/user-attachments/assets/53ff51b4-3c6e-4f75-9b8e-8738d0845a28)
![9  domain page](https://github.com/user-attachments/assets/73c39e60-37b3-4ef4-82eb-25ce8f7e0b69)
![10  Domain Login](https://github.com/user-attachments/assets/07d4af89-2a74-4639-9a6d-3b5cce690b69)
![11  Listed Computers on Domain](https://github.com/user-attachments/assets/36226c95-fb47-412c-8220-2b07fe0f530c)
![12  New user Simon](https://github.com/user-attachments/assets/a6ec70d7-5d8a-433c-be4f-c13b9d3b106a)
![13  Simon logging in](https://github.com/user-attachments/assets/ef52068a-2cab-439a-be93-325191b01039)
![14  Simon logged in](https://github.com/user-attachments/assets/1fd4cb13-22e1-421e-8467-10128705ecb7)
