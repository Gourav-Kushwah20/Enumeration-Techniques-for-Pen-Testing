# 🔎 PureDNS

[PureDNS GitHub Repository](https://github.com/d3mondev/puredns)

**PureDNS** is a fast and reliable DNS resolution and subdomain brute-forcing tool.  
It is designed to handle **large datasets efficiently** while mitigating common DNS issues such as:

- Wildcard domains  
- DNS poisoning  

PureDNS is commonly used alongside **MassDNS** and **DNSValidator** for optimal results.

---

## ✅ Prerequisites

### 1️⃣ MassDNS

MassDNS is a high-performance DNS stub resolver required by PureDNS for **bulk DNS lookups**.

#### Clone the repository
```bash
cd /opt
```

```bash
git clone https://github.com/blechschmidt/massdns.git
```

#### Compile and install

```bash
cd /opt/massdns
make
make install
```

---

## 📦 Install PureDNS

PureDNS is written in **Go** and can be installed directly using `go install`.

```bash
go install github.com/d3mondev/puredns/v2@latest
```

Move the binary to a system-wide location:

```bash
cp -v ~/go/bin/puredns /usr/local/bin/
```

---

# 🔐 DNSValidator

**DNSValidator** is used to build a **clean, reliable list of public DNS resolvers** for use with **PureDNS**.  
It filters out slow, unreliable, poisoned, or non-recursive resolvers.


## 📥 Download Public Resolver List

Download a large public DNS resolver list:

```bash
wget https://public-dns.info/nameservers-all.txt -O /opt/nameservers-all.txt
```

Check how many resolvers are in the list:

```bash
cat /opt/nameservers-all.txt | wc -l
```

Search for a specific resolver (example: Google DNS):

```bash
cat /opt/nameservers-all.txt | grep 8.8.8.8
```

---

## 🛠️ Install DNSValidator

### Clone the repository

```bash
cd /opt
```
```
git clone https://github.com/vortexau/dnsvalidator.git
```

### Navigate into the directory

```bash
cd dnsvalidator
```

### Install dependencies

```bash
pip install -r requirements.txt
```

### Install DNSValidator

```bash
python3 setup.py install
```

---

## ▶️ Run DNSValidator

Start DNSValidator:

```bash
dnsvalidator
```

Display the help menu:

```bash
dnsvalidator -h
```

---

## ➕ Additional Resolver Sources

### Trickest Resolvers
```bash
cd /opt
```
```
git clone https://github.com/trickest/resolvers.git
```

---

### Other Public Resolver Lists

```bash
wget https://public-dns.info/nameservers.txt
```

```bash
wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Miscellaneous/dns-resolvers.txt
```

---

### Count Resolvers (example – SecLists)

```bash
wc -l /usr/share/seclists/Miscellaneous/dns-resolvers.txt
```

---

## ✅ Validate and Generate Resolver List

Generate a **clean, reliable resolver list** using DNSValidator:

```bash
dnsvalidator -tL /opt/nameservers-all.txt -threads 50 -o /opt/resolvers.txt
```

---

### Alternative Inputs

Using a temporary resolver list:

```bash
dnsvalidator -tL /tmp/dns-resolvers.txt -threads 50 -o /opt/resolvers.txt
```
```bash
cat /opt/resolvers.txt | wc -l
```

Using SecLists resolvers directly:

```bash
dnsvalidator -tL /usr/share/seclists/Miscellaneous/dns-resolvers.txt -threads 50 -o /opt/resolvers.txt
```

---

## 🧠 Notes & Best Practices

* Always **validate resolvers** before using them with **MassDNS / PureDNS**
* Rotate resolver lists regularly to avoid:

  * Rate limiting
  * DNS poisoning
  * False positives
* Use **50–100 threads** for validation (adjust based on bandwidth & CPU)

---
## 🧠 Usage PureDNS
```bash
puredns -v
```
```bash
puredns -h
```
```bash
puredns bruteforce -h
```

---

## 🔨 Bruteforce Mode

### Basic Bruteforce

```bash
puredns bruteforce /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt google.com -r /opt/resolvers.txt
```

---

### Quiet Mode

```bash
puredns bruteforce /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt google.com -r /opt/resolvers.txt -q
```

---

### Using Custom Resolvers

```bash
puredns bruteforce /opt/subdomain-wordlists/all-subdomains.txt -r /opt/resolvers.txt google.com
```

---

### Save Output Quietly

```bash
puredns bruteforce /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -r /opt/resolvers.txt google.com -w google_vaild_domain.txt -q
```

---

### Wildcard Filtering with Rate Limit

```bash
puredns bruteforce /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -r /opt/resolvers.txt google.com -l 500 --wildcard-batch 100 -w google_valid_domains.txt
```

---

### Large Brute-force Example

```bash
puredns bruteforce /opt/subdomains/master_subdomains_wordlist.txt -l 5000 --wildcard-batch 100 -r /opt/my-resolvers/resolvers2.txt tesla.com
```

---

## 🧠 Notes

* `-r` → Custom validated resolvers (highly recommended)
* `-q` → Quiet mode (clean output)
* `-w` → Write valid subdomains to file
* `-l` → Rate limiting (prevents bans & resolver drops)
* `--wildcard-batch` → Handles wildcard DNS efficiently

---

## 📚 Using SecLists Wordlists

### Top 20k subdomains
```bash
puredns bruteforce /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -r /opt/resolvers.txt -l 50 --wildcard-batch 1000 -w tesla_valid_domains.txt tesla.com
```

### Skip wildcard validation (use with caution)

```bash
puredns bruteforce /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -r /opt/resolvers.txt tesla.com --wildcard-batch 100000 --skip-validation -w tesla.com.txt
```

---

## ✍️ Generate Custom Wordlists (mksub)

🔗 [mksub GitHub Repository](https://github.com/d3mondev/puredns)

```bash
go install github.com/trickest/mksub@latest
```

```bash
cp -v ~/go/bin/mksub /usr/local/bin/
```

```bash
mksub -d tesla.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -o tesla_wordlist.txt
```

```bash
 cat tesla_wordlist.txt| wc -l                                          
```

---

## 🌐 Resolve Mode

### Help

```bash
puredns resolve -h
```

### Resolve generated wordlist

```bash
puredns resolve tesla_wordlist.txt -r /opt/resolvers.txt
```

### 🔎 Resolve Saved Results
```bash
puredns resolve tesla.com.txt -r /opt/resolvers.txt
```


### Resolve a list using custom resolvers
```bash
puredns resolve subs.txt -r /opt/resolvers.txt
```

### Save resolved output to a file

```bash
puredns resolve subs.txt -r /opt/resolvers.txt -w resolved.txt
```

### Quiet mode (suppress progress output)

```bash
puredns resolve subs.txt -r /opt/resolvers.txt -q
```

### Increase rate limit for large lists

```bash
puredns resolve subs.txt -r /opt/resolvers.txt -l 500
```

---

## 🧹 Amass / Subfinder Cleanup

Use PureDNS to validate and clean results from other tools:

```bash
puredns resolve amass.txt -r /opt/resolvers.txt -w amass_valid.txt
```

This removes:

* ❌ Dead subdomains
* ❌ False positives
* ❌ Wildcard/noise entries

---

## 🚩 Important Flags

| Flag                | Description                                             |
| ------------------- | ------------------------------------------------------- |
| `-r`                | Resolver list file (**recommended**)                    |
| `-w`                | Write output to file                                    |
| `-q`                | Quiet mode                                              |
| `-l`                | Rate limit (queries per second)                         |
| `--skip-validation` | Skip wildcard & poisoning checks (**use with caution**) |

---

## 🔍 Resolve vs Bruteforce

| Feature | Resolve | Bruteforce |
|-------|---------|------------|
| Generates subdomains | ❌ No | ✅ Yes |
| Validates existing list | ✅ Yes | ❌ No |
| Wildcard filtering | ✅ Yes | ✅ Yes |
| Best for cleanup | ✅ Yes | ❌ No |

---

## 🔁 Typical Recon Workflow

```bash
subfinder -d example.com -o subs.txt
````

```bash
amass enum -passive -d example.com >> subs.txt
```

```bash
sort -u subs.txt > all_subs.txt
```

```bash
puredns resolve all_subs.txt -r /opt/resolvers.txt -w live_subs.txt
```

---

## 📝 Notes

* Always use **validated resolvers** to avoid false positives
* If results are empty, **reduce rate limit** or **regenerate resolvers**
* Avoid `--skip-validation` unless wildcard DNS is unavoidable
* Common next steps:

  * `httpx`
  * `nuclei`
  * `naabu`

---
