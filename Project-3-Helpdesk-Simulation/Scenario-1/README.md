# Scenario 1 — Account Lockout Policy Setup + Lockout + Unlock

## What This Simulates
A user (John Smith) repeatedly enters the wrong password and gets locked out of their account. The helpdesk technician configures the lockout policy, identifies the locked account in Active Directory, and unlocks it.

---

## Tools Used
- Group Policy Management Editor (DC01)
- Active Directory Users and Computers (DC01)
- Command Prompt — `gpupdate /force` (DC01 and Client01)

---

## Steps Performed

### Part A — Configure Account Lockout Policy
1. Opened Group Policy Management on DC01
2. Expanded Forest → Domains → mayanklab.local
3. Right clicked **Default Domain Policy** → Edit
4. Navigated to: Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy
5. Set **Account lockout threshold** to 5 invalid logon attempts
6. Windows auto-suggested remaining values — accepted:
   - Account lockout duration: 30 minutes
   - Reset account lockout counter after: 30 minutes
7. Ran `gpupdate /force` on DC01 to apply policy immediately
8. Ran `gpupdate /force` on Client01 to pull the updated policy

### Part B — Trigger the Lockout
9. On Client01, attempted login as `MAYANKLAB\jsmith` with wrong password 5 times
10. After 5th attempt — lockout error displayed

### Part C — Unlock the Account
11. On DC01, opened Active Directory Users and Computers
12. Navigated to IT Department OU → right clicked John Smith → Properties
13. Clicked Account tab → ticked **"Unlock account"** checkbox → Applied

### Part D — Verify Login
14. On Client01, logged in as `MAYANKLAB\jsmith` with correct password
15. Login successful — Welcome John Smith

---

## Policy Settings Configured

| Policy | Setting |
|---|---|
| Account lockout threshold | 5 invalid logon attempts |
| Account lockout duration | 30 minutes |
| Reset account lockout counter after | 30 minutes |

---

## Screenshots

| File | Description |
|---|---|
| Capture_1 | Account lockout threshold set to 5 invalid logon attempts |
| Capture_2 | All three lockout policy settings confirmed |
| Capture_3 | gpupdate /force running on DC01 |
| Capture_4 | gpupdate /force running on Client01 |
| Capture_5 | Failed login attempt — "The password is incorrect" |
| Capture_6 | Lockout error — "The referenced account is currently locked out" |
| Capture_7 | John Smith Properties open in AD Users and Computers |
| Capture_8 | Account tab — Unlock account checkbox ticked |
| Capture_9 | Welcome — John Smith — successful login after unlock |

---

## What I Learned
- Account lockout policy is not enabled by default in Active Directory — it must be configured via GPO
- `gpupdate /force` pushes policy changes immediately without waiting for the default refresh cycle
- Locked accounts are visible and manageable via the Account tab in AD Users and Computers
