# 🔧 MassDNS Configuration – Step by Step

## 1️⃣ Install MassDNS

### 📌 On Linux (Ubuntu / Kali)

```bash
git clone https://github.com/blechschmidt/massdns.git
cd massdns
make
```

After build, the binary will be:

```bash
bin/massdns
```

(Optional) Move it to PATH:

```bash
sudo cp bin/massdns /usr/local/bin/
```

---

## 2️⃣ Prepare a Resolver List (VERY IMPORTANT)

MassDNS **requires a resolver file** (public DNS servers).

### 📄 Create `resolvers.txt`

```bash
nano resolvers.txt
```

Add reliable resolvers:

```text
8.8.8.8
8.8.4.4
1.1.1.1
1.0.0.1
9.9.9.9
208.67.222.222
208.67.220.220
```

💡 You can also download large resolver lists:

```bash
wget https://raw.githubusercontent.com/janmasarik/resolvers/master/resolvers.txt
```

---

## 3️⃣ Prepare Subdomain Wordlist

Create a file with subdomains:

📄 `subs.txt`

```text
www
mail
api
dev
test
admin
blog
```

Or use large wordlists:

```bash
SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

---

## 4️⃣ Create Target Domains File

📄 `domains.txt`

```text
example.com
```

---

## 5️⃣ Run MassDNS (Basic Command)

```bash
massdns -r resolvers.txt -t A -o S -w output.txt subs.txt
```

### 🔍 Flags Explained

| Flag   | Meaning               |
| ------ | --------------------- |
| `-r`   | Resolver list         |
| `-t A` | Query type (A record) |
| `-o S` | Simple output         |
| `-w`   | Write output to file  |

---

## 6️⃣ Subdomain Brute-Force (Real Use Case)

```bash
massdns -r resolvers.txt \
-t A \
-o S \
-w results.txt \
subs.txt
```

For **multiple domains**:

```bash
massdns -r resolvers.txt -t A -o S -w results.txt all_subdomains.txt
```

---

## 7️⃣ Filter Valid Subdomains

MassDNS output contains noise. Clean it:

```bash
cat results.txt | grep -E " A " | cut -d ' ' -f1 | sed 's/\.$//' | sort -u > valid.txt
```

📄 `valid.txt` → clean subdomains list

---

## 8️⃣ Recommended Performance Settings

⚡ Faster & safer scan:

```bash
massdns -r resolvers.txt \
-t A \
-o S \
--rate 10000 \
--retry REFUSED \
-w output.txt subs.txt
```

| Option    | Purpose               |
| --------- | --------------------- |
| `--rate`  | Requests per second   |
| `--retry` | Retry refused queries |

---

## 9️⃣ Common DNS Record Types

| Type    | Use                |
| ------- | ------------------ |
| `A`     | IPv4 address       |
| `AAAA`  | IPv6               |
| `CNAME` | Aliases            |
| `MX`    | Mail servers       |
| `TXT`   | SPF / verification |

Example:

```bash
massdns -r resolvers.txt -t CNAME -o S -w cname.txt subs.txt
```

---

## 🔐 Best Practices

✅ Always use **good resolvers**
✅ Keep request rate reasonable
✅ Combine with tools like:

* `subfinder`
* `amass`
* `dnsx`

❌ Do NOT use default system DNS
❌ Avoid scanning without permission

---

## 🧠 Typical Workflow (Bug Bounty / Pentest)

```text
subfinder → massdns → dnsx → httpx
```

---


