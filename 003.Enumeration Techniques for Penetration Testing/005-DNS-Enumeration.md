# 🌐 DNS Enumeration

## 🔍 DNS Enumeration

**DNS Enumeration** is the process of collecting information about a domain and its DNS records to map out the domain’s infrastructure.  
It helps identify subdomains, mail servers, name servers, and other publicly available information that could reveal potential attack vectors.

> before we DNS enum we are check the scope of target.

reference: https://bugbounty.meta.com/scope/

---

## 🧱 Vertical Domain Co-Relation 

Examples of vertical domain co-relation, where **subdomains** are associated with the main domain:

- **armourinfosec.com**
  - admin.armourinfosec.com
  - mail.armourinfosec.com

- **tesla.com**
  - admin.tesla.com
  - mail.tesla.com
  - cp.tesla.com
  - test.tesla.com

---

## 🔗 Horizontal Domain Co-Relation

Examples of horizontal domain co-relation, where domains are associated across different TLDs or organizations:

- **armourinfosec domains**
  - *.thehackersworld.com
  - *.infosecwarrior.com
  - *.armourinfosec.io

- **tesla domains**
  - *.tesla.cn
  - *.teslamotors.com
  - *.tesla.services
  - *.teslainsuranceservice.com
  - *.solarcity.com

---

## ⭐ Why DNS Enumeration is Important

- **Information Gathering** – It allows attackers and security testers to gather data about the target’s network.
- **Identifying Attack Surfaces** – Misconfigured DNS records, exposed subdomains, and outdated infrastructure can be potential entry points.
- **Social Engineering** – Collected data can be used to craft more targeted phishing or social engineering attacks.
- **Pentesting & Red Teaming** – Understanding the DNS infrastructure helps in simulating real-world attack scenarios.

---

## 🧪 Types of DNS Enumeration

### 1️⃣ Direct Domain Enumeration
- Identifying subdomains and associated records through direct queries.

### 2️⃣ Reverse DNS Lookup
- Resolving an IP address back to its domain name.

### 3️⃣ Zone Transfer (AXFR) Enumeration
- Attempting to transfer the entire DNS zone file from a misconfigured DNS server.

### 4️⃣ Brute-Force Subdomain Discovery
- Trying common subdomain names to identify valid ones.

### 5️⃣ PTR Record Lookup
- Resolving IP addresses to domain names.

### 6️⃣ Certificate Transparency Logs
- Checking for subdomains and domains listed in publicly available SSL/TLS certificates.

### 7️⃣ WHOIS Lookup
- Gathering domain registration and ownership details.

---

## 🎯 Target Range

IP Address to Domain Name mapping within a specified range:

- 192.168.1.1/24
- 192.31.242.107
- 192.31.242.107/32
- 2620:134:b000::/40
- 192.31.243.0/26
- 192.31.243.64/28
- 192.31.243.96/27

---

## 📘 Common DNS Record Types

| Record Type | Description                                                     |
|-------------|-----------------------------------------------------------------|
| A           | Maps a domain to an IPv4 address                                |
| AAAA        | Maps a domain to an IPv6 address                                |
| CNAME       | Alias of one domain to another                                  |
| MX          | Mail server records                                             |
| NS          | Name server records                                             |
| SOA         | Start of Authority, contains domain admin and refresh info      |
| TXT         | Text records, used for SPF, DKIM, and other metadata             |
| PTR         | Maps an IP address to a domain (reverse lookup)                 |

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

## 🧪 Example DNS Enumeration Commands

### 1. Find all DNS records using `dig`

```bash
dig armourinfosec.com ANY
```

### 2. Reverse lookup for PTR records using `dig`

```bash
dig -x 8.8.8.8
```

### 3. Find subdomains using `dnsrecon`

```bash
dnsrecon -d armourinfosec.com -t std
```

### 4. Find subdomains using `sublist3r`

```bash
sublist3r -d armourinfosec.com
```

### 5. Perform zone transfer using `dig`

```bash
dig axfr @ns1.armourinfosec.com armourinfosec.com
```

---

