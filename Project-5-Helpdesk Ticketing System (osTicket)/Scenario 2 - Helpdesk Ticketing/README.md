# Scenario 2 - Helpdesk Ticketing

## What This Covers
Simulation of a complete helpdesk ticket lifecycle using osTicket. A user raises a ticket from Client01 reporting a network drive issue. The helpdesk agent receives, assigns, resolves, and closes the ticket from DC01.

---

## Tools Used
- osTicket Support Center (Client01 — end user portal)
- osTicket Agent Panel (DC01 — helpdesk agent panel)
- Microsoft Edge (both VMs)

---

## Ticket Details

| Field | Value |
|---|---|
| Submitted by | John Smith (jsmith@mayanklab.local) |
| Help Topic | General Enquiry |
| Issue | Cannot access shared network drive |
| Priority | Normal |
| Assigned To | John Smith (agent) |
| Resolved by | Mayank Rale (admin) |

---

## Steps Performed

### Part A — Raise a Ticket (Client01)
1. Logged into Client01 as `MAYANKLAB\jsmith`
2. Opened Microsoft Edge and navigated to:
```
http://192.168.1.10/osticket
```
3. Mayank Lab Helpdesk Support Center loaded successfully
4. Clicked **Open a New Ticket**
5. Filled in ticket form:
   - Email: `jsmith@mayanklab.local`
   - Full Name: John Smith
   - Help Topic: General Enquiry
   - Issue Summary: Cannot access shared network drive
   - Details: Unable to access the shared network drive this morning. Getting access denied error when trying to connect. Please investigate and resolve.
6. Clicked **Create Ticket**
7. Ticket confirmation received with unique ticket number

### Part B — View and Assign Ticket (DC01)
8. Logged into osTicket Agent Panel on DC01 at:
```
http://localhost/osticket/scp
```
9. Credentials: `mayank.admin` / `Welcome@2026!`
10. Clicked **Tickets** in the top menu
11. Ticket from John Smith visible in Open queue
12. Clicked ticket to open and review details
13. Assigned ticket to **John Smith** agent via Assign dropdown

### Part C — Resolve the Ticket (DC01)
14. Scrolled down to **Post Reply** section
15. Typed resolution:
```
Hi John, I have investigated the issue with your shared network drive access.
The problem was caused by incorrect drive mapping settings. I have remapped
the drive and verified access is now working correctly. Please try accessing
the drive again and let me know if you experience any further issues.
```
16. Changed ticket status from **Open** to **Resolved**
17. Clicked **Post Reply**
18. Ticket marked as Resolved with timestamp

### Part D — Close the Ticket
19. Ticket automatically moved to Closed queue
20. Clicked **Tickets → Closed** to verify
21. Confirmed ticket visible in Closed queue
22. Verified full ticket history showing:
    - Original submission from John Smith
    - Assignment to agent
    - Resolution reply from Mayank Rale
    - Timestamps for all actions

---

## Ticket Lifecycle Summary

```
User submits ticket (Client01)
        ↓
Ticket appears in Open queue (DC01 Agent Panel)
        ↓
Agent reviews and assigns ticket
        ↓
Agent posts resolution reply
        ↓
Ticket status changed to Resolved
        ↓
Ticket moves to Closed queue
        ↓
Full ticket history retained
```

---

## Screenshots

| File | Description |
|---|---|
| Capture_1 | Mayank Lab Helpdesk portal on Client01 |
| Capture_2 | Open a New Ticket form filled in |
| Capture_3 | Ticket confirmation — ticket number issued |
| Capture_4 | Agent Panel — ticket appearing in Open queue |
| Capture_5 | Ticket details open — assigned to John Smith |
| Capture_6 | Resolution reply posted — status set to Resolved |
| Capture_7 | Ticket in Closed queue — full lifecycle complete |

---

## What I Learned
- How the end user portal and agent panel work together in a helpdesk ticketing system
- How tickets flow through the lifecycle: Open → Assigned → Resolved → Closed
- How osTicket mirrors enterprise systems like ServiceNow — same concepts, different interface
- How resolution notes and ticket history provide an audit trail for IT support actions
- How to access a web application hosted on the server VM from a client VM across an internal network
