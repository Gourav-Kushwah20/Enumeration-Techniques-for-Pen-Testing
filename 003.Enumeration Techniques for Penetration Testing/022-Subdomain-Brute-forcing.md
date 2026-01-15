# 🔨 Subdomain Brute Forcing

**Subdomain brute forcing** is the process of discovering valid subdomains by brute-forcing DNS lookups against a target domain using a large list of potential subdomains.

---

## 🧩 Types of Subdomain Brute Forcing

### ➡️ Forward Lookup Brute Force
- Attempts to resolve a list of common subdomains to IP addresses using DNS.

### ⬅️ Reverse Lookup Brute Force
- Attempts to reverse-resolve IP addresses  
  *(e.g., from CIDR ranges or infrastructure)* back to subdomains.

---

## 📚 Wordlists for Subdomain Enumeration

### ✅ Recommended Wordlists
- **[SecLists](https://github.com/danielmiessler/SecLists)** (by Daniel Miessler)  
- **[Assetnote Wordlists](https://github.com/assetnote/wordlists)**  
- **[Jhaddix’s](https://github.com/jhaddix) `all.txt`**

---

## 🖥️ Local Setup (Kali / Parrot / Ubuntu)

Install SecLists:
```bash
apt install seclists
```

Navigate to DNS wordlists:

```bash
cd /usr/share/seclists/Discovery/DNS/
```

### 📂 Useful Files

```text
dns-Jhaddix.txt
```

- `subdomains-top1million-*`

---

## 📥 Download Wordlists

### 📄 Jhaddix `all.txt`

```bash
wget https://gist.githubusercontent.com/jhaddix/.../all.txt -O all.txt
````

```bash
cat all.txt > /opt/subdomain-wordlists/all-subdomain.txt
```

---

### 📚 Assetnote Wordlists

```bash
mkdir -p /opt/Wordlists && cd /opt/Wordlists
```

#### ⬇️ Download all from Assetnote (no index files)

```bash
wget -r --no-parent -R "index.html*" -e robots=off \
https://wordlists-cdn.assetnote.io/data/ -nH
```

---

## 🗂️ Organize Your Wordlists

```bash
# Find and copy all subdomain / DNS-related wordlists
mkdir -p /opt/subdomain-wordlists

for file in $(find . -iname "*subdomain*"); do
  cp -v "$file" /opt/subdomain-wordlists/
done

for file in $(find . -iname "*dns*"); do
  cp -v "$file" /opt/subdomain-wordlists/
done
```

---

## 🌐 DNS Resolvers

For tools like **massdns**, you’ll need good DNS resolvers.

### View default resolvers (SecLists)
```bash
cat /usr/share/seclists/Miscellaneous/dns-resolvers.txt
```

### Download recommended resolvers (massdns)

```bash
wget https://raw.githubusercontent.com/blechschmidt/massdns/master/lists/resolvers.txt
```

---

## 🛠️ Tools for Subdomain Brute Forcing

| Tool          | Description                                        | Link   |
| ------------- | -------------------------------------------------- | ------ |
| **Massdns**   | High-performance DNS stub resolver for brute force | [GitHub](https://github.com/blechschmidt/massdns) |
| **Findomain** | Fast subdomain discovery using multiple sources    | [GitHub](https://github.com/Findomain/Findomain) |
| **Amass**     | Enumeration, scraping, brute force, and mapping    | [GitHub](https://github.com/owasp-amass/amass) |
| **Sublist3r** | Fast passive subdomain enumeration                 | [GitHub](https://github.com/aboul3la/Sublist3r) |
| **Knockpy**   | Python-based subdomain brute-forcing tool          | [GitHub](https://github.com/guelfoweb/knock) |

---

## 🧠 Summary

* 📚 Use **high-quality wordlists** to increase brute-force effectiveness
* 🔀 Combine **passive and active** tools for better coverage
* ✅ Always verify results with **reliable resolvers** to avoid false positives
* 💥 Brute force remains one of the **most reliable methods** to find hidden subdomains when passive techniques fail

---

## Infosec Warrior Tools :
[Offensive Subdomains Wordlists Creator](https://github.com/InfoSecWarrior/Offensive-Pentesting-Scripts/tree/main/Subdomains-Wordlists)
