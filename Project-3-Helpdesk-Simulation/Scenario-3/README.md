# Scenario 3 — New User Onboarding

## What This Simulates
A new employee (Mike Rale) joins the HR Department. The helpdesk technician creates a new Organisational Unit, provisions a new user account, assigns it to the correct OU, and verifies the user can log into the domain from Client01.

---

## Tools Used
- Active Directory Users and Computers (DC01)
- Client01 login screen

---

## Steps Performed

### Part A — Create HR Department OU
1. Opened Active Directory Users and Computers on DC01
2. Right clicked `mayanklab.local` → New → Organisational Unit
3. Named the OU: **HR Department**
4. Clicked OK — HR Department OU appeared in the AD structure

### Part B — Create the New User
5. Right clicked HR Department OU → New → User
6. Filled in user details:
   - First name: Mike
   - Last name: Rale
   - Full name: Mike Rale
   - User logon name: `mrale`
7. Clicked Next → set password meeting complexity requirements
8. Unticked "User must change password at next logon"
9. Ticked "Password never expires" (for lab purposes)
10. Clicked Next → Finish
11. Mike Rale account confirmed inside HR Department OU

### Part C — Verify Login
12. Switched to Client01
13. At login screen → Other user → entered `MAYANKLAB\mrale`
14. Entered password
15. Login successful — Welcome Mike Rale

---

## User Account Details

| Field | Value |
|---|---|
| Full Name | Mike Rale |
| Username | mrale |
| Domain | mayanklab.local |
| OU | HR Department |
| Logon name | mrale@mayanklab.local |

---

## Screenshots

| File | Description |
|---|---|
| Capture_1 | New OU dialog — HR Department name entered |
| Capture_2 | AD structure — HR Department OU created and visible |
| Capture_3 | New user dialog — Mike Rale details filled in |
| Capture_4 | Password configuration — "Password never expires" ticked |
| Capture_5 | Mike Rale account confirmed inside HR Department OU |
| Capture_6 | Client01 login screen — mrale@mayanklab.local entered |
| Capture_7 | Welcome — Mike Rale — login successful |

---

## What I Learned
- New OUs can be created directly from the right click menu in AD Users and Computers
- User accounts must be created inside the correct OU to ensure proper GPO application
- New domain users can log into any domain-joined machine immediately after account creation
