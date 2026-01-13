# 🌐 Virtual Host Enumeration

**Virtual Host Enumeration** is the process of discovering **hidden or undocumented virtual hosts** configured on a web server.  
A single server IP can host multiple websites (virtual hosts), and the correct site is served based on the **`Host` header** in the HTTP request.

By manipulating or fuzzing the **Host header**, attackers and security testers can identify **additional websites or applications** running on the same server.

---

## 🧠 How Virtual Hosting Works

- 🌍 Web servers (**Apache, Nginx, IIS**) use the **Host header** to determine which website to serve.
- ❓ If an unknown or incorrect host is supplied, the server may:
  - 🧾 Serve a default website
  - ❌ Return an error
  - 🚨 Accidentally expose another virtual host

### 📌 Example Request

```http
GET / HTTP/1.1
Host: admin.target.com
```

---

## ❓ Why Virtual Host Enumeration Is Important

* 🔐 Finds **hidden admin panels**
* 🧪 Discovers **internal or staging environments**
* ⚠️ Reveals **misconfigured applications**
* 🗺️ Expands the **attack surface** during reconnaissance

---

## 🛠️ Common Techniques

### 1️⃣ Host Header Fuzzing

- 📤 Sending multiple requests with different **Host** values to detect valid virtual hosts.

---

## 2️⃣ Response Analysis

### 🔍 Comparing:
- 📡 Status codes  
- 📏 Response length  
- 📄 Page content  
- 🧾 Headers  

---

## 3️⃣ Certificate Inspection

- 🔐 Extracting domain names from **SSL certificates**

---

## 🧰 Tools Used

- ⚡ `ffuf`  
- 🧱 `gobuster`  
- 🐺 `wfuzz`  
- 🧨 `feroxbuster`  
- 🛰️ `nmap` *(http-vhosts script)*  
- 🕷️ `nikto`  
- 🧠 `WhatWeb`  

---

## ⚔️ ffuf (Example)

```bash
ffuf -w vhosts.txt -u http://TARGET_IP/ -H "Host: FUZZ.target.com"
```

---

## 🧪 Virtual Host Enumeration Tools

A curated list of commonly used tools for **Virtual Host (VHost) enumeration** during web security testing and reconnaissance.

## ⚡ ffuf

- Fast and flexible fuzzer, widely used for **VHost discovery**

```bash
ffuf -w vhosts.txt -u http://TARGET_IP/ -H "Host: FUZZ.target.com"
````

```bash
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://192.168.1.51/ -H "Host: FUZZ.armour.local"
```

```bash
ffuf -fs 703 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://192.168.1.51/ -H "Host: FUZZ.armour.local"
```

---

## 🧱 gobuster

* Supports **VHost enumeration** with good performance

```bash
gobuster vhost -u http://TARGET_IP -w vhosts.txt
```

---

## 🐺 wfuzz

* Highly customizable fuzzing tool

```bash
wfuzz -c -w vhosts.txt -H "Host: FUZZ.target.com" http://TARGET_IP/
```

---

## 🧨 feroxbuster

* Primarily used for content discovery, but also supports **VHost fuzzing**

```bash
feroxbuster -u http://TARGET_IP -H "Host: FUZZ.target.com"
```

---

## 🕷️ nikto

* Can sometimes identify **alternate virtual hosts**

```bash
nikto -h http://TARGET_IP
```
---

## 🛰️ nmap (http-vhosts NSE script)

- Uses **NSE scripts** for virtual host detection

```bash
nmap --script http-vhosts -p 80,443 TARGET_IP
```

---

## 🧠 WhatWeb

* Detects **web technologies** and may reveal **virtual host information**

```bash
whatweb http://TARGET_IP
```

---

## 📚 Useful Wordlists

### 🔹 SecLists

* `Discovery/DNS/subdomains-top1million-5000.txt`
* `Discovery/Web-Content/vhosts.txt`

### 🔹 Custom wordlists generated from:

* 🌐 DNS enumeration
* 🔐 SSL certificate transparency logs
* 🕰️ Wayback Machine results

---

## 💡 Tips

* 🔍 Compare **response size**, **status codes**, and **headers**
* 🎯 Use filters such as:

  * `--filter-size`
  * `--filter-status`

- 🧪 Test both header formats:
  - `Host: FUZZ.target.com`
  - `Host: FUZZ`

---

## ✅ When Virtual Host Enumeration Works Best

- 🌐 Target accessed via **IP address**
- 🏢 **Shared hosting** environments
- ☁️ **Cloud infrastructure**
- 🧪 **CTF and lab** environments

---

## 🔑 Key Takeaway

**Virtual Host Enumeration** helps uncover **hidden applications** by abusing how web servers route traffic based on the **Host header**.  
It is a **critical step** in web reconnaissance and penetration testing.
