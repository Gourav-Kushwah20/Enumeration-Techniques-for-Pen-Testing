# Findomain – Fast Subdomain Enumeration Tool

**[Findomain](https://github.com/Findomain/Findomain)** is a blazing-fast subdomain enumeration tool written in **Rust**.  
It supports both **passive** and **active** subdomain discovery, making it an excellent choice for modern reconnaissance workflows.

---

## 🛠 Installation

Download the latest Linux binary from GitHub:

```bash
wget https://github.com/Findomain/Findomain/releases/download/10.0.1/findomain-linux.zip
````

Move it to your system’s executable path:

```bash
unzip Findomain-master.zip  
```

```bash
mv -v Findomain-master /usr/local/bin/findomain
```

Make it executable:

```bash
chmod +x /usr/local/bin/findomain
```

Verify installation:

```bash
findomain
```

---

## ⚙️ Basic Usage

### 1️⃣ Passive Subdomain Enumeration

```bash
findomain -t instagram.com
```

📌 This performs **passive enumeration** using built-in **OSINT sources**.

---

## 🔥 Active Enumeration with Wordlist and Threading

```bash
findomain --output -t tesla.com -w /usr/share/seclists/Discovery/DNS/dns-Jhaddix.txt --threads 50 -r
```

```bash
findomain --output -t tesla.com -w /usr/share/dnsenum/dns.txt --threads 50 -r
```

### Option Explanation

* `-t` → Target domain
* `-w` → Wordlist for brute force
* `--threads` → Number of concurrent threads
* `-r` → Enable brute-force resolution
* `--output` → Saves output to a file (default: `<domain>.txt`)

---

## ⚙️ Using a Configuration File

### Download the default configuration file

```bash
wget https://raw.githubusercontent.com/Findomain/Findomain/master/config_examples/config.example.yml
```

### Move and rename it for custom use

```bash
mv config.example.yml /opt/findomain_config.yml
```

### Use it in a scan

```bash
findomain --config /opt/findomain_config.yml --output -t tesla.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --threads 50 -r
```

---

## 📤 Output

* By default, output is saved in the **current directory** as:

  ```
  tesla.com.txt
  ```

  or the file specified using `--output-file`.

* When using `--config`, you can control:

  * DNS resolving behavior
  * API integrations
  * Output formats (e.g., **JSON**, **CSV**)

---

