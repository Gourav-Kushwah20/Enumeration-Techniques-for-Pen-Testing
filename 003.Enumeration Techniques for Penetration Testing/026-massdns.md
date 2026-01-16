# ⚡ MassDNS

[MassDNS Repo]

MassDNS is a **high-performance DNS stub resolver** for bulk lookups and reconnaissance.  
It supports **A, AAAA, CNAME, and PTR** record types and is frequently used in **subdomain enumeration workflows**.

---

## 📦 Installation

### Clone the MassDNS repository
```bash
git clone https://github.com/blechschmidt/massdns.git
```

### Navigate to the MassDNS directory

```bash
cd /opt/massdns/
```

### Build the MassDNS binary

```bash
make
```

### Create a symbolic link to use MassDNS globally

```bash
ln -s /opt/massdns/bin/massdns /usr/local/bin/massdns
```

---

## ✅ Verify Installation

Check if MassDNS is accessible and view available options:

```bash
massdns -h
```

---

## 🌐 Resolver List

MassDNS requires a **list of DNS resolvers** to function properly.

```bash
# Example (commonly used resolver list from SecLists)
cat /usr/share/seclists/Miscellaneous/dns-resolvers.txt
```
```
cat /opt/massdns/lists/resolvers.txt | wc -l
```

> 💡 Using **clean and reliable resolvers** is critical to avoid false positives and rate-limiting.

🧾 Online Resolver List

You can download a ready-made resolver list for MassDNS from the official repository:

https://raw.githubusercontent.com/blechschmidt/massdns/master/lists/resolvers.txt


---

## 🛠️ Preparing the Wordlist

Copy a DNS wordlist from **SecLists** for brute-forcing subdomains:

```bash
cp /usr/share/seclists/Discovery/DNS/all.txt all.txt
```
```bash
cp -v /usr/share/dnsenum/dns.txt Downloads/enum-technique/dns.txt
```
Append the target domain (e.g. `tesla.com`) to each entry:

```bash
sed -i -e 's/$/.tesla.com/' all.txt
```
```bash
sed -i -e 's/$/.instagram.com/' dns.txt
```

Preview the first 1000 entries:
```bash
head -n 1000 dns.txt
```

Preview the last 1000 entries:

```bash
tail -n 1000 dns.txt
```

---

## 🌐 Subdomain Enumeration Using A Records

Use **MassDNS** to resolve subdomains to **A records**:

```bash
massdns -r /usr/share/seclists/Miscellaneous/dns-resolvers.txt -t A dns.txt -o S 
-w inst_domain.txt
```

* `-r` → Resolver list
* `-t A` → Query A records
* `-o S` → Simple output format
* `-w` → Write output to file

---

## 🔗 Using CNAME Resolution

Run MassDNS with **CNAME** type to discover alias relationships:

```bash
massdns -t CNAME -w tesla.com.CNAME.txt -o S -r /opt/resolvers.txt tesla.com.txt
```
---

## 🧹 Post-processing Results

### Count how many results were returned
```bash
cat tesla_domain.txt | wc -l
```

### Clean up the output by removing record types and trailing dots

```bash
sed -e 's/A.*//; s/CN.*//; s/\.$//' tesla_domain.txt
```

### Or apply the changes directly to the file

```bash
sed -i -e 's/A.*//; s/CN.*//; s/\.$//' tesla_domain.txt
```

---

## 🔗 CNAME Lookup for All Subdomains

Run a CNAME lookup for every discovered subdomain:

```bash
massdns -r /opt/massdns/lists/resolvers.txt -t CNAME all.txt -o S -w tesla_domain_cname.txt
```

This helps identify:

* CDN endpoints
* Third-party services
* Alias chains

---

## 🤖 JSON Output for Automation

Use the `-o J` option to produce **JSON-formatted output**, useful for scripting and pipelines:

```bash
massdns -r /opt/resolvers/resolvers.txt -t A subdomains-top1million-5000.txt -o J -w tesla.com.json
```

Ideal for:

* Automation workflows
* Parsing with `jq`
* Feeding into other recon tools

---

## 🔁 PTR Record Enumeration

Reverse DNS lookups use **PTR records** to resolve IP addresses back to hostnames.

### Format IP addresses for PTR lookup

```bash
sed -i -e 's/$/.in-addr.arpa/' ip.txt
```

### Verify the file contents

```bash
cat ip.txt
```


## 🔁 Perform PTR Queries

Run PTR (reverse DNS) lookups using **MassDNS**:

```bash
massdns -r /usr/share/seclists/Miscellaneous/dns-resolvers.txt -t PTR ip.txt -o S -w hosts-ptr.txt
```

---

## 🏷️ Extract Hostnames from the PTR Results

Extract only the resolved hostnames from the output file:

```bash
cut -f3 -d " " hosts-ptr.txt
```

---

## 🎁 Bonus: Using Assetfinder with MassDNS

### Install Assetfinder

Assetfinder discovers subdomains from **public OSINT sources**:

```bash
apt install assetfinder
```

---

### Count Discovered Subdomains for a Domain

```bash
assetfinder tesla.com | wc -l
```

---

### Pipe Assetfinder Results Directly into MassDNS

Resolve Assetfinder-discovered subdomains using MassDNS:

```bash
assetfinder tesla.com | massdns -r /opt/massdns/lists/resolvers.txt -o S -w tesla_domain2.txt
```

---


