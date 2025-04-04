<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory set up on Azure</h1>
This tutorial shows how Active Directory is set up on Windows virtual machines within Azure.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
  
<h2>Domain Controller setup </h2>

First, I created a resource group in Azure and named it AD-Lab.

---

![ade1](https://github.com/user-attachments/assets/34c65dcb-8407-45da-9886-8085c1cb303b)

---

 I also set up a virtual network called ABV-Lab.
 
 ---
 
![a2](https://github.com/user-attachments/assets/b01629df-7494-425b-b2f7-10f8d5da7119)

---

Within this network, I launched a virtual machine named DC-1, selecting Windows Server 2022 as the image.

---


![aze3](https://github.com/user-attachments/assets/63d6ec00-a5f4-4444-96d1-1c5960417f9c)
![ade4](https://github.com/user-attachments/assets/813dafa1-2406-4e6a-93c0-8d446106e118)
![ade5](https://github.com/user-attachments/assets/2a6f0944-9a8b-4eab-89ae-e26fbc04a26e)

---

Next, I configured DC-1’s network settings and set its IP address to static to ensure stable connectivity.

---

![ade9](https://github.com/user-attachments/assets/6cd18429-1e97-4234-bce7-562a32de73af)

![ade10](https://github.com/user-attachments/assets/6ccf71b4-3c6f-408d-bd4a-9041c1c72044)

![ade11](https://github.com/user-attachments/assets/57afc05a-2160-4b88-bd09-ecbd93befddb)

---

Then, I created another virtual machine, Client-1, using a standard Windows 10 image (not a server version), ensuring it was placed on the same subnet as DC-1.

---

![ade6](https://github.com/user-attachments/assets/811493e1-bacd-48ae-bf3b-c3a978702bb6)

![ade7](https://github.com/user-attachments/assets/198fa827-5e32-4044-976d-03574397e6cc)

![ade8](https://github.com/user-attachments/assets/653cbedf-5ad2-43e4-b2bc-7177164a1313)

---

I retrieved DC-1’s public IP address, signed into it, and disabled the firewall by turning off the Domain, Private, and Public profile firewalls.

---

![ade12](https://github.com/user-attachments/assets/1d8997fa-4cb0-429e-976b-79d635b37992)

![ade13](https://github.com/user-attachments/assets/2866823c-8537-4185-bbfb-aa29333a5b22)

![firewall](https://github.com/user-attachments/assets/f9f7ea4f-9f86-4da5-a5fd-fc4183cd350d)

---



Afterward, I updated Client-1’s DNS settings to point to DC-1’s private IP address. I then restarted Client-1 and signed into it.

---

![ade14](https://github.com/user-attachments/assets/cd0259c7-f128-4945-854d-5df28f43d2b6)

![ade15](https://github.com/user-attachments/assets/754bd832-081d-49b4-b6a9-4e6a43ff7ad9)

![ade15 (1)](https://github.com/user-attachments/assets/a1cd5411-3e7a-4728-9e3d-b8c612a169ab)

![ade19](https://github.com/user-attachments/assets/ae2e1e60-05c9-4672-8b86-01ceea2d1b32)

---

Once signed in, I tested the connectivity by pinging the domain controller to ensure it was reachable. To confirm everything was configured correctly, I ran the command ipconfig /all on Client-1 to verify that the DNS server was set to DC-1’s private IP address.

---

![ade20](https://github.com/user-attachments/assets/b965231b-2526-4e64-8490-bb4c6a76dfad)

![ade21a](https://github.com/user-attachments/assets/0f9d6466-f550-456c-b41e-530fa67b591b)

---

<h2>Installing Active Directory </h2>

Now that the domain and Client-1 are set up, let's proceed with installing Active Directory.

---

I started by going to Add Roles and Features in Server Manager, then selected Active Directory Domain Services.

---
![ade1](https://github.com/user-attachments/assets/8130b164-6baa-4302-87c1-77664d6ba2a2)
![ade2](https://github.com/user-attachments/assets/17d8e95c-71af-43af-be7f-53128dc3f33b)

---


I clicked Next until I reached the installation screen. After the installation finished, I clicked on the flag with the yellow warning sign and selected Promote this server to a domain controller.

---

![ade3](https://github.com/user-attachments/assets/9157d9c0-3b69-4dcc-8199-34813d47d959)
![ade4](https://github.com/user-attachments/assets/11c93a93-3765-4286-a42a-c7d684c2d6bf)

---

I chose to Add a new forest and set the domain name as myadlab.com. Whatever domain name you choose, make sure to remember it.

---

![ade5](https://github.com/user-attachments/assets/cac4d3f4-bbc5-4ac7-ad70-cea5274512bb)

---

For the domain controller options, I kept it simple by setting the password to Password1. I unchecked the DNS delegation option and clicked Next until I reached the Install button. Once ready, I clicked Install and allowed the installation to complete. The server automatically restarted after the installation.

---

![ad6](https://github.com/user-attachments/assets/a490e07b-a539-43af-92e5-3f612be34abd)
![ad7](https://github.com/user-attachments/assets/ef95c0af-4e78-4482-9e05-0dc988486edf)
![ad8](https://github.com/user-attachments/assets/644703bd-52b1-4841-aaf6-12ea4967f6e2)

---

After the restart, I logged in as a domain user. For the login, I used myadlab.com\labuser with the password Cyberlab123!.

---

![ad9](https://github.com/user-attachments/assets/d2e38282-44e8-4f62-92fe-3ea2fc4a22ab)

---

<h2> Creating a Domain Admin and adding Client-1 as a Domain user </h2>

Now that Active Directory is installed, we’ll set up a Domain Admin and add Client-1 as a user of the domain.

I started by going to DC-1 and opening Active Directory Users and Computers. 

Then, I navigated to myadlab.com, right-clicked on it, selected New > Organizational Unit, and named it _EMPLOYEES. I repeated the process to create another Organizational Unit called _ADMINS.

---

![a10](https://github.com/user-attachments/assets/08d16c65-86b0-4903-9b11-e2ee5271f233)
![ade11](https://github.com/user-attachments/assets/044cb3c4-5527-4eef-af72-98cb5e550f27)

---

With the folders set up, I went to the _ADMINS folder, right-clicked, and selected New > User. I entered a name and logon name—Peter Parker for the name and Not_Spiderman for the logon name. 

For lab purposes, I set the password to Cyberlab123! and changed the password setting to Password Never Expires.

---

![a12](https://github.com/user-attachments/assets/8aeae419-fa72-47f0-aa35-6b442498c3fd)
![ade13](https://github.com/user-attachments/assets/b2484316-cceb-40e3-b8eb-e3ddada7f591)

---

Next, I made Peter a Domain Admin. 

To do this, I clicked on Peter Parker’s name, went to Properties > Member Of > Add, then typed Domain Admins and clicked Check Name. Once it refreshed, I clicked Apply, making Peter a Domain Admin.

---

![ade14](https://github.com/user-attachments/assets/ecca5262-dc6f-49d5-8881-016ec1e61a36)
![ade15](https://github.com/user-attachments/assets/d505b858-31a6-4f3b-9e2b-30c6b57a67fc)

---

Since Peter is now a Domain Admin, I signed out of the admin account and used Peter’s account for the remaining tasks.

I then signed into Client-1, opened Settings, and clicked on Rename this PC (Advanced).

Next, I clicked Change, selected Member of Domain, entered the domain name, and logged in with the Peter Parker admin account.

The VM welcomed me into the domain, and I restarted the system.

---

![adelab last](https://github.com/user-attachments/assets/78856636-1177-46c1-9bd5-7fa6b238a3f2)
![adelab3](https://github.com/user-attachments/assets/ce37581c-a04d-4cb0-883d-621e8d2e6a05)

---

After the restart, I returned to DC-1, opened Active Directory Users and Computers, and checked under Computers to ensure that Client-1 was listed.

---

![ad16](https://github.com/user-attachments/assets/f0406eec-7fc5-49e7-a030-2273416ea796)

---

This setup is essential for configuring Active Directory for future labs that will require domain integration.
