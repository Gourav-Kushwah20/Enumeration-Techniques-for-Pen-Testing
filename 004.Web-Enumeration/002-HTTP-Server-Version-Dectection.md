# 🌐 HTTP-Server-Version-Detection

## 🔍 HTTP Server Version Detection

This document describes multiple techniques to identify **HTTP server software and versions** using **Netcat**, **Telnet**, and **Nmap**.
These techniques are commonly used during the **reconnaissance and enumeration phase** of a security assessment or penetration test.

> **Note:** Server version details may be hidden, altered, or proxied. Always validate results using multiple methods.

Reference:
[https://github.com/InfoSecWarrior/Offensive-Pentesting-Lab/blob/main/Vulnerable-OVA/Readme.md](https://github.com/InfoSecWarrior/Offensive-Pentesting-Lab/blob/main/Vulnerable-OVA/Readme.md)

---

## 🧪 1. Netcat (nc) – HTTP Server Version Detection

Netcat is a lightweight networking utility that allows manual interaction with TCP/UDP services.
Sending a raw HTTP request can reveal server banner information via response headers.

---

## 🔌 Connect to an HTTP Server on Port 80

```bash
nc 192.168.1.15 80
```

Send a valid HTTP request:

```http
GET / HTTP/1.1
Host: 192.168.1.15
Connection: close
```

Press **Enter twice** to submit the request.

---

## 👀 Observe the Following Headers

* `Server` (e.g., Apache, nginx, IIS)
* `X-Powered-By` (framework or backend hints)
* HTTP response status and additional headers

---

## 🧾 Connect with Verbose Output

```bash
nc -v 192.168.1.15 80
```

---
## 🔌 Connect to an HTTP Service on a Non-Standard Port

```bash
nc -v 192.168.1.15 2222
```

Useful when web services are running on ports other than **80** or **443**.

---

## 🧪 2. Telnet – HTTP Server Version Detection

Telnet can also be used for manual banner grabbing and behaves similarly to Netcat.

---

## 🔗 Connect to an HTTP Server Using Telnet

```bash
telnet 192.168.1.15 80
```

Send the request:

```http
GET / HTTP/1.1
Host: 192.168.1.15
Connection: close
```

Press **Enter twice** to receive the response.

---

## 👀 Key Headers to Inspect

* `Server`
* `X-Powered-By`
* `Set-Cookie`
* `Via` / proxy headers

---

## 🛰️ 3. Nmap – HTTP Server Version Detection

Nmap automates **service discovery**, **version detection**, **OS fingerprinting**, and **script-based enumeration**.

## 🔍 Scan All TCP Ports

```bash
nmap -v -p- 192.168.1.211
```

* Scans all **65,535 TCP ports**
* Detects services running on **uncommon ports**


## 🧪 Service and OS Detection on Specific Ports

```bash
nmap -v -sT -sV -A -O -p 22,80,2222,3306,8009,8080,8081 192.168.1.211
```

Helps identify:

* Web servers (Apache, nginx, IIS)
* Application servers (Tomcat, Jenkins)
* Databases and SSH services


## 🌐 HTTP-Focused Scan on Port 80

```bash
nmap -v -sT -sV -A -O -p 80 192.168.1.211
```

Optimized for quick HTTP enumeration.



## 🧭 Full TCP Scan on Another Host

```bash
nmap -v -sT -p- 172.16.0.129
```

Standard TCP connect scan across all ports.

---

```bash
nmap -v -sT -sC -A -p- 192.168.1.15 -oA my-webserver
```

* Scans **all TCP ports**
* Uses **TCP connect scan**
* Runs **default NSE scripts**
* Enables **OS, version, and script detection**
* Verbose output
* Saves results in **all formats**
---


## 🌐 HTTP-Only Detailed Scan on Another Target

```bash
nmap -v -sT -sV -A -O -p 80 172.16.0.129
```

* Focused analysis of a **single HTTP service**

---

## 🧪 Full Service and Version Scan on All Ports

```bash
nmap -v -sT -sV -A -p- 192.168.1.211
```

Includes:

* Service version detection
* OS fingerprinting
* NSE scripts
* Traceroute

---

## 📦 Full Scan with No Ping and Saved Output

```bash
nmap -v -Pn -sT -sV -sC -A -O \
-p 22,80,2222,3306,8009,8080,8081 \
-oA output 192.168.56.108
```

---

## ✅ Advantages

* Works when **ICMP is blocked**
* Saves output in **.nmap**, **.xml**, and **.gnmap** formats
* Executes **default NSE scripts**

---

## 📘 Nmap Options Reference

| Option | Description                                        |
| ------ | -------------------------------------------------- |
| `-v`   | Verbose output                                     |
| `-p-`  | Scan all 65,535 TCP ports                          |
| `-sT`  | TCP Connect scan                                   |
| `-sV`  | Service version detection                          |
| `-A`   | Aggressive scan (OS, version, scripts, traceroute) |
| `-O`   | OS detection                                       |
| `-Pn`  | Skip host discovery (no ping)                      |
| `-sC`  | Run default NSE scripts                            |
| `-oA`  | Output in all formats (`.nmap`, `.xml`, `.gnmap`)  |

---

## ⚠️ Practical Notes & Limitations

* HTTP/2 and HTTPS may **not reveal banners** via Netcat or Telnet
* Reverse proxies, **WAFs**, and load balancers can **mask backend servers**
* Some servers **spoof or remove** the `Server` header
* Always validate findings using:

  * Multiple tools
  * Different request methods
  * Application-level fingerprinting

---

## 💡 Tip

* **Netcat & Telnet** → raw, low-level visibility
* **Nmap** → scalable automation
* ✅ **Best results come from combining both approaches**

---
