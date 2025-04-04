<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


# 🖥️ Active Directory Lab Setup in Azure

This guide outlines how to set up a basic Active Directory environment in Azure using two virtual machines: a Domain Controller (`DC-1`) and a Client (`Client-1`), both connected within the same virtual network.

---

## ✅ Setup Domain Controller (DC-1)

1. Create a **Resource Group** in your preferred region.
2. Create a **Virtual Network** and a **Subnet** (e.g., 10.0.0.0/16 and 10.0.0.0/24).
3. Create a **Windows Server 2022 VM** named `DC-1` with the following credentials:
   - **Username:** `labuser`
   - **Password:** `Cyberlab123!`
4. After the VM is created, set `DC-1`’s **Private IP address** to **static**.
5. Log into the `DC-1` VM and **disable the Windows Firewall** (for testing purposes only).

---

## 🧑‍💻 Setup Client VM (Client-1)

1. Create a **Windows 10 VM** named `Client-1` using the same credentials:
   - **Username:** `labuser`
   - **Password:** `Cyberlab123!`
2. Attach `Client-1` to the **same region and Virtual Network** as `DC-1`.
3. Set `Client-1`’s **DNS settings** to the **Private IP address** of `DC-1`.
4. Restart the `Client-1` VM from the Azure Portal.
5. Log into `Client-1` and attempt to **ping `DC-1`'s private IP address** to test connectivity.
6. Open **PowerShell** and run `ipconfig /all` to verify:
   - Ping to `DC-1` is successful.
   - DNS server is correctly set to `DC-1`'s private IP.

---

> ⚠️ **Important:**  
> These credentials and settings are for lab/testing use only. Do not use default passwords in production environments.

---

## 🛠️– Install and Configure Active Directory

### 🧩 Install Active Directory Domain Services (AD DS)

1. Log into `DC-1`
2. Open **Server Manager**
3. Install the **Active Directory Domain Services** role
4. After installation, click **"Promote this server to a domain controller"**
5. Select **Add a new forest** and set the domain name as: mydomain.com

> ⚠️ This can be anything – just remember what you use
6. Set a **Directory Services Restore Mode (DSRM)** password
7. Complete the wizard and restart the server
8. Log back in using: mydomain.com\labuser


---

### 👤 Create a Domain Admin User

1. Open **Active Directory Users and Computers (ADUC)**
2. Create the following Organizational Units:
- `_EMPLOYEES`
- `_ADMINS`
3. In `_ADMINS`, create a user:
- **Name:** Jane Doe  
- **Username:** `jane_admin`  
- **Password:** `Cyberlab123!`
4. Add `jane_admin` to the **Domain Admins** security group
5. Log out and log back in as: mydomain.com\jane_admin


> ✅ From this point on, use `jane_admin` as your main admin account.

---

### 🔗 Join Client-1 to the Domain

1. Ensure the DNS setting on `Client-1` points to `DC-1`’s private IP (**already done**)
2. Restart `Client-1` (**already done**)
3. Log into `Client-1` as the local admin (`labuser`)
4. Join the PC to the domain: `mydomain.com`  
_(this will restart the computer)_
5. Log into `DC-1` and open **ADUC**
6. Create a new OU named `_CLIENTS`
7. Drag `Client-1` into the `_CLIENTS` OU


---

## 🧪 Part 2 – User Access & Automation

### 🖥️ Enable Remote Desktop for Domain Users on Client-1

1. Start both VMs if they’re off
2. Log into `Client-1` as: mydomain.com\jane_admin

3. Open **System Properties**
4. Go to the **Remote Desktop** tab
5. Allow access to **Domain Users**
6. You can now log into `Client-1` as a non-admin domain user

> 🔐 In production, this would typically be done using **Group Policy**.

---

### 👥 Bulk Create Domain Users via PowerShell

1. Log into `DC-1` as `jane_admin`
2. Open **PowerShell ISE** as Administrator
3. Create a new script file and paste in the provided user creation script
4. Run the script to create multiple users
5. Open **ADUC** and confirm the accounts appear in the `_EMPLOYEES` OU
6. Attempt to log into `Client-1` using one of the new user accounts  
> _(Take note of the passwords in the script)_

---

> ✅ **Lab Complete!** You've set up a domain, created admin and user accounts, joined a client machine, enabled RDP access, and tested domain logins.





