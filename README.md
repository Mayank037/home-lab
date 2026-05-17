# 🖥️ Active Directory Home Lab — Windows Server 2022

**Built by:** Mayank Rale  
**GitHub:** [github.com/Mayank037/home-lab](https://github.com/Mayank037/home-lab)  
**Platform:** Oracle VirtualBox on Windows 11  
**Status:** ✅ Complete

---

## Overview

This project documents the build of a fully functional Active Directory home lab using Windows Server 2022 running inside a VirtualBox virtual machine. The lab simulates a real-world corporate IT environment including domain configuration, user provisioning, organisational unit structure, and Group Policy enforcement.

This lab was built to develop and demonstrate hands-on skills in Windows Server administration, Active Directory management, and IT support operations — directly relevant to Level 1/2 helpdesk and IT support roles.

---

## Lab Environment

| Component | Details |
|---|---|
| Host OS | Windows 11 |
| Virtualisation Software | Oracle VirtualBox |
| VM Name | DC01 |
| Guest OS | Windows Server 2022 Standard Evaluation |
| RAM Allocated | 4096 MB |
| CPU Allocated | 2 vCPUs |
| Storage | 50 GB virtual disk |
| Network Adapter | Intel PRO/1000 MT Desktop (NAT) |

---

## What Was Built

### Phase 1 — Virtual Machine Setup
- Installed Oracle VirtualBox on Windows 11 host
- Created VM (DC01) with 4GB RAM, 2 CPUs, 50GB disk
- Attached Windows Server 2022 evaluation ISO (4.70 GB)
- Selected Desktop Experience edition for GUI access
- Completed clean custom installation to unallocated disk

### Phase 2 — Network Configuration (Static IP)
Configured a static IP address on the server to ensure stable domain communication:

| Setting | Value |
|---|---|
| IP Address | 192.168.1.10 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.1.1 |
| Preferred DNS | 127.0.0.1 (loopback — server is its own DNS) |

### Phase 3 — Active Directory Domain Services Installation
- Opened Server Manager → Add Roles and Features
- Selected **Active Directory Domain Services** role
- Additional features automatically added: Group Policy Management, AD DS Tools, Active Directory Administrative Center, AD DS Snap-Ins
- Installation completed successfully on WIN-R0FLIQ67M6T

### Phase 4 — Domain Controller Promotion
- Promoted server to Domain Controller using the AD DS Configuration Wizard
- Created a **new forest** with root domain: `mayanklab.local`
- NetBIOS domain name: `MAYANKLAB`
- DNS Server: Yes
- Global Catalog: Yes
- Prerequisites check passed successfully
- Server automatically rebooted and logged in as `MAYANKLAB\Administrator`

### Phase 5 — Organisational Unit Structure
Created the following OU structure under `mayanklab.local`:

```
mayanklab.local
├── IT Department
├── Finance
├── Domain Controllers
├── Computers
└── Users
```

### Phase 6 — User Account Provisioning

| Full Name | Username | Department | Domain |
|---|---|---|---|
| John Smith | jsmith | IT Department | mayanklab.local |
| Sarah Jones | sjones | Finance | mayanklab.local |

Both accounts configured with:
- Secure password set
- "User must change password at next logon" disabled for lab purposes
- Accounts active and accessible

### Phase 7 — Group Policy Object (GPO)
Created and linked a GPO named **IT Password Policy** to the IT Department OU.

**Policy settings configured:**

| Policy | Setting |
|---|---|
| Maximum password age | 90 days |
| Minimum password age | 30 days |
| Minimum password length | 10 characters |
| Password must meet complexity requirements | Enabled |

---

## Skills Demonstrated

- Windows Server 2022 installation and configuration
- VirtualBox VM creation and management
- Static IP and DNS configuration
- Active Directory Domain Services installation
- Forest and domain creation
- Organisational Unit design
- User account provisioning and management
- Group Policy Object creation and linking
- Password policy enforcement
- IT documentation and SOP writing

---

## Screenshots

All screenshots documenting each phase of the build are included in the `/screenshots` folder of this repository, organised by phase:

- `Capture_1` — DC01 VM setup starting Windows Server installation
- `Capture_2` — ISO attached (4.70 GB), Install Now screen
- `Capture_3` — Custom installation type selected
- `Capture_4` — Drive 0 Unallocated Space (50 GB) selected
- `Capture_5` — Windows Server 2022 desktop (first login)
- `Capture_6` — Static IP configuration before changes
- `Capture_7` — Static IP set: 192.168.1.10 / DNS: 127.0.0.1
- `Capture_8` — Windows Server 2022 desktop, Server Manager open
- `Capture_9` — Add Roles and Features Wizard launched
- `Capture_10` — Role-based installation type selected
- `Capture_11` — Server WIN-R0FLIQ67M6T selected as destination
- `Capture_12` — Active Directory Domain Services role ticked
- `Capture_13` — Installation confirmation showing AD DS + Group Policy Management
- `Capture_14` — NetBIOS domain name set to MAYANKLAB
- `Capture_15` — Review Options: mayanklab.local domain confirmed
- `Capture_16` — Prerequisites check passed successfully
- `Capture_17` — MAYANKLAB\Administrator login screen (domain live)
- `Capture_18` — Windows Server 2022 desktop post-domain-promotion
- `Capture_19` — Active Directory Users and Computers showing mayanklab.local
- `Capture_20` — (additional documentation)
- `Capture_21` — IT Department OU creation
- `Capture_22` — AD structure showing Finance and IT Department OUs
- `Capture_23` — John Smith user creation (jsmith@mayanklab.local)
- `Capture_24` — Password configuration for jsmith
- `Capture_25` — John Smith account confirmed (jsmith@mayanklab.local)
- `Capture_26` — Sarah Jones account confirmed (sjones@mayanklab.local)
- `Capture_27` — Group Policy Management open, Forest: mayanklab.local
- `Capture_28` — GPM tree expanded showing Finance and IT Department OUs
- `Capture_29` — New GPO named "IT Password Policy" being created
- `Capture_30` — Minimum password length set to 10 characters
- `Capture_31` — Maximum password age set to 90 days
- `Capture_32` — Final password policy: complexity enabled, all settings configured


---

## What I Learned

- How to build and configure a Windows Server domain controller from scratch in a virtualised environment
- How Active Directory structures work: forests, domains, OUs, and user objects
- How Group Policy Objects are created, linked, and applied at the OU level
- How DNS integrates with Active Directory (server as its own DNS resolver)
- How to document technical work in a professional, reproducible format

---

## Next Steps

- [ ] Project 2: Add a Windows 10 client VM and join it to `mayanklab.local`
- [ ] Project 3: Simulate helpdesk scenarios (account lockouts, password resets)
- [ ] Project 4: Network troubleshooting between DC01 and client VM
- [ ] CompTIA Network+ certification
- [ ] MS-900 Microsoft 365 Fundamentals certification

---

## About Me

Master of Business Information Systems graduate from the Australian National University (ANU), CompTIA A+ certified, actively building hands-on IT skills through home lab projects. Seeking IT support and helpdesk roles in Australia.

📧 ralemayank@gmail.com
