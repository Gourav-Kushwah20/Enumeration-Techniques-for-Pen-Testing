# 🧠 DNS-Subdomain-Takeover

## 🎯 DNS Subdomain Takeover

* This document outlines a **structured and practical methodology** for detecting **DNS subdomain takeovers** using open-source tools such as `puredns`, `massdns`, `dnsx`, `httpx`, and `nuclei`.
* A **subdomain takeover** occurs when a DNS record (usually a **CNAME**) points to a third-party service (e.g., S3, Heroku, GitHub Pages), but the resource on that service is **unclaimed, deleted, or misconfigured**, allowing an attacker to claim it.

---

## 🧰 Tools Used

* **puredns** – High-performance brute-force DNS enumeration
* **subfinder** – Passive subdomain discovery
* **massdns** – Bulk DNS resolution (CNAME, A, etc.)
* **dnsx** – Fast DNS resolver and CNAME extractor
* **httpx** – HTTP probing and service fingerprinting
* **nuclei** – Vulnerability scanner with takeover templates
* **takeover.py** – Python-based takeover detection script

---

## 🔎 1. Subdomain Enumeration (Active + Passive)

### 🕵️ Passive Enumeration

```bash
subfinder -d subdomaintakeovers.com -silent > subs_passive.txt
```


### ⚡ Active Brute-Forcing

```bash
puredns bruteforce /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt subdomaintakeovers.com -r /opt/resolvers.txt --skip-validation -w subs_active.txt
```

---

## 🧩 Combine and Deduplicate

```bash
cat subs_passive.txt subs_active.txt | sort -u > subs_all.txt
```

---

## 🌐 2. Resolve CNAME Records

### ⚡ Using dnsx (Fast & Clean)

```bash
dnsx -l subs_all.txt -silent -cname -resp -r /opt/resolvers.txt -o cname_raw.txt
```

---

### 🧪 Using massdns (Alternative)

```bash
massdns -r /opt/resolvers.txt -t CNAME subs_all.txt -o S -w cname_massdns.txt
```

---

## 🔗 3. Filter External CNAMEs

### 🚫 Remove internal or self-referencing CNAMEs

```bash
grep -vE "(subdomaintakeovers\.com\.?$)" cname_raw.txt > cname_external.txt
```

---

### 🧹 Extract only subdomain names and normalize

```bash
cut -d " " -f 1 cname_external.txt | sed 's/\.$//' > cname_hosts.txt
```

---

## 🔇 4. Noise Reduction (Optional but Recommended)

Exclude known owned infrastructure to reduce false positives:

```bash
grep -vE "(cloudflare\.net|amazonaws\.com\.cn|googleusercontent\.com)" cname_hosts.txt > cname_filtered.txt
```

> 📝 **Note:** This step is **target-specific** and should be adjusted per organization.

---

## 🧪 5. Scan for Takeovers Using Nuclei

```bash
nuclei -list cname_filtered.txt -t ~/nuclei-templates/takeovers -severity low,medium,high
```

### 📦 Recommended Template Sources

* 🔗 [https://github.com/projectdiscovery/nuclei-templates](https://github.com/projectdiscovery/nuclei-templates)
* 🔗 [https://github.com/EdOverflow/can-i-take-over-xyz](https://github.com/EdOverflow/can-i-take-over-xyz)

---

## ⚡ 6. DNSX → Nuclei One-Liner

Quickly pipe CNAME results directly into Nuclei:

```bash
dnsx -l subs_all.txt -silent -cname -resp-only | nuclei -t ~/nuclei-templates/takeovers/
```

---

## 🌍 7. Probe HTTP Services

### 🔍 Identify live services and fingerprints

```bash
httpx -l subs_all.txt -silent -status-code -title -web-server -tech-detect -location
```

---

### 👀 Look For

* ❌ **404** or service-specific error pages
* 💬 Messages like **"No such app"**, **"Bucket does not exist"**
* 🏷️ Third-party branding **without ownership**


---

## ✅ 8. Final Validation (Critical Step)

### 🚨 Before reporting a takeover:

1. 🔐 **Verify** the service allows claiming
2. 👤 **Confirm** there is no existing owner
3. 🔎 **Cross-check** against

   * [https://github.com/EdOverflow/can-i-take-over-xyz](https://github.com/EdOverflow/can-i-take-over-xyz)
4. 📸 **Capture evidence**:

   * HTTP response
   * DNS records
   * Error messages

> ⚠️ **Never claim resources without written authorization.**

---

## 🤖 9. Python Automation (takeover.py)

### 📥 Setup

```bash
git clone https://github.com/antichown/subdomain-takeover
cd subdomain-takeover
pip install -r requirements.txt
```

---

### ▶️ Run the tool

```bash
python takeover.py \
  -d subdomaintakeovers.com \
  -w cname_hosts.txt \
  -t 20
```

---

## 🧪 Example Takeover Candidates

```text
bucket.subdomaintakeovers.com   CNAME bucket-test1.s3.amazonaws.com
blog.subdomaintakeovers.com     CNAME blog-test1.wordpress.com
api.subdomaintakeovers.com      CNAME myapi-test.ngrok.io
```

> 📝 These **must be manually verified** to confirm whether the backing service is **unclaimed**.

---

## 📚 References

* 🔗 [https://github.com/EdOverflow/can-i-take-over-xyz](https://github.com/EdOverflow/can-i-take-over-xyz)

---

## 📝 Notes for Reporting

* 🔥 **Severity** is usually **High** if the service is confirmed claimable
* 📎 Include **DNS proof**, **HTTP proof**, and **service documentation**
* 🚫 Avoid **speculative reporting** without proper validation

---

