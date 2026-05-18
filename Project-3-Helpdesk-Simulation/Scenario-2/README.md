# Scenario 2 — Password Reset

## What This Simulates
A user (Sarah Jones) has forgotten her password. The helpdesk technician resets the password from Active Directory and verifies the user can log in with the new credentials.

---

## Tools Used
- Active Directory Users and Computers (DC01)
- Client01 login screen

---

## Steps Performed

### Part A — Reset the Password
1. Opened Active Directory Users and Computers on DC01
2. Navigated to Finance OU → located Sarah Jones
3. Right clicked Sarah Jones → Reset Password
4. Entered new password meeting complexity requirements:
   - Minimum 10 characters
   - Uppercase, lowercase, number, special character
5. Unticked "User must change password at next logon"
6. Ticked "Unlock the user's account"
7. Clicked OK — received success confirmation

### Part B — Verify Login
8. Switched to Client01
9. At login screen → Other user → entered `MAYANKLAB\sjones`
10. Entered new password
11. Login successful — Welcome Sarah Jones

---

## Password Complexity Requirements

| Requirement | Detail |
|---|---|
| Minimum length | 10 characters |
| Uppercase letter | Required |
| Lowercase letter | Required |
| Number | Required |
| Special character | Required |

> Password complexity is enforced by the IT Password Policy GPO created in Project 1

---

## Screenshots

| File | Description |
|---|---|
| Capture_1 | Reset Password dialog open — Sarah Jones in Finance OU |
| Capture_2 | New password entered, "Unlock the user's account" ticked |
| Capture_3 | Confirmation — "The password for Sarah Jones has been changed" |
| Capture_4 | Welcome — Sarah Jones — login successful on Client01 |

---

## What I Learned
- Password resets in Active Directory are done via right click → Reset Password on the user object
- The complexity policy set in Project 1 enforces minimum password requirements across all domain users
- Ticking "Unlock the user's account" during reset is good practice even when the account is not locked
