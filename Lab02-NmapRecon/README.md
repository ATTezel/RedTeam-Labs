# Lab02 – Basic Network Scanning with Nmap

## 🧠 Objective
Perform active reconnaissance on a local target (Metasploitable2) using Nmap to identify open ports and running services.

---

## 🛠️ Tools
- Nmap

---

## 💻 Commands Used
```bash
nmap -sS -sV -T4 -p- 192.168.56.101 -oN fullscan.txt
```

---

## Findings
Open Ports:

21 (FTP), 22 (SSH), 23 (Telnet), 25 (SMTP), 53 (DNS), 80 (HTTP), 139/445 (SMB), 3306 (MySQL)

Detected Vulnerable Services:

vsftpd 2.3.4

Samba smbd

ISC BIND 9.4.2

---

## What I Learned
Mastered full-port scanning and service version detection

Learned how to detect potentially exploitable services

Recognized the importance of recon before exploitation

---

## Screenshot


📅 Date
23 May 2025
