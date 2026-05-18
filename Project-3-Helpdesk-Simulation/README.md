# 🎧 Project 3 — Helpdesk Simulation Scenarios

**Built by:** Mayank Rale  
**GitHub:** [github.com/Mayank037/home-lab](https://github.com/Mayank037/home-lab)  
**Platform:** Oracle VirtualBox on Windows 11  
**Status:** ✅ Complete

---

## Overview

This project simulates real-world Level 1/2 helpdesk scenarios using the Active Directory environment built in Projects 1 and 2. Each scenario replicates a common IT support ticket that a helpdesk technician would handle in a corporate environment — from account lockouts and password resets to new user onboarding and account management.

All scenarios are performed across two VMs: **DC01** (Windows Server 2022 Domain Controller) and **Client01** (Windows 10 domain-joined workstation).

---

## Lab Environment

| Component | Details |
|---|---|
| Host OS | Windows 11 |
| Virtualisation Software | Oracle VirtualBox |
| Domain Controller | DC01 — Windows Server 2022 |
| Client Machine | Client01 — Windows 10 |
| Domain | mayanklab.local |

---

## Scenarios

| # | Scenario | Tool Used |
|---|---|---|
| 1 | Account Lockout Policy Setup + Lockout + Unlock | Group Policy Management, AD Users and Computers |
| 2 | Password Reset | Active Directory Users and Computers |
| 3 | New User Onboarding | Active Directory Users and Computers |
| 4 | Disable and Enable Account | Active Directory Users and Computers |

---

## Scenario 1 — Account Lockout Policy + Lockout + Unlock

### What Was Simulated
A user (John Smith) repeatedly enters the wrong password and gets locked out. The helpdesk technician identifies the locked account in Active Directory and unlocks it.

### What Was Configured First
Before simulating the lockout, an Account Lockout Policy was configured via Group Policy Management since Windows Server does not enforce lockout by default.

**Lockout Policy Settings:**

| Policy | Setting |
|---|---|
| Account lockout threshold | 5 invalid logon attempts |
| Account lockout duration | 30 minutes |
| Reset account lockout counter after | 30 minutes |

### Steps Performed
1. Opened Group Policy Management on DC01
2. Edited **Default Domain Policy** → Computer Configuration → Windows Settings → Security Settings → Account Policies → Account Lockout Policy
3. Set lockout threshold to 5 invalid attempts
4. Ran `gpupdate /force` on DC01 and Client01 to apply policy immediately
5. Attempted login as `MAYANKLAB\jsmith` with wrong password 5 times on Client01
6. Account locked out — error message displayed on Client01
7. Opened Active Directory Users and Computers on DC01
8. Located John Smith in IT Department OU → Properties → Account tab
9. Ticked **"Unlock account"** checkbox → Applied
10. Verified successful login as jsmith on Client01

### Screenshots

| File | Description |
|---|---|
| Capture_1 | Group Policy Management — Default Domain Policy being edited |
| Capture_2 | Account Lockout Policy — threshold set to 5 attempts |
| Capture_3 | All three lockout policy settings configured |
| Capture_4 | gpupdate /force running successfully on DC01 |
| Capture_5 | Failed login attempt on Client01 as jsmith |
| Capture_6 | Account lockout error message on Client01 |
| Capture_7 | John Smith Properties open — Account tab showing locked status |
| Capture_8 | Unlock account checkbox ticked |
| Capture_9 | Successful login — Welcome John Smith |

---

## Scenario 2 — Password Reset

### What Was Simulated
A user (Sarah Jones) has forgotten her password. The helpdesk technician resets the password from Active Directory and verifies the user can log in with the new credentials.

### Steps Performed
1. Opened Active Directory Users and Computers on DC01
2. Located Sarah Jones in Finance OU
3. Right clicked → Reset Password
4. Entered new password meeting complexity requirements
5. Unticked "User must change password at next logon"
6. Ticked "Unlock the user's account"
7. Confirmed success message
8. Logged in as `MAYANKLAB\sjones` on Client01 with new password
9. Verified successful login

### Screenshots

| File | Description |
|---|---|
| Capture_1 | Right click Sarah Jones — Reset Password option visible |
| Capture_2 | Reset Password dialog — new password entered |
| Capture_3 | Confirmation — password for Sarah Jones has been changed |
| Capture_4 | Welcome — Sarah Jones — login successful on Client01 |

---

## Scenario 3 — New User Onboarding

### What Was Simulated
A new employee (Mike Rale) joins the HR Department. The helpdesk technician creates a new Organisational Unit, provisions a new user account, and verifies the user can log into the domain from Client01.

### Steps Performed
1. Opened Active Directory Users and Computers on DC01
2. Right clicked `mayanklab.local` → New → Organisational Unit → named **HR Department**
3. Right clicked HR Department OU → New → User
4. Entered user details — Mike Rale, username: `mrale`
5. Set password meeting complexity requirements
6. Unticked "User must change password at next logon"
7. Ticked "Password never expires" for lab purposes
8. Confirmed Mike Rale account created inside HR Department OU
9. Logged in as `MAYANKLAB\mrale` on Client01
10. Verified successful login — Welcome Mike Rale

### Screenshots

| File | Description |
|---|---|
| Capture_1 | New OU dialog — HR Department name entered |
| Capture_2 | AD structure showing HR Department OU created |
| Capture_3 | New user dialog — Mike Rale details filled in |
| Capture_4 | Password configuration for mrale |
| Capture_5 | Mike Rale account confirmed inside HR Department OU |
| Capture_6 | Client01 login screen — MAYANKLAB\mrale entered |
| Capture_7 | Welcome — Mike Rale — login successful |

---

## Scenario 4 — Disable and Enable Account

### What Was Simulated
An employee (John Smith) goes on extended leave. The helpdesk technician disables the account to block access, verifies login is blocked on Client01, then re-enables the account and confirms access is restored.

### Steps Performed
1. Opened Active Directory Users and Computers on DC01
2. Located John Smith in IT Department OU
3. Right clicked → Disable Account
4. Confirmed disabled status — down arrow icon appeared on account
5. Switched to Client01 — attempted login as `MAYANKLAB\jsmith`
6. Ran `gpupdate /force` and `klist purge` to clear cached credentials
7. Confirmed login blocked — "Your account has been disabled" error displayed
8. Returned to DC01 → right clicked John Smith → Enable Account
9. Confirmed account re-enabled — down arrow icon removed
10. Logged in as jsmith on Client01 — access restored successfully

### Screenshots

| File | Description |
|---|---|
| Capture_1 | Right click John Smith — Disable Account option visible |
| Capture_2 | Confirmation — jsmith has been disabled |
| Capture_3 | AD Users and Computers — disabled icon on John Smith |
| Capture_4 | gpupdate /force and klist purge run on Client01 |
| Capture_5 | Client01 — account disabled error message |
| Capture_6 | Right click John Smith — Enable Account option visible |
| Capture_7 | Confirmation — jsmith has been enabled |
| Capture_8 | Welcome — John Smith — login successful after re-enable |

---

## Skills Demonstrated

- Group Policy Object configuration and enforcement
- Account lockout policy setup and management
- Active Directory account unlock procedure
- Password reset and complexity policy compliance
- New Organisational Unit creation
- New user account provisioning and OU assignment
- Account disable and enable procedures
- Credential cache management (`gpupdate /force`, `klist purge`)
- End-to-end verification of all changes on a domain-joined client
- IT documentation and SOP writing

---

## What I Learned

- How to configure and enforce account lockout policies via Group Policy
- How `gpupdate /force` pushes policy changes immediately without waiting for the refresh cycle
- How Windows caches domain credentials locally and how to clear them with `klist purge`
- How all common helpdesk account management tasks are performed in Active Directory
- How to verify every change made on the server by testing on the client machine

---

---

## About Me

Master of Business Information Systems graduate from the Australian National University (ANU), CompTIA A+ certified, actively building hands-on IT skills through home lab projects. Seeking IT support and helpdesk roles in Australia.

📧 ralemayank@gmail.com
