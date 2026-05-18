# 💻 Project 2 — Domain Join (Windows 10 Client to Active Directory)

**Built by:** Mayank Rale  
**GitHub:** [github.com/Mayank037/home-lab](https://github.com/Mayank037/home-lab)  
**Platform:** Oracle VirtualBox on Windows 11  
**Status:** ✅ Complete

---

## Overview

This project extends the Active Directory home lab built in Project 1 by adding a Windows 10 client virtual machine and joining it to the `mayanklab.local` domain. The lab simulates a real-world helpdesk scenario where a technician provisions a new workstation, configures its network settings, and connects it to the corporate domain — then verifies domain authentication by logging in as an Active Directory user.

---

## Lab Environment

| Component | Details |
|---|---|
| Host OS | Windows 11 |
| Virtualisation Software | Oracle VirtualBox |
| Domain Controller VM | DC01 — Windows Server 2022 (from Project 1) |
| Client VM Name | Client01 |
| Client Guest OS | Windows 10 (64-bit) |
| RAM Allocated | 2048 MB |
| Storage | 50 GB virtual disk |
| Network Adapter | Intel PRO/1000 MT Desktop (Internal Network — `intnet`) |
| Domain | mayanklab.local |

---

## What Was Built

### Phase 1 — Client VM Creation

- Opened Oracle VirtualBox Manager (DC01 already running from Project 1)
- Created new VM named **Client01**
- Selected Windows 10 (64-bit) as OS version
- Attached Windows 10 ISO (`Windows.iso`, 4.56 GB)
- Allocated 2048 MB RAM, 50 GB virtual disk
- Set Network Adapter to **Internal Network (`intnet`)** to communicate with DC01

### Phase 2 — Windows 10 Installation

- Booted Client01 from the attached ISO
- Completed clean Windows 10 installation
- Created a local account named **LocalAdmin** during setup
- Arrived at Windows 10 desktop — client VM operational

### Phase 3 — Static IP and DNS Configuration

For Client01 to find and join the domain, its DNS must point to DC01 (the domain controller). Configured a static IP via **Control Panel → Network and Internet → Network Connections → Ethernet Properties → IPv4**:

| Setting | Value |
|---|---|
| IP Address | 192.168.1.20 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.1.10 |
| Preferred DNS | 192.168.1.10 (DC01 — the domain controller) |

> DNS pointing to DC01 is critical — without it, Windows cannot locate the domain to join.

### Phase 4 — Domain Join

Joined Client01 to `mayanklab.local` via **Settings → About → Rename this PC (advanced) → Change → Domain**:

- Selected **Domain** radio button
- Entered domain name: `mayanklab.local`
- Clicked OK — Windows prompted for domain credentials
- Entered `MAYANKLAB\Administrator` with the domain admin password
- Received confirmation: **"Welcome to the mayanklab.local domain."**
- Restarted Client01 to apply changes

### Phase 5 — Domain User Login Verification

After restart, verified that Active Directory user accounts created in Project 1 could authenticate on the domain-joined client:

- At the login screen, selected **Other user**
- Entered `MAYANKLAB\jsmith` (John Smith — IT Department)
- Entered password
- Login screen confirmed: **"Sign in to: MAYANKLAB"**
- Logged in successfully — **"Welcome — John Smith"** displayed

This confirms end-to-end Active Directory authentication working across two VMs on the same internal network.

---

## Skills Demonstrated

- VirtualBox VM creation and network configuration
- Windows 10 installation and initial setup
- Static IP and DNS configuration on a client machine
- Internal network setup between two VirtualBox VMs
- Domain join procedure (GUI method)
- Active Directory credential authentication from a client workstation
- End-to-end verification of domain user login
- IT documentation and SOP writing

---

## Screenshots

All screenshots are in the `/screenshots` folder, organised by phase:

| File | Description |
|---|---|
| Capture_1 | DC01 login screen — MAYANKLAB\Administrator (domain confirmed live) |
| Capture_2 | New VM wizard — Client01 being created, Windows 10 ISO attached |
| Capture_3 | VirtualBox Manager — DC01 and Client01 both running, Internal Network confirmed |
| Capture_4 | Client01 first boot — Windows 10 desktop |
| Capture_5 | IPv4 Properties — static IP 192.168.1.20, DNS set to 192.168.1.10 (DC01) |
| Capture_6 | Computer Name/Domain Changes — mayanklab.local entered |
| Capture_7 | Windows Security prompt — MAYANKLAB\Administrator credentials entered |
| Capture_8 | "Welcome to the mayanklab.local domain" confirmation |
| Capture_9 | Restart prompt — domain join changes applied |
| Capture_10 | Client01 login screen — MAYANKLAB\jsmith being entered |
| Capture_11 | "Welcome — John Smith" — domain user successfully logged in |

---

## What I Learned

- How to configure two VirtualBox VMs to communicate on the same internal network
- How DNS resolution is essential for domain join — the client must point to the DC as its DNS server
- How the domain join process works end-to-end: network config → credentials → confirmation → restart
- How Active Directory user accounts authenticate on domain-joined machines
- How to verify a successful domain join by logging in as a domain user on the client

---

## Next Steps

- [ ] Project 3: Simulate helpdesk scenarios (account lockouts, password resets)
- [ ] Project 4: Network troubleshooting between DC01 and Client01

---

## About Me

Master of Business Information Systems graduate from the Australian National University (ANU), CompTIA A+ certified, actively building hands-on IT skills through home lab projects. Seeking IT support and helpdesk roles in Australia.

📧 ralemayank@gmail.com
