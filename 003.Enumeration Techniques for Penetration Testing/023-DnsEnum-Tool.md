# 🔎 dnsenum – DNS Enumeration Tool

**dnsenum** is a Perl-based DNS enumeration tool designed to automate the process of gathering various DNS records, including **subdomains, mail servers, name servers, and zone transfer testing**.  
It is commonly used by **penetration testers** and **red teamers** during the reconnaissance phase.

---

## ⚙️ Installation

If `dnsenum` is not installed on your system:

```bash
apt install dnsenum
```

> This installs `dnsenum` from the system’s package repository.

---

## 🚀 Basic Usage

Use the following commands to get started with **dnsenum**.

---

## 📖 Display Help Menu

```bash
dnsenum --help
```

This command lists all available options and usage syntax for `dnsenum`.

---

## 🔍 Verbose Scan on a Domain

```bash
dnsenum -v instagram.com
```

Performs a **verbose DNS enumeration** on `tesla.com`, displaying detailed progress and results.

---

## 🧪 Verbose Scan on a Known Vulnerable Domain

```bash
dnsenum -v zonetransfer.me
```

Tests the enumeration process on `zonetransfer.me`, which is commonly used for **training and demonstration purposes**.


---

## ⚡ Quick Scan

```bash
dnsenum zonetransfer.me
```

Performs a **standard scan** without verbose output.

---

## 📚 Default Wordlist

The default DNS wordlist used by **dnsenum** is typically located at:

```bash
cat /usr/share/dnsenum/dns.txt | wc -l
```

This shows how many entries exist in the default wordlist.

### 🔍 View the Wordlist Content

```bash
cat /usr/share/dnsenum/dns.txt
```

---

## 🌐 Using a Custom DNS Server

To perform enumeration using a **specific DNS resolver**:

```bash
dnsenum instagram.com --dnsserver edns69.ultradns.com
```

This queries `edns69.ultradns.com` instead of the system’s default DNS server.

---

## 🚀 Advanced Usage Examples

### 🧵 Using a Custom Wordlist with Multi-threading and Output Saving

```bash
dnsenum --threads 50 -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -r -o tesla_domain tesla.com --dnsserver edns69.ultradns.com
```

#### 🔧 Option Breakdown

* `--threads` → Sets concurrency for faster brute-forcing
* `-f` → Specifies a custom wordlist
* `-r` → Enables recursive enumeration
* `-o` → Saves output to a file
* `--dnsserver` → Uses a custom DNS resolver

---

## 📈 Using a Larger Wordlist for Extended Enumeration

```bash
dnsenum --threads 50 -f /usr/share/seclists/Discovery/DNS/all.txt -r -o tesla_domain tesla.com --dnsserver edns69.ultradns.com
```

> Use this with a **more comprehensive wordlist** for thorough DNS enumeration.

---

## 🏢 Internal Network Target with Custom Resolver

```bash
dnsenum --threads 64 --dnsserver 10.10.10.224 -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt htbhost.htb
```

> Targeting an **internal domain** with a specified DNS server in a lab or corporate environment.

---

## ⚙️ Option Breakdown

| Option        | Description                                        |
| ------------- | -------------------------------------------------- |
| `-f`          | File path to the subdomain brute-force wordlist    |
| `-r`          | Enables reverse lookups on IP addresses found      |
| `-o`          | Output file or folder for saving results           |
| `--threads`   | Sets number of concurrent threads (improves speed) |
| `--dnsserver` | Specify custom DNS server to resolve queries       |

---

## 💡 Pro Tips

* 🧪 Test **dnsenum** first on training domains like `zonetransfer.me` before using it on production targets.
* 🔗 Combine with tools like **massdns**, **amass**, and **subfinder** for wider reconnaissance coverage.
* ⚖️ Always ensure you are working within **legal and authorized scopes** for DNS enumeration.

---

## ✅ Key Takeaway

* **dnsenum** is powerful for **active DNS enumeration**
* Works well with **custom resolvers and large wordlists**
* Best used during **early reconnaissance and brute-force phases**
* Combine with **passive tools** for maximum coverage 🔥
