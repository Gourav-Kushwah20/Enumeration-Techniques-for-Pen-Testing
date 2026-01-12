# 🌐 Internet Archives and Subdomain Enumeration

## 📚 Internet Archives and Subdomain Enumeration

**Internet Archives** are large-scale web crawlers and indexing systems that periodically scan websites and store historical snapshots of their content. These archives are extremely valuable for **subdomain enumeration**, as they often explain infrastructure that no longer appears in DNS or search engines.

By analyzing historical records, we can:

- 🕰️ Discover **old, forgotten, or deprecated subdomains**
- 🔁 Generate **permutations** to uncover additional valid subdomains
- 🕵️ Improve **passive reconnaissance** during penetration testing and bug bounty hunting

---

## 🧩 Extracting Historical Subdomains

### 🔍 Querying Internet Archives for URLs

We use tools like `waybackurls`, `gau`, or `gauplus` to retrieve archived URLs for a target domain.

---

### 🗄️ Using `waybackurls`

```bash
waybackurls instagram.com > insta.com-waybackurls.txt
```

This fetches all known URLs for `tesla.com` from the Wayback Machine.

---

### 🚀 Using `gau` (GetAllUrls)

```bash
gau instagram.com > insta.com-gau.txt
```

## 🔎 Sources Used by `gau`

`gau` pulls URLs from multiple sources, including:

- 🗄️ Wayback Machine  
- 🌍 Common Crawl  
- 🔗 URLScan  
- 🛡️ VirusTotal  

---

## 🧪 Extracting Unique Subdomains from URLs

Archived tools return **full URLs**, but we usually only need the **subdomains**.  
This is done using [`unfurl`](https://github.com/tomnomnom/unfurl).

```bash
cat tesla.com-gau.txt | unfurl -u domains | sort -u > subdomains.txt
```

---

## 📖 Explanation

* 🔍 `unfurl -u domains` → Extracts domain names from URLs
* ♻️ `sort -u` → Removes duplicate entries and keeps results unique


## 📄 Example Output (`subdomains.txt`)

```text
about.instagram.com
about.intern.instagram.com
accountscenter.instagram.com
api.instagram.com
```

---

## 🔁 Generating Subdomain Permutations

## 🧬 dnsgen

**dnsgen** is a permutation-based subdomain generation tool widely used in reconnaissance, bug bounty hunting, and penetration testing.  
It creates possible subdomains by applying common patterns, prefixes, suffixes, and mutations to known domains or subdomains.

---

## ❓ What `dnsgen` Does

### 📥 dnsgen takes:
- 🌐 A base domain or list of known subdomains  
- 📃 Optional wordlists  

### 📤 And generates:
- 🆕 New subdomain permutations  
- 🧪 Common development, staging, API, and infrastructure variants  

> ⚠️ **Note:** Output from `dnsgen` is **not validated**.  
> Always resolve results using a DNS resolver.

---

## ⚙️ Installation

### 📦 Using pip
```bash
pip install dnsgen
```

### 🧱 Or from source

```bash
git clone https://github.com/ProjectAnte/dnsgen.git
```
```bash
cd dnsgen
```
```bash
python3 setup.py install
```

## 🚀 Basic Usage

### 🌐 Generate subdomains from a domain
```bash
dnsgen domain_list.txt
```

---

### 📚 Generate subdomains using a wordlist

```bash
dnsgen -w deepmagic.com-prefixes-top500.txt domain_list.txt
```

#### 📝 Explanation:

* `-w` → Wordlist for prefixes/suffixes

---

## 🧠 Typical Recon Pipeline

`dnsgen` is usually chained with a DNS resolution tool:

```bash
dnsgen -w deepmagic.com-prefixes-top500.txt -f instagram.com | dnsx -silent
```

### 🔄 Flow:

1. 🧩 Generate permutations with `dnsgen`
2. 🌐 Resolve valid domains using `dnsx`
3. ✅ Output only live subdomains

---

## 🔁 Using Existing Subdomains as Input

```bash
cat subdomains.txt | dnsgen | dnsx -silent
```




