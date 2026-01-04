# 🛠️ DNS Client Tools

## 🌐 Default Ports / Common DNS Ports

* **TCP:** `53`
* **UDP:** `53`

---

## 📌 Example Commands

### 1. Scan DNS ports using `nmap`

```bash
nmap -v -sV -sT -sU -p T:53,U:53 192.168.1.43
```

---

### 2. Comprehensive DNS service scan with `nmap`

```bash
nmap -v -Pn -sV -sC -sT -sU -p T:53,U:53 192.168.1.43
```

---

### 3. Test DNS connectivity using `netcat` (TCP)

```bash
nc -v 192.168.1.43 53
```

---

### 4. Test DNS connectivity using `netcat` (UDP)

```bash
nc -vu 192.168.1.43 53
```

---
## 🔍 Key DNS Enumeration Tools

| Tool          | Purpose                           | Example Command                                                            |
| ------------- | --------------------------------- | -------------------------------------------------------------------------- |
| **nslookup**  | Query DNS records                 | `nslookup armourinfosec.com`                                               |
| **dig**       | Detailed DNS lookup               | `dig armourinfosec.com ANY`                                                |
| **host**      | Simple DNS lookup                 | `host armourinfosec.com`                                                   |
| **nmap**      | DNS and port scanning             | `nmap -p 53 --script=dns-brute armourinfosec.com`                          |
| **dnsrecon**  | Automated DNS enumeration         | `dnsrecon -d armourinfosec.com`                                            |
| **dnsenum**   | Brute force DNS enumeration       | `dnsenum armourinfosec.com`                                                |
| **sublist3r** | Subdomain enumeration             | `sublist3r -d armourinfosec.com`                                           |
| **crt.sh**    | Certificate search for subdomains | [https://crt.sh/?q=armourinfosec.com](https://crt.sh/?q=armourinfosec.com) |

---

## ⚙️ Installing and Verifying Bind-Utils

## 1. Check if `bind-utils` is installed

```bash
rpm -qa | grep bind
```

---

## 2. Install `bind-utils` using `yum`

```bash
yum install bind-utils
```

---

## 3. Check the installed version of `bind-utils`

```bash
rpm -qi bind-utils-9.11.4.26.P2.el7_9.5.x86_64
```

---

## 4. List the installed files from `bind-utils` package

```bash
rpm -ql bind-utils-9.11.4.26.P2.el7_9.3.x86_64
```

---

## 🧰 Common DNS Client Tools in `bind-utils`

| Tool         | Path                | Description                |
| ------------ | ------------------- | -------------------------- |
| **dig**      | `/usr/bin/dig`      | Query DNS records          |
| **host**     | `/usr/bin/host`     | Simple DNS lookup          |
| **nslookup** | `/usr/bin/nslookup` | Interactive DNS query tool |

---

# 🌐 DNS Queries Using `dig`

## 🔹 Basic Usage

### 1. Query a domain’s DNS records

```bash
dig google.com
```

---

### 2. Specify a custom DNS server

```bash
dig @8.8.8.8 google.com
```

---
# 🔎 Query Specific DNS Records

### 1. **A Record (IPv4)**

```bash
dig google.com A
```

---

### 2. **AAAA Record (IPv6)**

```bash
dig google.com AAAA
```

---

### 3. **NS Record (Name Server)**

```bash
dig google.com NS
```

---

### 4. **MX Record (Mail Exchange)**

```bash
dig google.com MX
```

---

### 5. **SOA Record (Start of Authority)**

```bash
dig google.com SOA
```

---

### 6. **TXT Record (Text Information)**

```bash
dig google.com TXT
```

---

### 7. **ALL Records**

```bash
dig google.com ANY
```

---

### 8. **HINFO Record (Host Information)**

```bash
dig armourinfosec.com HINFO
```

---


## 🧹 Simplified Output

### 1. Shortened output for cleaner results

```bash
dig google.com +short
```

---

### 2. Shortened output for specific records

```bash
dig armourinfosec.com NS +short
```
```bash
dig armourinfosec.com MX +short
```
```bash
dig google.com ANY +short
```

---

## 🎛️ Customizing Output

### 1. Suppress all output

```bash
dig google.com +noall
```

---

### 2. Show only the answer section

```bash
dig google.com +noall +answer
```

---

### 3. Show both question and answer sections

```bash
dig google.com +noall +answer +question
```

---

### 4. Clean output by removing comments and unnecessary sections

```bash
dig google.com +nocomments +noquestion +noauthority +noadditional +nostats
```

---


## 📦 Batch Domain Queries

### 1. Create a list of domains

```bash
vim domain_list.txt
```

**Example content:**

```text
google.com
facebook.com
armourinfosec.com
youtube.com
```

---

### 2. Query multiple domains from a file

```bash
dig -f domain_list.txt
```

---

### 3. Short output for batch queries

```bash
dig -f domain_list.txt +short
```

---

## 🔁 Reverse DNS Lookup

### 1. PTR record lookup for an IP address

```bash
dig -x 8.8.8.8
```

---

### 2. Shortened PTR record lookup

```bash
dig -x 8.8.8.8 +short
```

---

## 🔄 Batch Reverse DNS Lookup

### 1. Create a list of IP addresses

```bash
vim ip_add_list.txt
```

## 📄 Example Content

```text
8.8.8.8
64.6.64.6
8.8.4.4
1.1.1.1
20.20.20.20
```

---

## 2. Format the list using `awk`

```bash
awk '{print "-x " $0}' ip_add_list.txt > ip_add_list2.txt
```

---

## 3. Format the list using `sed`

```bash
cat ip_add_list.txt | sed -e 's/.*/-x &/' > ip_add_list3.txt
```

---

## 4. Perform batch reverse lookup

```bash
dig -f ip_add_list2.txt +short
```

---

## 5. Alternative batch lookup

```bash
dig -f ip.txt +short
```

---

## 🌐 DNS Queries Using `host`

The `host` command is a simple DNS lookup utility used to convert domain names to IP addresses and retrieve other DNS records.



## 🔹 Basic Usage

### 1. Lookup IP address for a domain

```bash
host google.com
```

---

## 🔎 Query Specific DNS Records (using `host`)

### 1. Lookup **NS (Name Server)** records

```bash
host -t ns google.com
```

---

### 2. Lookup **MX (Mail Exchange)** records

```bash
host -t mx google.com
```

---

### 3. Lookup **SOA (Start of Authority)** record

```bash
host -t soa google.com
```

---

## 🌐 DNS Queries Using `nslookup`

The `nslookup` (Name Server Lookup) command is used to query Internet name servers interactively or non-interactively for information about hostnames, IP addresses, and DNS records.

## 🔹 Basic Usage

### 1. Lookup IP address for a domain

```bash
nslookup google.com
```

---

### 2. Specify a custom DNS server

```bash
nslookup google.com 64.6.64.6
```

---

## 🔎 Query Specific DNS Records (using `nslookup`)


### 1. Lookup **A (IPv4)** records

```bash
nslookup -type=A google.com
```

---

### 2. Lookup **AAAA (IPv6)** records

```bash
nslookup -type=AAAA google.com
```
---

### 3. Lookup **NS (Name Server)** records

```bash
nslookup -type=NS google.com
```

---

### 4. Lookup **MX (Mail Exchange)** records

```bash
nslookup -type=MX google.com
```

---

### 5. Lookup **SOA (Start of Authority)** record

```bash
nslookup -type=SOA google.com
```

---

### 6. Lookup **TXT (Text)** records

```bash
nslookup -type=TXT google.com
```

---

### 7. Lookup **all available records**

```bash
nslookup -type=any google.com
```

---

## 🌐 Lookup Specific Domain


### 1. Lookup a specific domain

*(example: `armourinfosec.com`)*

```bash
nslookup www.armourinfosec.com
```

---

## 🖥️ Interactive Mode

You can use `nslookup` in interactive mode to perform multiple queries:

```bash
nslookup
```

### Example interactive session:

```text
> facebook.com
> set type=ns
```

---
