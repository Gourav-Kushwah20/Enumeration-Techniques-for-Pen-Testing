# 🌐 Web-Enumeration

## 🔍 Web Enumeration and Web Server Enumeration

* Web Enumeration and Web Server Enumeration are **fundamental phases of reconnaissance** in penetration testing and vulnerability assessments.
* Together, they help map **application functionality** and identify **server-side technologies, configurations, and weaknesses**.

---

## 🧩 1. Web Enumeration

### 📖 Definition

Web Enumeration is the process of discovering the **structure**, **content**, and **functionality** of a web application.

---

### 🎯 Focus Areas

* Pages, directories, and endpoints
* Hidden or restricted resources
* Authentication mechanisms and user roles
* API endpoints (REST / GraphQL)
* Application-specific features (admin panels, uploads, blogs, user areas)

---

### 🔎 Common Enumeration Activities

* Crawling websites for links and parameters
* Reviewing `robots.txt` and `sitemap.xml`
* Directory and file brute-forcing (`/admin`, `/backup`, `/uploads`)
* Analyzing JavaScript files for hidden endpoints
* Discovering exposed APIs and internal routes

---

## 🖥️ 2. Web Server Enumeration

### 📖 Definition

* Web Server Enumeration focuses on identifying the **server software**, **version**, **modules**, and **configuration** that support a web application.

---

### 🎯 Focus Areas

* Web server type and version (Apache, Nginx, IIS)
* Supported modules and extensions
* HTTP methods and protocols
* Misconfigurations (directory listing, default files)
* Server banners and technology disclosure

---

### 🔎 Common Enumeration Activities

* HTTP header inspection
* Banner grabbing
* Service and version detection
* Vulnerability scanning
* Technology fingerprinting

---

## 📊 3. Key Differences

| Aspect  | Web Enumeration               | Web Server Enumeration                      |
| ------- | ----------------------------- | ------------------------------------------- |
| Scope   | Application-level             | Server-level                                |
| Targets | Pages, endpoints, APIs        | Server software, modules                    |
| Goal    | Discover hidden functionality | Identify technologies and misconfigurations |
| Tools   | Dirb, Gobuster, Burp Suite    | curl, Nmap, WhatWeb, Nikto                  |

---
## 🧭 4. Enumeration Workflow

### Step 1: Web Server Enumeration

* Identify server software and version
* Inspect HTTP headers
* Detect enabled HTTP methods
* Identify server-side technologies

---

### Step 2: Web Enumeration

* Crawl the application
* Discover directories and files
* Identify authentication and authorization flows
* Enumerate APIs and parameters

---

## 🎯 5. Enumeration Goals

* Identify web server software and versions
* Detect frameworks and backend technologies
* Discover hidden files, directories, and endpoints
* Identify misconfigurations and default content
* Find potential attack surfaces for exploitation

---

## 🧰 6. Techniques and Tools

### 6.1 Banner Grabbing

Using `nc`:

```bash
nc target.com 80
HEAD / HTTP/1.0
```

Using `curl`:

```bash
curl -I http://target.com
```

```text
HTTP/1.1 200 OK
Server: Apache/2.4.41 (Ubuntu)
```

---

##  🛰️ 6.2 Nmap Scanning

Basic service/version scan:

```bash
nmap -sV -p 80,443 target.com
```

Aggressive scan with scripts:

```bash
nmap -sC -sV -A target.com
```

---

## 🛡️ 6.3 Nikto – Vulnerability Scanning

```bash
nikto -h http://target.com
```

---

## 🧬 6.4 WhatWeb – Technology Fingerprinting

```bash
whatweb http://target.com
```

Example:

```text
Apache[2.4.41], PHP[7.4.3]
```

---

## 📁 6.5 Directory and File Discovery

### Dirb

```bash
dirb http://target.com
```

---
## 🧰 6.6 Gobuster

```bash
gobuster dir -u http://target.com \
  -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

---

## 🧨 6.7 Feroxbuster

```bash
feroxbuster -u http://target.com -w wordlist.txt
```

---

## 🧠 Browser-Based Fingerprinting

* Wappalyzer
* BuiltWith

**Detects:**

* CMS (WordPress, Joomla, Drupal)
* Frameworks (Laravel, Express)
* Analytics and third-party services

---

## 🔄 6.8 HTTP Method Testing

```bash
curl -X OPTIONS http://target.com -i
```

Example:

```text
Allow: GET, POST, PUT, DELETE
```

---

## 🌐 6.9 Virtual Host Discovery

```bash
vhostscan -t http://target.com
```
---

## 🛡️ 6.10 WAF Detection

```bash
wafw00f http://target.com
```

---

## 🧪 6.11 Fuzzing Parameters and Endpoints

### ffuf

```bash
ffuf -u http://target.com/FUZZ -w common.txt
```

### wfuzz

```bash
wfuzz -c -w wordlist.txt --hc 404 http://target.com/FUZZ
```

---

## 🍪 6.12 Cookies and Session Analysis

```bash
curl -I http://target.com
```

Check for:

* Missing `HttpOnly` or `Secure` flags
* Weak session handling
* Predictable session IDs

---

## 🧾 6.13 HTTP Header Analysis

Key headers:

* `Server`
* `X-Powered-By`
* Security headers (CSP, X-Frame-Options)
* `ETag`

---

## 🧪 Example Enumeration Workflow

1. Grab server headers (`curl -I`)
2. Run Nmap for services and versions
3. Fingerprint technologies using WhatWeb
4. Enumerate directories and files
5. Test HTTP methods
6. Run Nikto for known issues
7. Detect WAFs and virtual hosts
8. Fuzz parameters and endpoints
9. Validate findings manually

---

## 💡 7. Pro Tips

* Save scan results for correlation
* Always validate findings manually
* Review JavaScript files carefully
* Combine automated tools with Burp Suite or OWASP ZAP
* Avoid excessive scanning on production targets

---

## 🧰 8. Supporting Tools and Resources

* **amass** – Subdomain enumeration
* **theHarvester** – OSINT data collection
* **Aquatone** – Web screenshots
* **EyeWitness** – Visual reconnaissance
* **httpx** – Fast web probing
* **nuclei** – Template-based vulnerability scanning

---
## 🌐 Common Web Ports and Admin Interfaces

## 🧩 Web Services

| Service | Ports          | Protocol |
| ------- | -------------- | -------- |
| HTTP    | 80, 8080, 8000 | TCP      |
| HTTPS   | 443, 8443      | TCP      |

---

## 🖥️ Application and Web Servers

| Technology      | Ports      | Description     |
| --------------- | ---------- | --------------- |
| Apache Tomcat   | 8080, 8443 | Java App Server |
| GlassFish       | 4848, 8080 | Admin + Web     |
| JBoss / WildFly | 8080, 9990 | Admin Console   |
| WebLogic        | 7001       | Admin Interface |
| WebSphere       | 9043, 9060 | Admin Console   |
| Jenkins         | 8080       | CI/CD Tool      |

---

## 🧰 Hosting Control Panels

| Panel   | Ports       | Notes           |
| ------- | ----------- | --------------- |
| cPanel  | 2082 / 2083 | Hosting Panel   |
| WHM     | 2086 / 2087 | Server Admin    |
| Plesk   | 8880 / 8443 | Hosting Control |
| Webmail | 2095 / 2096 | Email Access    |

---

