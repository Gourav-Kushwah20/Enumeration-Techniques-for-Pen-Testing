# ➕ gauplus

🔗 **GitHub Repository:**  
https://github.com/bp0lr/gauplus

**gauplus** is an enhanced version of `gau` (GetAllUrls).  
It aggregates archived URLs from multiple public sources, making it extremely useful for **reconnaissance**, **endpoint discovery**, and **subdomain enumeration**.

---

## 📊 Data Sources Used by gauplus

`gauplus` collects URLs from several well-known archives:

- 🗄️ **Wayback Machine** – Historical snapshots of websites  
- 🌐 **Common Crawl** – Large-scale web crawl datasets  
- 🛡️ **VirusTotal** – URLs observed through malware and threat intelligence feeds  
- 🔍 **URLScan.io** – URLs captured during website scans  
- 📚 **Other public archives** – Additional passive data sources  

---

## ⚙️ Installation

Make sure **Go** is installed and configured correctly, then run:

```bash
go install github.com/bp0lr/gauplus@latest
```

### ✅ Verify installation

```bash
gauplus -h
```
---
## 📌 Usage

## 🌐 Fetch URLs for a Domain

To retrieve archived URLs for a domain (including subdomains):

```bash
gauplus -t 5 -random-agent -subs instagram.com
```

### 💾 Save output to a file

```bash
gauplus -t 5 -random-agent -subs instagram.com > insta.com-gauplus.txt
```

---

## 🧾 Explanation of Common Flags

* 🧵 `-t 5`
  Number of concurrent threads (default: `1`). Higher values improve speed.

* 🎭 `-random-agent`
  Uses random User-Agent strings to reduce blocking or rate limiting.

* 🌍 `-subs`
  Includes all discovered subdomains in the results.

---

## 🧩 Extracting Only Subdomains

Since `gauplus` outputs **full URLs**, you can extract just the domain names using `unfurl`.

### 🔎 Extract domains to stdout

```bash
cat insta.com-gauplus.txt | unfurl -u domains
```

### 💾 Save extracted domains to a file

```bash
cat insta.com-gauplus.txt | unfurl -u domains > insta.com-domains.txt
```

---

## ⚡ One-liner (Recommended)

```bash
gauplus -t 5 -random-agent -subs instagram.com | unfurl -u domains > insta.com-domains.txt
```
---

## 🧪 Example Output

### ▶️ Running:
```bash
gauplus -t 5 -random-agent -subs tesla.com | unfurl -u domains
```

### 📄 May produce:

```text
www.tesla.com
shop.tesla.com
blog.tesla.com
api.tesla.com
energy.tesla.com
```

---

## 💡 Tips & Best Practices

* ♻️ Pipe output into `sort -u` to remove duplicates:

```bash
gauplus -subs tesla.com | unfurl -u domains | sort -u
```

* 🔗 Combine with tools like `httpx`, `nuclei`, or `ffuf` for further testing

* 🕵️ Best suited for **passive reconnaissance**
  *(no direct interaction with the target infrastructure)*

---


