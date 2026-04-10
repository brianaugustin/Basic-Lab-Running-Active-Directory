# Basic-Home-Lab-Running-Active-Directory
### Basic home lab running Active Directory with a domain controller and users.

I built a home lab by deploying Windows Server 2025 as a Domain Controller for the brian.local forest, configuring it with a static IP of 192.168.204.131. I installed and verified essential roles including Active Directory Domain Services (AD DS) and DNS, then configured Windows 11 client machines to point to the server for name resolution. After confirming connectivity via nslookup and successful pings, I joined the client machines to the domain to enable centralized user management and group policy testing.

# Setting up Windows 2025 Server

### Server Role & Infrastructure Setup
* **Installed Core Roles:** I used **Server Manager** to install and verify essential infrastructure roles, specifically **Active Directory Domain Services (AD DS)** and **DNS Server**.
* **Verified Network Configuration:** I used the `ipconfig` command on the Windows Server 2025's Command Prompt to confirm the server's current network settings, identifying the IPv4 address as **192.168.204.131**.

### Network Customization
* **Configured Static IP:** I manually assigned a **static IPv4 address** on the Windows Server 2025 to the server to ensure its role as a Domain Controller remains stable. I set the Subnet Mask to `255.255.255.0` and the Default Gateway to `192.168.204.2`.
* **Set DNS Resolution:** I configured the **Preferred DNS server** to the loopback address (`127.0.0.1`) so the server resolves names through itself, and added Google's public DNS (`8.8.8.8`) as an alternate for external connectivity.
* **Managed DNS Services:** I accessed the **DNS Manager** to oversee the forward lookup zones and server health, ensuring the `WIN-6T124H35KRB` server was online and resolving correctly within the environment.

![0Capture - Listed Installed Roles   Features](https://github.com/user-attachments/assets/4a04378d-e204-41e9-b3d4-6c742a7f1edb)
![1Capture-Windows Server IpConfig](https://github.com/user-attachments/assets/3e71423a-c289-417f-a5f7-b76dba132ff5)
![2Capture-Ip Static IP Server](https://github.com/user-attachments/assets/d756b4f4-3b47-4fc8-98cb-438357ed78f1)
![3Capture-DNS Server](https://github.com/user-attachments/assets/c4abc372-6fdf-43a5-bc29-d7c136872c8c)

---
# Setting up PCs for DNS Server

### **DNS Configuration**
I updated the network adapter settings on the **Mark-Win** and **Tim-Win** client machines. While keeping the IP addresses dynamic, I manually configured the **Preferred DNS server** to point directly to my Domain Controller at `192.168.204.131`. This step is crucial for allowing the workstations to locate and communicate with the Active Directory forest.

### **Interface Verification**
I used the Command Prompt to audit the network stack on the client machines. By running `ipconfig /all`, I verified that the clients were successfully receiving their IP addresses via DHCP (such as `192.168.204.134` and `192.168.204.136`) and, more importantly, that the DNS settings were correctly applied, showing my Domain Controller as the primary resolver.

### **Resolution & Connectivity Testing**
I performed a series of tests from the client workstations to ensure the infrastructure was ready. I ran an `nslookup` for the `brian.local` domain, which successfully resolved to the server's static IP. I followed this with a `ping` test, which confirmed a stable, low-latency connection between the clients and the server with no packet loss.


![4Capture-MARK DNS IPv4 Config](https://github.com/user-attachments/assets/515090aa-bd27-4c60-9a71-b6e17b8e2f91)
![5Capture-TIM DNS IPv4 Config](https://github.com/user-attachments/assets/1dab1fe9-7668-4fb8-bec9-bff9bde32a63)
![6Capture-Mark Ipconfig All](https://github.com/user-attachments/assets/ca94e809-6d36-4c18-a023-c5acc11be871)
![6Capture-Brian Ipconfig All](https://github.com/user-attachments/assets/897fe696-c8b0-4f73-a95a-2bee3d23addf)
![7  ping brian local on server from brian pc](https://github.com/user-attachments/assets/f61cff54-a928-49c3-9988-0ac4965470dc)

---
# Joining Domain

In these images, I initiated the process of joining the workstation to the newly created domain.

I navigated to the Access work or school section within the Windows Accounts settings. Using the Join a domain wizard, I entered the root domain name brian.local. This step triggers the workstation to search the network for the Domain Controller I previously configured, using the DNS settings I manually assigned earlier to locate the forest.

![8  domain page](https://github.com/user-attachments/assets/53ff51b4-3c6e-4f75-9b8e-8738d0845a28)
![9  domain page](https://github.com/user-attachments/assets/aa195440-01ff-466a-900f-83a703f17a46)

---
# Domain Successfully Connected

In these images, I finalized the integration of the client workstations into the Active Directory environment and verified their status on the server.

### **Domain Authentication**
I successfully joined a workstation to the domain. The screenshot shows the **Windows Security** prompt where I authenticated the join request using the **Domain Administrator** credentials. By entering the administrator username and password for `brian.local`, I authorized the machine to be added as a trusted member of the forest.

### **Active Directory Verification**
I switched over to the **Domain Controller** to confirm the operation was successful. Within the **Active Directory Users and Computers** management console, I navigated to the **Computers** container. I verified that the workstation—listed as `DESKTOP-7MRGQF6`—is now officially registered as a computer object in the domain, confirming that the client is fully integrated and ready for centralized management.

![10  Domain Login](https://github.com/user-attachments/assets/07d4af89-2a74-4639-9a6d-3b5cce690b69)
![11  Listed Computers on Domain](https://github.com/user-attachments/assets/36226c95-fb47-412c-8220-2b07fe0f530c)


---
# New Active Directory User - Simon

In this step, I used **Active Directory Users and Computers** on the Domain Controller to provision a new user account. I created the user **Simon Says** with the logon name `simon@brian.local`. 

I configured the account settings to ensure the **password never expires** and deselected the requirement for the user to change their password at the next logon, making it ready for immediate use in my lab environment. This user object now exists within the centralized database, allowing "Simon" to authenticate from any workstation currently joined to the `brian.local` domain.

![12  New user Simon](https://github.com/user-attachments/assets/a6ec70d7-5d8a-433c-be4f-c13b9d3b106a)


---
# Simon Logging into Domain on PC

In these images, I performed the first domain login for the newly created user to verify that the Active Directory authentication flow is working correctly.

### **Domain Authentication**
I navigated to the Windows login screen on the workstation and selected **Other user**. I entered the domain credentials for the account I just created, using the format `BRIAN\simon`. This step demonstrates the workstation communicating with the Domain Controller to verify the credentials against the Active Directory database.

### **Profile Provisioning & Session Verification**
Once authenticated, I successfully logged into the desktop. Since this was a fresh domain login, Windows automatically provisioned a new local user profile for **Simon Says**. I then verified the active session, confirming that the workstation is now running under a domain-user context rather than a local account, completing the end-to-end lab setup.

![13  Simon logging in](https://github.com/user-attachments/assets/ef52068a-2cab-439a-be93-325191b01039)
![14  Simon logged in](https://github.com/user-attachments/assets/1fd4cb13-22e1-421e-8467-10128705ecb7)













# Images
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
