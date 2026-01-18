# Active Directory Lab Setup (VMware)

This guide explains how to set up a basic **Active Directory (AD) lab** using **VMware**, **Windows Server**, and a **Windows 11 client**.
It is intended for **IT interview preparation** and hands-on Active Directory practice.

---

## Prerequisites

- VMware Workstation Player or Pro
- Windows Server 2022 or 2025 ISO
- Windows 11 **Pro or Enterprise** ISO (Home edition cannot join a domain)
- Minimum 8 GB RAM (16 GB recommended)
- Virtualization enabled in BIOS (Intel VT-x / AMD-V)

---

## Virtual Machine Setup

### Step 1: Install VMware
Download and install VMware Workstation Player:
https://www.vmware.com/products/workstation-player.html

---

### Step 2: Create Virtual Machines

You will create **two virtual machines**:
1. **Windows Server** – Domain Controller
2. **Windows 11** – Domain-joined client

---

### Step 3: Create a New Virtual Machine

1. Open VMware
2. Click **Create a New Virtual Machine**
3. Select **I will install the operating system later**
4. Click **Next**

---

### Step 4: Choose Guest Operating System

- **Windows Server VM**
  - OS: Microsoft Windows
  - Version: Windows Server 2022 or 2025

- **Windows 11 VM**
  - OS: Microsoft Windows
  - Version: Windows 11 x64

---

### Step 5: VM Hardware Configuration (Recommended)

| Component | Server | Windows 11 |
|---------|--------|------------|
| CPU | 2 cores | 2 cores |
| RAM | 4–6 GB | 4–6 GB |
| Disk | 60 GB | 60 GB |
| Network | NAT or Host-Only | Same as Server |

Both VMs **must be on the same virtual network**.

---

### Step 6: Attach ISO Files

1. Open **VM Settings**
2. Select **CD/DVD (SATA)**
3. Choose **Use ISO image file**
4. Attach:
   - Windows Server ISO to Server VM
   - Windows 11 ISO to Client VM

---

## Windows Server Installation

1. Power on the Windows Server VM
2. Select **Windows Server 2022 Standard Evaluation**
3. Choose **Desktop Experience**
4. Select **Custom: Install Windows only**
5. Select the primary disk and complete installation

---

## Initial Server Configuration

### Set Administrator Password
Create the local Administrator password after first boot.

---

### Rename the Server
1. Open **Server Manager → Local Server**
2. Change the computer name (example: `DC01`)
3. Restart the server

---

### Configure Static IP Address

Domain Controllers must use a static IP.

Example:
```
IP Address: 192.168.10.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.10.1
DNS Server: 192.168.10.10
```

---

### Verify Network and Time
- Confirm correct time zone
- Verify network connectivity

---

## Install Active Directory Domain Services

1. Open **Server Manager**
2. Click **Add roles and features**
3. Choose **Role-based or feature-based installation**
4. Select the local server
5. Check:
   - Active Directory Domain Services
   - DNS Server
6. Under Features, select:
   - Group Policy Management
7. Click **Install**

---

## Promote Server to Domain Controller

1. In Server Manager, click **Promote this server to a domain controller**
2. Select **Add a new forest**
3. Choose a root domain name (example: `corp.local`)
4. Set the **DSRM password**
5. Complete the prerequisite check
6. Click **Install** and allow the server to reboot

---

## Verify Active Directory

After reboot:
- Log in as `corp\Administrator`
- Open:
  - Active Directory Users and Computers
  - DNS Manager
  - Group Policy Management

---

## Windows 11 Client Setup

1. Install Windows 11 Pro or Enterprise
2. Set DNS to the Domain Controller IP:
```
192.168.10.10
```
3. Join the domain:
   - Settings → System → About → Domain Join
   - Domain: `corp.local`
4. Restart the client

---
