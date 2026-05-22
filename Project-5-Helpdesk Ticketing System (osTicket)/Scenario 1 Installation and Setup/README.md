# Scenario 1 — Installation and Setup

## What This Covers
Full installation and configuration of XAMPP and osTicket on DC01 (Windows Server 2022), including database setup, file transfer via VirtualBox shared folder, and post-installation configuration.

---

## Tools Used
- Oracle VirtualBox — Shared Folder configuration
- XAMPP v8.0.30 — Apache, MySQL, PHP, phpMyAdmin
- osTicket v1.16.6
- Microsoft Edge (DC01)
- Command Prompt (DC01)

---

## Steps Performed

### Part A — File Transfer via VirtualBox Shared Folder
1. Downloaded XAMPP installer and osTicket zip on Windows 11 host machine
2. Created `C:\LabFiles` folder on host
3. Opened VirtualBox → DC01 Settings → Shared Folders
4. Added shared folder:
   - Path: `C:\LabFiles`
   - Name: `LabFiles`
   - Auto-mount: Yes
   - Mount point: `Z:\`
5. Installed VirtualBox Guest Additions on DC01 to enable shared folder access
6. Accessed shared folder on DC01 via Network → VBOXSVR → LabFiles (Z: drive)
7. Confirmed XAMPP installer and osTicket folder visible on DC01

### Part B — XAMPP Installation
8. Ran `xampp-windows-x64-8.0.30-0-VS16-installer` from Z: drive
9. Accepted UAC warning — installed to `C:\xampp`
10. Components installed: Apache, MySQL, PHP, phpMyAdmin
11. Opened XAMPP Control Panel
12. Started **Apache** — running on ports 80 and 443
13. Started **MySQL** — running on port 3306
14. Both services confirmed green and running

### Part C — Database Setup
15. Opened phpMyAdmin at `http://localhost/phpmyadmin`
16. Clicked Databases tab
17. Created new database: `osticket`
18. Set MySQL root password via Command Prompt:
```
cd C:\xampp\mysql\bin
mysql -u root
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Welcome@2026!';
FLUSH PRIVILEGES;
exit
```

### Part D — osTicket Installation
19. Copied osTicket upload folder from Z: drive to `C:\xampp\htdocs\`
20. Renamed folder from `upload` to `osticket`
21. Renamed `ost-sampleconfig.php` to `ost-config.php` via Command Prompt:
```
copy C:\xampp\htdocs\osticket\include\ost-sampleconfig.php C:\xampp\htdocs\osticket\include\ost-config.php
```
22. Opened osTicket installer at `http://localhost/osticket/setup`
23. Prerequisites check completed:
    - ✅ PHP v8.0.30
    - ✅ MySQLi extension loaded
24. Increased PHP max_execution_time from 120 to 300 seconds in php.ini
25. Restarted Apache after php.ini changes
26. Completed Basic Installation form:

| Field | Value |
|---|---|
| Helpdesk Name | Mayank Lab Helpdesk |
| Default Email | admin@mayanklab.local |
| Admin First Name | Mayank |
| Admin Last Name | Rale |
| Admin Username | mayank.admin |
| MySQL Database | osticket |
| MySQL Username | root |
| MySQL Password | Welcome@2026! |

27. Clicked Install Now — installation completed successfully
28. Deleted setup directory for security:
```
rmdir /s /q C:\xampp\htdocs\osticket\setup
```

### Part E — Post-Installation Configuration
29. Logged into Admin Control Panel at `http://localhost/osticket/scp`
30. Verified Helpdesk Name: Mayank Lab Helpdesk
31. Added Windows Firewall rule to allow HTTP from Client01:
```
netsh advfirewall firewall add rule name="Allow HTTP" protocol=TCP dir=in localport=80 action=allow
```
32. Verified osTicket portal accessible from Client01 at `http://192.168.1.10/osticket`
33. Created helpdesk agent — John Smith:
    - Username: jsmith
    - Email: jsmith@mayanklab.local
    - Department: Support
34. Confirmed John Smith appearing in agents list

---

## Troubleshooting Notes

| Issue | Cause | Fix |
|---|---|---|
| PHP 500 error on install | max_execution_time too low | Increased to 300s in php.ini |
| Shared folder not visible | Guest Additions not installed | Installed VBoxWindowsAdditions.exe |
| Client01 can't reach osTicket | Windows Firewall blocking port 80 | Added inbound HTTP firewall rule |
| MySQL password required | Root had no password set | Set password via mysql command line |

---

## Screenshots

| File | Description |
|---|---|
| Capture_1 | XAMPP installer running on DC01 |
| Capture_2 | XAMPP Control Panel — Apache and MySQL running green |
| Capture_3 | phpMyAdmin open at localhost |
| Capture_4 | osticket database created in phpMyAdmin |
| Capture_5 | osTicket installer — prerequisites check passed |
| Capture_6 | osTicket Basic Installation form filled in |
| Capture_7 | osTicket installation completing |
| Capture_8 | osTicket Admin Control Panel — logged in as Mayank |
| Capture_9 | System Settings — Mayank Lab Helpdesk configured |
| Capture_10 | Agents list — Mayank Rale as admin agent |
| Capture_11 | Add New Agent form — John Smith details filled in |
| Capture_12 | Agent Access tab — Support department assigned |
| Capture_13 | Agents list — John Smith added successfully |
| Capture_14 | Windows Firewall rule added for port 80 |
| Capture_15 | osTicket portal accessible from Client01 |

---

## What I Learned
- How to deploy a full LAMP-style web stack on Windows Server using XAMPP
- How VirtualBox shared folders and Guest Additions enable file transfer between host and VM
- How PHP configuration settings directly affect web application behaviour
- How Windows Firewall rules control inbound web traffic
- How osTicket installation mirrors real-world web application deployment processes
