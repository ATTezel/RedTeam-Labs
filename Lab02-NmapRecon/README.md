# 🔎 Lab02 – Basic Network Scanning with Nmap

> **Date:** 23 May 2025  
> **Target:** Metasploitable2  
> **Tool Used:** Nmap  
> **Focus:** Full port scan + version detection for recon

---

## 🛡️ Description

This lab demonstrates the first and most critical step in any red team engagement: **network reconnaissance**. Using `nmap`, I performed a full TCP port scan against a local Metasploitable2 VM to identify open ports and vulnerable services.

---

## 🎯 Target System

- Metasploitable2 (local virtual machine)  
- Internal IP: `192.168.56.101`  
- Common intentionally vulnerable services exposed

---

## 🧨 Exploitation Prep – Commands Used

```bash
nmap -sS -sV -T4 -p- 192.168.56.101 -oN fullscan.txt
```
| Flag  | Purpose                               |
| ----- | ------------------------------------- |
| `-sS` | TCP SYN scan (stealthy and fast)      |
| `-sV` | Detect service versions               |
| `-T4` | Speed up the scan                     |
| `-p-` | Scan all 65535 TCP ports              |
| `-oN` | Output scan results to `fullscan.txt` |


## 📊 Findings
Open Ports:

```
21 (FTP), 22 (SSH), 23 (Telnet), 25 (SMTP), 53 (DNS),  
80 (HTTP), 139/445 (SMB), 3306 (MySQL)
```
Detected Vulnerable Services:

- vsftpd 2.3.4 → Known backdoor (CVE-2011-2523)

- Samba smbd → Privilege escalation and RCE vectors

- ISC BIND 9.4.2 → DNS-related exploits possible

## 📊 Real-World Relevance
Reconnaissance is where most real attacks begin. Mapping exposed services lets an attacker prioritize targets and plan attacks. Poorly secured services like outdated FTP, SMB, or Telnet are frequently the entry point in corporate breach reports.

## 🧠 What I Learned
How to perform comprehensive scans across all TCP ports

How to identify vulnerable services via version fingerprinting

Why thorough recon prevents guesswork during exploitation

That even a simple scan can expose major security gaps

## Screenshot

Below is a screenshot showing the open ports and running services discovered using nmap on the Metasploitable2 target:

![Nmap Scan Result](https://github.com/ATTezel/RedTeam-Labs/blob/main/lab2/Screen%20Shot%202025-05-23%20at%2020.27.08.png)
)

Additionally, the following screenshot captures the active service bindings and port status for deeper enumeration:

![Listening Ports](https://github.com/ATTezel/RedTeam-Labs/blob/main/lab2/Screen%20Shot%202025-05-23%20at%2020.27.38.png))

![](https://github.com/ATTezel/RedTeam-Labs/blob/main/lab2/Screen%20Shot%202025-05-23%20at%2020.20.14.png)


![](https://github.com/ATTezel/RedTeam-Labs/blob/main/lab2/Screen%20Shot%202025-05-23%20at%2020.25.37.png)


## 📁 Notes
- This scan will serve as the base for upcoming exploits, including FTP, Samba, and MySQL attacks.

- Report was saved to fullscan.txt and manually analyzed for priority targets.
