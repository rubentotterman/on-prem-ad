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

