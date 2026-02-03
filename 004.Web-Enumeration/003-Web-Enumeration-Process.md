# 🖥️ Machine – My_Web_Server

![My Web Server](./img/My-web_server.png)

## 📌 Reference

* [https://github.com/InfoSecWarrior/Offensive-Pentesting-Lab/blob/main/Vulnerable-OVA/Readme.md](https://github.com/InfoSecWarrior/Offensive-Pentesting-Lab/blob/main/Vulnerable-OVA/Readme.md)

---

## 🌐 Target Information

* **IP Address:** `192.168.1.15`

---

## 🔎 Enumeration

Now scanning the target using **Nmap** and other tools.

➡️ Related tools & notes:
[HTTP Server Version Detection](002-HTTP-Server-Version-Dectection.md)

---

## 🔍 Full Nmap Scan (All Ports)

**Attacker Machine:** Kali Linux (root)

```bash
nmap -v -sT -sC -A -p- 192.168.1.15 -oA my-webserver
```

---

## 📂 Nmap Output Files

```bash
ls -lh
```

```text
total 20K
-rw-rw-r-- 1 root root  874 Feb  3 14:27 my-webserver.gnmap
-rw-rw-r-- 1 root root 2.6K Feb  3 14:27 my-webserver.nmap
-rw-rw-r-- 1 root root 9.4K Feb  3 14:27 my-webserver.xml
```

---

```bash
cat my-webserver.nmap
```
- Output
```bash        
# Nmap 7.95 scan initiated Tue Feb  3 14:26:50 2026 as: /usr/lib/nmap/nmap -v -sT -sC -A -p- -oA my-webserver 192.168.1.15
Nmap scan report for 192.168.1.15 (192.168.1.15)
Host is up (0.028s latency).
Not shown: 65528 closed tcp ports (conn-refused)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 cd:dc:8f:24:51:73:54:bc:87:62:a2:e6:ed:f1:c1:b4 (RSA)
|   256 a9:39:a9:bf:b2:f7:01:22:65:07:be:15:48:e8:ef:11 (ECDSA)
|_  256 77:f5:a9:ff:a6:44:7c:9c:34:41:f1:ec:73:5e:57:bd (ED25519)
80/tcp   open  http    Apache httpd 2.4.38 ((Debian))
| http-robots.txt: 1 disallowed entry 
|_/wp-admin/
|_http-title: Armour &#8211; Just another WordPress site
|_http-favicon: Unknown favicon MD5: D41D8CD98F00B204E9800998ECF8427E
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-generator: WordPress 5.3.2
|_http-server-header: Apache/2.4.38 (Debian)
2222/tcp open  http    nostromo 1.9.6
|_ssh-hostkey: ERROR: Script execution failed (use -d to debug)
|_http-server-header: nostromo 1.9.6
|_http-title: Radius by TEMPLATED
| http-methods: 
|_  Supported Methods: GET HEAD POST
3306/tcp open  mysql   MySQL (unauthorized)
8009/tcp open  ajp13   Apache Jserv (Protocol v1.3)
|_ajp-methods: Failed to get a valid response for the OPTION request
8080/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
|_http-title: Apache Tomcat/8.0.33
| http-methods: 
|_  Supported Methods: GET HEAD POST
|_http-open-proxy: Proxy might be redirecting requests
|_http-server-header: Apache-Coyote/1.1
|_http-favicon: Apache Tomcat
8081/tcp open  http    nginx 1.14.2
|_http-title: Visualize by TEMPLATED
|_http-server-header: nginx/1.14.2
| http-methods: 
|_  Supported Methods: GET HEAD
MAC Address: 34:6F:24:E5:35:DB (AzureWave Technology)
Device type: general purpose|router
Running: Linux 4.X|5.X, MikroTik RouterOS 7.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5 cpe:/o:mikrotik:routeros:7 cpe:/o:linux:linux_kernel:5.6.3
OS details: Linux 4.15 - 5.19, OpenWrt 21.02 (Linux 5.4), MikroTik RouterOS 7.2 - 7.5 (Linux 5.6.3)
Uptime guess: 21.574 days (since Tue Jan 13 00:41:25 2026)
Network Distance: 1 hop
TCP Sequence Prediction: Difficulty=258 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT      ADDRESS
1   27.99 ms 192.168.1.15 (192.168.1.15)

Read data files from: /usr/share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Feb  3 14:27:26 2026 -- 1 IP address (1 host up) scanned in 35.93 seconds
```

---

## 📄 Nmap Scan Output

```bash
cat my-webserver.nmap
```

### 🔍 Scan Details

```text
# Nmap 7.95 scan initiated Tue Feb  3 14:26:50 2026
# Command used:
# nmap -v -sT -sC -A -p- -oA my-webserver 192.168.1.15
```

---

## 🎯 Target Host

* **IP Address:** `192.168.1.15`
* **Host Status:** Up
* **Latency:** 0.028s
* **Network Distance:** 1 hop
* **MAC Address:** `34:6F:24:E5:35:DB` (AzureWave Technology)

---

## 🔓 Open Ports & Services

```text
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2
80/tcp   open  http    Apache httpd 2.4.38 (Debian)
2222/tcp open  http    nostromo 1.9.6
3306/tcp open  mysql   MySQL (unauthorized)
8009/tcp open  ajp13   Apache Jserv Protocol v1.3
8080/tcp open  http    Apache Tomcat 8.0.33
8081/tcp open  http    nginx 1.14.2
```

---

## 🔐 SSH Information (Port 22)

* **Service:** OpenSSH 7.9p1
* **Protocol:** SSH-2
* **Host Keys Detected:**

  * RSA 2048
  * ECDSA 256
  * ED25519 256

---

## 🌐 HTTP Enumeration

### Port 80 – Apache / WordPress

* **Server:** Apache 2.4.38 (Debian)
* **CMS:** WordPress 5.3.2
* **Robots.txt:** `/wp-admin/`
* **Title:** *Armour – Just another WordPress site*
* **Allowed Methods:** `GET, HEAD, POST, OPTIONS`

---

### Port 2222 – Nostromo Web Server

* **Server:** nostromo 1.9.6
* **Title:** *Radius by TEMPLATED*
* **Allowed Methods:** `GET, HEAD, POST`

---

### Port 8080 – Apache Tomcat

* **Version:** 8.0.33
* **Title:** *Apache Tomcat/8.0.33*
* **Allowed Methods:** `GET, HEAD, POST`
* **Note:** Possible open proxy behavior

---

### Port 8081 – Nginx

* **Version:** nginx 1.14.2
* **Title:** *Visualize by TEMPLATED*
* **Allowed Methods:** `GET, HEAD`

---

## 🗄️ Database Service

### Port 3306 – MySQL

* **State:** Open
* **Authentication:** Unauthorized (credentials required)

---

## ⚙️ Additional Services

### Port 8009 – AJP

* **Service:** Apache JServ Protocol v1.3
* **Status:** No valid response to OPTIONS request

---

## 🖥️ OS Detection

* **Operating System:** Linux
* **Kernel Range:** 4.15 – 5.19
* **Possible Matches:**

  * Debian / Linux 4.x–5.x
  * OpenWrt 21.02
  * MikroTik RouterOS 7.x
* **Uptime:** ~21 days

---

## 🧭 Traceroute

```text
HOP RTT      ADDRESS
1   27.99 ms 192.168.1.15
```

---

## ✅ Scan Summary

* **Total Ports Scanned:** 65,535
* **Open Ports:** 7
* **Scan Time:** 35.93 seconds
* **Host Status:** 1 host up

---

## 🧠 What to Do After Scanning?

After completing the Nmap scan, the next step is **service enumeration and prioritization**.
Since the scan reveals **7 open ports**, it is neither efficient nor practical to attack all ports randomly. A **structured approach** is required.

---

## ⏱️ Time Management Strategy

* **Baseline Enumeration Time:**
  Allocate **~15 minutes per open port** for initial enumeration.

* **Total Initial Time:**

  ```
  7 ports × 15 minutes = ~1.75 hours
  ```

* **If a Vulnerability Is Found:**

  * Extend enumeration by another **15–30 minutes**
  * Move toward **proof-of-concept exploitation**

* **Maximum Time Per Port:**

  * **30 minutes normally**
  * **Up to 1 hour** if strong attack vectors are identified

This prevents tunnel vision and keeps the assessment efficient.

---

## 🎯 Port Prioritization Logic

Not all ports are equally valuable. **Port priority depends on the service running**, its **attack surface**, and your **experience with that service**.

### General Priority Order

1. **Web Services (HTTP / HTTPS)**
2. **File Sharing Services**
3. **Databases**
4. **Remote Access Services**
5. **Other / Rare Services**

---

## 🚦 Port Prioritization for This Machine

Based on the Nmap scan, the open ports are:

| Priority | Port | Service               | Reason                                          |
| -------- | ---- | --------------------- | ----------------------------------------------- |
| 1️⃣      | 80   | HTTP (WordPress)      | Large attack surface, known CMS vulnerabilities |
| 2️⃣      | 2222 | HTTP (Nostromo 1.9.6) | Known RCE vulnerabilities                       |
| 3️⃣      | 8080 | Apache Tomcat         | Admin panels, weak creds, RCE                   |
| 4️⃣      | 8081 | Nginx Web Server      | Misconfig, file disclosure                      |
| 5️⃣      | 8009 | AJP                   | Ghostcat-style issues                           |
| 6️⃣      | 3306 | MySQL                 | Needs creds, usually post-foothold              |
| 7️⃣      | 22   | SSH                   | Brute-force only if creds found                 |

---

## 🧪 Why Web Services First?

* Web services:

  * Are **directly accessible**
  * Have **huge attack surfaces**
  * Often lead to **initial foothold**
* CMS platforms like **WordPress** and **Tomcat** frequently expose:

  * RCE
  * File upload flaws
  * Weak credentials
  * Outdated plugins

---

## 🧭 Decision-Making Principle

> **“Prioritize the service you are most familiar with.”**

If you are strong in:

* Web exploitation → Start with **HTTP**
* Databases → Check **MySQL**
* Credentials → Focus on **SSH**

Experience + service exposure = fastest entry.

---

## 🧩 Enumeration Flow (Recommended)

1. Enumerate **HTTP services**
2. Look for **known vulnerabilities**
3. Gain **initial access**
4. Use credentials/configs to attack:

   * SSH
   * MySQL
5. Escalate privileges

---

## ✅ Key Takeaways

* Scanning only tells **what is open**
* Enumeration decides **where to attack**
* Time-boxing prevents wasted effort
* Prioritization depends on:

  * Service type
  * Known vulnerabilities
  * Personal skillset

---

## 🧪 Practical: Vulnerability Research Using Browser

### 🎯 Objective

* Identify known vulnerabilities for discovered services
* Verify **affected vs fixed versions**
* Locate **public exploit references** for further analysis

---

## 🌐 Practical 1: Apache HTTP Server 2.4.38 (Debian)

### 🔍 Browser-Based Vulnerability Search

Open a browser and search using the following queries:

```url
apache 2.4.38 debian vulnerabilities
```

```url
apache 2.4.38 debian exploit
```

```url
site:exploit-db.com apache 2.4.38
```

---

### 📌 What to Look For

While reviewing search results, focus on:

* CVE IDs affecting **Apache < 2.4.39**
* Vulnerability type (RCE, LPE, DoS)
* Exploit requirements (local access, module dependency)
* Debian-specific security notes (backported patches)

---

### 🛠️ Fixed Version Verification

Check the official Apache security documentation:

* Apache HTTP Server Security Advisories
* Debian Security Tracker

Key example:

| CVE ID        | Vulnerability              | Affected Version | Fixed Version |
| ------------- | -------------------------- | ---------------- | ------------- |
| CVE-2019-0211 | Local Privilege Escalation | < 2.4.39         | 2.4.39        |

📌 **Note:**
Debian may apply security patches without changing the version number. Always verify via Debian Security Tracker.

---

## 🌐 Practical 2: Nostromo Web Server 1.9.6 (Port 2222)

```
2222/tcp open  http    nostromo 1.9.6
```

This service is **high priority** due to known **Remote Code Execution (RCE)** vulnerability.

---

## 🔥 Vulnerability Overview

* **Service:** Nostromo HTTP Server
* **Version:** 1.9.6
* **CVE:** CVE-2019-16278
* **Impact:** Remote Code Execution (Unauthenticated)
* **Severity:** Critical

---

## 🔎 Two Reliable Methods to Find Exploit Information

### ✅ Method 1: Technical Walkthrough (Blog)

Provides:

* Vulnerability explanation
* Attack logic
* Python exploit walkthrough

🔗 Reference:
[https://medium.com/@vkeshri657/remote-code-execution-on-nostromo-web-server-using-python-exploit-66ec45d265e5](https://medium.com/@vkeshri657/remote-code-execution-on-nostromo-web-server-using-python-exploit-66ec45d265e5)

---

### ✅ Method 2: Public Exploit Code (GitHub)

Provides:

* Ready-to-analyze exploit code
* CVE reference
* Exploit usage details

🔗 Reference:
[https://github.com/cancela24/CVE-2019-16278-Nostromo-1.9.6-RCE](https://github.com/cancela24/CVE-2019-16278-Nostromo-1.9.6-RCE)

---

## 🧠 Why This Port Is Prioritized

* Public **unauthenticated RCE**
* No credentials required
* Direct path to **initial foothold**
* High success rate in lab environments

---

## ✅ Practical Summary

* Apache 2.4.38 research helps identify **post-exploitation paths**
* Nostromo 1.9.6 offers a **direct RCE attack vector**
* Browser-based research confirms:

  * Vulnerability existence
  * Affected versions
  * Available exploit references

---

another way to exploit [exploit](004-Nostromo-1.9.6-exploit.md)