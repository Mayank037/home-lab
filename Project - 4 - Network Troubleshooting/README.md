# 🌐 Project 4 — Network Troubleshooting

**Built by:** Mayank Rale  
**GitHub:** [github.com/Mayank037/home-lab](https://github.com/Mayank037/home-lab)  
**Platform:** Oracle VirtualBox on Windows 11  
**Status:** ✅ Complete

---

## Overview

This project demonstrates real-world network troubleshooting skills using the Active Directory lab environment built in Projects 1 and 2. Each scenario simulates a common network diagnostic task performed by a helpdesk or IT support technician, using built-in Windows command-line tools and network settings.

All scenarios are performed across two VMs: **DC01** (Windows Server 2022 Domain Controller) and **Client01** (Windows 10 domain-joined workstation).

---

## Lab Environment

| Component | Details |
|---|---|
| Host OS | Windows 11 |
| Virtualisation Software | Oracle VirtualBox |
| Domain Controller | DC01 — Windows Server 2022 — 192.168.1.10 |
| Client Machine | Client01 — Windows 10 — 192.168.1.20 |
| Network Type | Internal Network (intnet) |
| Domain | mayanklab.local |

---

## Scenarios

| # | Scenario | Tool Used |
|---|---|---|
| 1 | Verify connectivity between DC01 and Client01 | ping |
| 2 | Check IP configuration on both machines | ipconfig /all |
| 3 | Verify DNS resolution | nslookup |
| 4 | Trace network path between machines | tracert |
| 5 | Simulate network issue — disable and re-enable adapter | Network Connections |

---

## Scenario 1 — Verify Connectivity (ping)

### What Was Tested
Verified two-way connectivity between Client01 and DC01 using ping by IP address and domain name.

### Commands Run

| Machine | Command | Result |
|---|---|---|
| Client01 | `ping 192.168.1.10` | ✅ 4/4 replies |
| Client01 | `ping mayanklab.local` | ✅ 4/4 replies, resolved to 192.168.1.10 |
| DC01 | `ping 192.168.1.20` | ✅ 4/4 replies |

### Troubleshooting Finding
DC01 initially could not ping Client01 — all packets timed out with 100% loss. Root cause identified as **Windows Firewall on Client01 blocking ICMP requests** by default. Resolved by adding an inbound firewall rule:
```
netsh advfirewall firewall add rule name="Allow ICMPv4" protocol=icmpv4:8,any dir=in action=allow
```

### Screenshots

| File | Description |
|---|---|
| Capture_1 | Client01 pinging DC01 by IP — 4/4 replies |
| Capture_2 | Client01 pinging mayanklab.local — 4/4 replies |
| Capture_3 | DC01 pinging Client01 by IP — 4/4 replies after firewall fix |

---

## Scenario 2 — IP Configuration Check (ipconfig /all)

### What Was Tested
Verified full network configuration on both machines including IP address, subnet mask, default gateway, DNS server, and domain membership.

### Key Findings

**Client01:**

| Setting | Value |
|---|---|
| Host Name | DESKTOP-VDDJGSF |
| IP Address | 192.168.1.20 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.1.1 |
| DNS Server | 192.168.1.10 (DC01) |
| Primary DNS Suffix | mayanklab.local |

**DC01:**

| Setting | Value |
|---|---|
| Host Name | WIN-R0FLIQ67M6T |
| IP Address | 192.168.1.10 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.1.1 |
| DNS Server | 127.0.0.1 (loopback — server is its own DNS) |
| Primary DNS Suffix | mayanklab.local |

### Screenshots

| File | Description |
|---|---|
| Capture_1 | Client01 — ipconfig /all showing full network config |
| Capture_2 | DC01 — ipconfig /all showing full network config |

---

## Scenario 3 — DNS Resolution (nslookup)

### What Was Tested
Verified DNS resolution of domain names and hostnames across both machines using nslookup.

### Commands Run

| Machine | Command | Result |
|---|---|---|
| Client01 | `nslookup mayanklab.local` | ✅ Resolved to 192.168.1.10 |
| Client01 | `nslookup win-r0fliq67m6t.mayanklab.local` | ✅ Resolved to 192.168.1.10 |
| DC01 | `nslookup DESKTOP-VDDJGSF.mayanklab.local` | ✅ Resolved to 192.168.1.20 |

### Troubleshooting Finding
Initial nslookup of `DC01.mayanklab.local` returned **Non-existent domain** because the DC's actual hostname is **WIN-R0FLIQ67M6T** not DC01. Identified correct hostname via `ipconfig /all` and confirmed the Host (A) record in DNS Manager. DNS Manager also confirmed the following records registered in the mayanklab.local zone:
- `win-r0fliq67m6t` → 192.168.1.10
- `DESKTOP-VDDJGSF` → 192.168.1.20

### Screenshots

| File | Description |
|---|---|
| Capture_1 | Client01 — nslookup mayanklab.local resolves to 192.168.1.10 |
| Capture_2 | Client01 — nslookup win-r0fliq67m6t.mayanklab.local resolves to 192.168.1.10 |
| Capture_3 | DC01 — nslookup DESKTOP-VDDJGSF.mayanklab.local resolves to 192.168.1.20 |

---

## Scenario 4 — Trace Network Path (tracert)

### What Was Tested
Traced the network path between Client01 and DC01 to verify routing and hop count.

### Commands Run

| Machine | Command | Result |
|---|---|---|
| Client01 | `tracert 192.168.1.10` | ✅ 1 hop — direct connection confirmed |
| Client01 | `tracert mayanklab.local` | ✅ 1 hop — resolves and traces correctly |
| DC01 | `tracert 192.168.1.20` | ✅ 1 hop — direct connection confirmed |

### Screenshots

| File | Description |
|---|---|
| Capture_1 | Client01 — tracert to DC01 by IP |
| Capture_2 | Client01 — tracert to mayanklab.local |
| Capture_3 | DC01 — tracert to Client01 by IP |

---

## Scenario 5 — Simulate Network Issue (Disable/Enable Adapter)

### What Was Simulated
Simulated a user reporting sudden loss of network connectivity. Disabled the network adapter on Client01, verified connectivity was lost, then re-enabled it and confirmed connectivity was restored.

### Steps Performed
1. Verified ping to DC01 successful before making changes
2. Opened Network Connections on Client01
3. Right clicked Ethernet adapter → Disabled
4. Attempted ping to DC01 — confirmed network unreachable
5. Right clicked Ethernet adapter → Enabled
6. Verified ping to DC01 successful again

### Screenshots

| File | Description |
|---|---|
| Capture_1 | Ping successful before disabling adapter |
| Capture_2 | Ethernet adapter disabled in Network Connections |
| Capture_3 | Ping fails — network unreachable |
| Capture_4 | Ethernet adapter re-enabled |
| Capture_5 | Ping successful after re-enabling adapter |

---

## Skills Demonstrated

- Network connectivity verification using ping
- Full IP configuration analysis using ipconfig /all
- DNS name resolution testing using nslookup
- Network path tracing using tracert
- Windows Firewall rule management
- DNS Manager — viewing and understanding zone records
- Network adapter management — disable and enable
- Real-world troubleshooting methodology — identify, isolate, resolve, verify
- IT documentation and SOP writing

---

## What I Learned

- Windows Firewall blocks ICMP by default — a common cause of ping failures in corporate environments
- `ipconfig /all` reveals critical network details including DNS server assignment and domain membership
- The DNS server name shown in nslookup output reflects the actual hostname registered in DNS — not a display name
- `tracert` confirms direct connections (1 hop) vs routed connections (multiple hops)
- Disabling and re-enabling a network adapter is a fundamental first troubleshooting step for connectivity issues

---



## About Me

Master of Business Information Systems graduate from the Australian National University (ANU), CompTIA A+ certified, actively building hands-on IT skills through home lab projects. Seeking IT support and helpdesk roles in Australia.

📧 ralemayank@gmail.com
