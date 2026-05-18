# Scenario 4 — Disable and Enable Account

## What This Simulates
An employee (John Smith) goes on extended leave. The helpdesk technician disables the account to block access, verifies login is blocked on Client01, then re-enables the account and confirms access is restored.

---

## Tools Used
- Active Directory Users and Computers (DC01)
- Command Prompt — `gpupdate /force`, `klist purge` (Client01)
- Client01 login screen

---

## Steps Performed

### Part A — Disable the Account
1. Opened Active Directory Users and Computers on DC01
2. Navigated to IT Department OU → located John Smith
3. Right clicked John Smith → Disable Account
4. Confirmation: **"Object John Smith has been disabled"**
5. John Smith account now shows a down arrow (disabled) icon in AD

### Part B — Verify Access is Blocked
6. Switched to Client01
7. Ran `gpupdate /force` to clear cached policy
8. Ran `klist purge` to clear cached Kerberos tickets
9. Attempted login as `MAYANKLAB\jsmith`
10. Error displayed: **"Your account has been disabled. Please see your system administrator"**

### Part C — Re-enable the Account
11. Returned to DC01 → Active Directory Users and Computers
12. Right clicked John Smith → Enable Account
13. Confirmation: **"Object John Smith has been enabled"**
14. Down arrow icon removed — account active again

### Part D — Verify Login Restored
15. Switched to Client01
16. Logged in as `MAYANKLAB\jsmith` with correct password
17. Login successful — Welcome John Smith

---

## Key Commands Used

| Command | Purpose |
|---|---|
| `gpupdate /force` | Forces immediate Group Policy refresh on the client |
| `klist purge` | Clears cached Kerberos authentication tickets |

> Both commands were required because Windows caches domain credentials locally. Without clearing the cache, a disabled account could still log in using stored credentials.

---

## Screenshots

| File | Description |
|---|---|
| Capture_1 | Right click John Smith — Disable Account option visible |
| Capture_2 | Confirmation — "Object John Smith has been disabled" |
| Capture_3 | AD Users and Computers — disabled icon on John Smith |
| Capture_4 | Client01 — "Your account has been disabled" error |
| Capture_5 | Right click John Smith — Enable Account option visible |
| Capture_6 | Confirmation — "Object John Smith has been enabled" |
| Capture_7 | AD Users and Computers — John Smith account active again |
| Capture_8 | Welcome — John Smith — login successful after re-enable |

---

## What I Learned
- Disabling an account immediately blocks all new authentication attempts from the domain controller
- Windows caches credentials locally — `gpupdate /force` and `klist purge` are required to clear the cache and force a fresh authentication check against the DC
- Re-enabling an account in AD restores full access instantly without any other changes needed
