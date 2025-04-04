<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Curating Users, using Group policy and Managing Accounts</h1>

This tutorial demonstrates how to create and manage individual users, as well as efficiently manage multiple users at once using group policies.

If you need to set up Active Directory, refer to my [Active Directory Setup](https://github.com/AustinmJoseph/AD-Setup) tutorial.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell
- Active Directory Users and Computers(ADUC)

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2> Set up </h2>

To create users for our domain, we first need to ensure that domain users can connect via RDP (Remote Desktop Protocol).

Log into Client-1 using the admin account Not_Spiderman. Open System Properties, navigate to Remote Desktop, and allow domain users to access RDP.

---

![a1](https://github.com/user-attachments/assets/5cae0676-d3ca-4486-8620-ea2611952ab8)
![ade1](https://github.com/user-attachments/assets/b738e3d6-855f-47af-ac11-0ed9ef9a1e84)
![ade3](https://github.com/user-attachments/assets/cb49230f-875a-4d0a-86f8-6b68fd4817ba)

---

<h2> Creating Users </h2>

Now that the setup is complete, let’s create the users.

First, log into DC-1 and open PowerShell ISE as an administrator. 

Click on New Script and paste the [script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1). 

---

![ade4](https://github.com/user-attachments/assets/5e76d72e-5158-4805-9ee2-e78872c213c1)

---

For this lab, I created 10 employees and kept the password the same.

---

![a5](https://github.com/user-attachments/assets/2d3e4d7f-f8af-4788-b0dd-e5811bcdfa5f)

---

Next, open Active Directory Users and Computers (ADUC), navigate to _EMPLOYEES, and you should see the randomly generated users. 

Choose one of them and log into Client-1 to verify that it works.

---

![a6](https://github.com/user-attachments/assets/d600d0b8-7755-4613-9e47-5383ae751ee7)

![a7](https://github.com/user-attachments/assets/0b76e7d1-22db-4165-bdc8-b55ebb32c812)

![a8](https://github.com/user-attachments/assets/ae4f9b43-7136-4715-bd78-8a755e8f2308)

![a9](https://github.com/user-attachments/assets/dcbf54b1-5ff2-4303-a3d6-ed71df57bca0)

---

<h2> Group Policy and Account Managment</h2>


To practice working with Group Policy, we will create a new policy to intentionally lock an employee out, then reset and unlock their account.

- Step 1: Configure Account Lockout Policy
	1.	Log into DC-1, open Run, and enter gpmc.msc to open the Group Policy Management Console (GPMC).
	2.	Navigate to Default Domain Policy, right-click it, and select Edit.
	3.	In the Group Policy Management Editor, go to:
Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.
	4.	Click Account Lockout Threshold and set it to 5 failed attempts.
	5.	Apply the policy.
---

![a10](https://github.com/user-attachments/assets/d83ff7b3-5602-4339-b089-de0f03b65987)
![ade1](https://github.com/user-attachments/assets/f15db34c-482b-471f-8767-28420dd832cc)
![ade2](https://github.com/user-attachments/assets/8548358e-ebe1-4767-96f9-e5da1aaf8ae5)
![ade3](https://github.com/user-attachments/assets/54322d9f-2cf7-4414-9268-09d62e05e6cd)

---

- Step 2: Enforce the Policy on Client-1
	1.	Log into Client-1 using your admin account.
	2.	Open Command Prompt and enter: gpupdate /force

This forces the Group Policy update on the machine.

---

![a14](https://github.com/user-attachments/assets/0a19758e-5ef4-4c74-bac1-09eaa492bc89)

---

- Step 3: Lock an Employee Account
	1.	Attempt to log in 6 times using an employee account with the wrong password.
	2.	The account should now be locked.
---

![a15](https://github.com/user-attachments/assets/62e33fd4-b361-4226-ad28-843fe5a3ead8)

---


- Step 4: Unlock the Account in ADUC
	1.	On DC-1, open Active Directory Users and Computers (ADUC).
	2.	Navigate to _EMPLOYEES, find the locked account, and double-click it.
	3.	Go to the Account tab, check Unlock Account, and apply the changes.
	4.	Try logging in again—it should now work.

---

![ade3 (1)](https://github.com/user-attachments/assets/c8472b30-3273-4fb8-abb2-a5db6876532c)
![a17](https://github.com/user-attachments/assets/5135c983-56bf-4c09-99c6-9438d2a27a34)

---

- Step 5: Disable and Re-Enable the Account
	1.	In ADUC, right-click the same user and select Disable Account.
	2.	Try logging in—it should fail.
	3.	Go back to ADUC, right-click the user, and select Enable Account.
	4.	Log in again—it should now work.

---

![ade4](https://github.com/user-attachments/assets/6545356c-e1cd-4e1f-8e2b-9c74162d7c8d)
![a21](https://github.com/user-attachments/assets/1a66c739-919b-412d-bf37-09ae423a3fa1)
![ade5](https://github.com/user-attachments/assets/04489f5f-9588-48d5-9190-f0a7fd7cb761)
![a17](https://github.com/user-attachments/assets/adc06a97-e4fa-4b6b-b5f6-e5eb7193434b)

---

- Step 6: Check Event Logs

For additional monitoring, open Event Viewer, search for the employee’s name, and review the logs to track login attempts and account changes.

This exercise demonstrates how Group Policy can be used to enforce security measures and how ADUC can be used to manage user accounts efficiently.

---

![a22](https://github.com/user-attachments/assets/a31017ee-68dd-40d9-992a-477d1708c748)

---



















