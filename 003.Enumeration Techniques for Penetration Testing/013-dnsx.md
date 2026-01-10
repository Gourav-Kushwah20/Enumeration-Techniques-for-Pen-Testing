# 🌐 dnsx

**dnsx** is a **fast and multi-purpose DNS toolkit** 🧰 that allows running multiple DNS queries using a list of **user-supplied resolvers**.  
It’s widely used in **reconnaissance** and **subdomain validation** workflows 🚀.

---

## ⚙️ Installing dnsx

### 🧑‍💻 Using `go install`
```bash
go install -v github.com/projectdiscovery/dnsx/cmd/dnsx@latest
````

---

### 🕰️ Using `go get` (for older Go versions)

```bash
GO111MODULE=on go get -v github.com/projectdiscovery/dnsx/cmd/dnsx
```

---

## 📂 Moving the Binary to System Path

Move the compiled binary so it can be accessed globally 🌍:

```bash
cp -v /root/go/bin/dnsx /usr/local/bin/
```

---

## ✅ Verifying Installation

### 🔍 Check if `dnsx` is installed correctly

```bash
dnsx
```

---

### 🏷️ Display dnsx version

```bash
dnsx -version
```

---

### ❓ Show help menu

```bash
dnsx -h
```

---

## 🚀 Why Use dnsx?

* ⚡ **High-performance DNS resolution**
* 🔁 Supports **custom resolver lists**
* 🧠 Ideal for **validating subdomains**
* 🤖 Integrates perfectly with:

  * Subfinder
  * Amass
  * Findomain
  * OneForAll

---

## ▶️ Running dnsx Queries

### 🔁 Reverse DNS Lookup (PTR Records)

#### 🔹 Single IP Lookup
```bash
echo "8.8.8.8" | dnsx -silent -resp-only -ptr
```

---

#### 🔹 Bulk Reverse Lookup from a File

Create a file with IP addresses:

```bash
vim ip-list.txt
```

Example `ip-list.txt`:

```text
8.8.8.8
8.8.4.4
64.6.64.6
1.1.1.1
```

Run bulk PTR lookup:

```bash
dnsx -l ip-list.txt -silent -resp-only -ptr
```

---

## 🌐 Scanning CIDR Ranges

* 🔍 **Scan a large CIDR block:**

```bash
echo "8.8.0.0/16" | dnsx -silent -resp-only -ptr
```

* 🔍 **Scan a medium CIDR block:**

```bash
echo "106.201.194.0/23" | dnsx -silent -resp-only -ptr
```

* 🔍 **Scan a small CIDR block:**

```bash
echo "82.196.42.196/28" | dnsx -silent -resp-only -ptr
```

* 🔍 **Scan an entire /24 subnet:**

```bash
echo "82.196.42.0/24" | dnsx -silent -resp-only -ptr
```

---

## 🧹 Filtering Dead Records

* ❌ **Filter out non-resolving (dead) domains:**

```bash
cat insta_domain.txt | dnsx
```

* ✅ **Show only responsive DNS records:**

```bash
cat insta_domain.txt | dnsx -resp
```

---

## 📥 Extracting A Records

- 🔍 **Extract A records from a domain list (show response):**
```bash
cat insta_domain.txt | dnsx -silent -a -resp
```

* 📄 **Extract A records from a file list:**

```bash
dnsx -l insta_domain.txt -silent -a -resp
```

* ✅ **Extract only IP addresses (response-only):**

```bash
cat insta_domain.txt | dnsx -silent -a -resp-only
```

```bash
dnsx -l insta_domain2.txt -silent -a -resp-only
```

* 🌐 **Example with another target (Airbnb):**

```bash
dnsx -l insta_domain.txt -silent -a -resp
```

---

## 🔎 Querying Multiple Record Types

* 🧩 **Query A, AAAA, NS, PTR, CNAME records together:**

```bash
dnsx -l insta_domain.txt -silent -a -aaaa -ns -ptr -resp -cname
```

```bash
dnsx -l tesla-all_domains.txt -silent -a -aaaa -ns -ptr -resp -cname
```

---

## 🔗 Extracting CNAME Records

* 📄 **Extract only CNAME responses from a file:**

```bash
dnsx -l insta_domain.txt -silent -cname -resp-only
```

* 🔍 **Extract CNAME records from stdin (with response):**

```bash
cat insta_domain.txt | dnsx -silent -cname -resp
```

* ✅ **Extract only CNAME targets (response-only):**

```bash
cat insta_domain.txt | dnsx -silent -cname -resp-only
```

* 🚫 **Filter CNAME records by response codes (ignore errors):**

```bash
cat insta_domain.txt | dnsx -silent -cname -rcode noerror,servfail,refused
```

```bash
dnsx -l tesla-all_domains.txt -silent -cname -rcode noerror,servfail,refused
```
