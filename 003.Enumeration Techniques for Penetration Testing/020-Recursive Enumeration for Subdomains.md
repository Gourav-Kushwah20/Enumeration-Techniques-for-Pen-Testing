# 🔁 Recursive Enumeration for Subdomains

**Recursive subdomain enumeration** is used to identify **commonly recurring base domains** and **subdomain patterns** from an existing list of subdomains.  
This technique helps uncover structural patterns and enables **deeper enumeration** by expanding known naming conventions.

---

## 🎯 Use Cases

- 🔍 Identify frequently used **root domains**
- 🧩 Detect **naming patterns** across subdomains
- 🌳 Discover **deeper subdomain levels** for further brute-forcing
- 🚀 Improve coverage in **reconnaissance workflows**

---

## 🛠️ Commands for Recursive Enumeration

### 📊 Extracting and Ranking Root Domains

This command extracts **root domains**  
(e.g. `example.com` from `api.sub.example.com`), counts their frequency, and displays the most common ones:

```bash
cat tesla.com-subdomain.txt | rev | cut -d '.' -f 3,2,1 | rev | sort | uniq -c | sort -nr | grep -v ' 1 ' | head -n 10 | sed -e 's/^[[:space:]]*//' | cut -d ' ' -f 2
```

---

## 🧠 Command Breakdown

* `cat tesla.com-subdomain.txt`
  → Reads the file containing discovered subdomains

* `rev`
  → Reverses each line to simplify extraction of domain components

* `cut -d '.' -f 3,2,1`
  → Extracts the last three domain components
  *(e.g. `example.com` from `api.sub.example.com`)*

* `rev`
  → Reverses the output back to normal domain format

* `sort`
  → Sorts domains alphabetically

* `uniq -c`
  → Counts occurrences of each domain

* `sort -nr`
  → Sorts results numerically (highest first)

* `grep -v ' 1 '`
  → Removes domains that appear only once

* `head -n 10`
  → Displays the top 10 most frequent root domains

* `sed -e 's/^[[:space:]]*//'`
  → Cleans leading spaces

* `cut -d ' ' -f 2`
  → Outputs only the domain name

---
## 🌊 Extracting Deeper Subdomain Levels

To identify **third- and fourth-level subdomains**  
(e.g. `dev.api.example.com`), use the following command:

```bash
cat tesla.com-subdomain.txt | rev | cut -d '.' -f 4,3,2,1 | rev | sort | uniq -c | sort -nr | grep -v ' 1 ' | head -n 10 | sed -e 's/^[[:space:]]*//' | cut -d ' ' -f 2
```

---

## 🔍 Key Difference

* `cut -d '.' -f 4,3,2,1`
  → Extracts the **last four domain components**, allowing identification of **deeper subdomain structures**

This is especially useful for discovering recurring environments such as:

* `dev`
* `staging`
* `test`
* `internal`

---

## 📄 Example Output

### 🌐 Root Domain Extraction

```text
tesla.com
energy.tesla.com
solar.tesla.com
api.tesla.com
```

### 🌳 Deeper Subdomain Extraction

```text
dev.api.tesla.com
staging.solar.tesla.com
test.energy.tesla.com
internal.api.tesla.com
```

---

## 🔑 Key Insight

Extracting deeper subdomain levels helps uncover **environment-based naming patterns**
that can be reused for **recursive brute-forcing and permutation attacks** during reconnaissance.

---

## ✅ Conclusion

Recursive subdomain enumeration helps you:

- 🔁 Identify **frequently used root and subdomain patterns**
- 🌳 Discover **multi-level subdomains** missed by standard enumeration
- 🧾 Generate **high-quality wordlists** for further brute-forcing
- 🚀 Strengthen overall **reconnaissance coverage**

By leveraging recursive techniques, you can move beyond surface-level discovery  
and uncover **deeper infrastructure patterns** that are often overlooked.
