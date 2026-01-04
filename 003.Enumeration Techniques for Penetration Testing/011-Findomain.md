# 🔎 Findomain

**[Findomain](https://github.com/Findomain/Findomain)** is a **fast and powerful subdomain enumeration tool** designed for security professionals 🛡️.

```bash
apt install findomain
````

---

## ⬇️ Downloading Findomain

To download the **latest Findomain release**, visit the **releases page** or use the command below 📦:

```bash
curl -LO https://github.com/Findomain/Findomain/releases/download/8.2.1/findomain-linux.zip
```

---

## 📂 Extracting the Archive 

Once the file is downloaded, extract it using `unzip` 🗜️:

```bash
unzip findomain-linux.zip
```

---

## ⚙️ Making the Binary Executable

Grant executable permissions to the `findomain` binary 🔑:

```bash
chmod +x findomain
```

---

## 🚚 Moving Findomain to a System Directory

Move the binary to `/usr/local/bin/` so it can be accessed globally 🌍:

```bash
cp -vr findomain /usr/local/bin
```

---

## 🧹 Stripping Debugging Symbols

(Optional) Reduce binary size and remove debugging symbols 🧽:

```bash
strip -s /usr/local/bin/findomain
```
---

## ✅ Verifying Installation

- 🔍 **Check if Findomain is installed correctly by running:**
```bash
findomain --help
````

> 📘 This command displays the help menu, listing all available options.

---

## 🚀 Running Findomain for Subdomain Enumeration

* 🌐 **Find subdomains of a target domain and save results to a file:**

```bash
findomain -t instagram.com -u output.txt
```

---

## 📌 Additional Usage Examples

### 1️⃣ Output results to the console (no file)

```bash
findomain -t instagram.com
```

---

### 2️⃣ Use multiple target domains from a file

📄 *(example: `domains.txt`)*

```bash
findomain -f domains.txt -u results.txt
```

---

### 3️⃣ Use Findomain with an API key (if configured)

🔑 *(improves results & speed)*

```bash
findomain -t instagram.com --api-key YOUR_API_KEY
```

---

## 📚 Notes & Tips

* ⚡ Findomain is **very fast** compared to many other tools
* 🕵️ Mostly **passive**, safe for recon & bug bounty
* 🔄 Combine with **Subfinder / Amass** for better coverage
* 📈 Use API keys to unlock **premium data sources**

📖 For more advanced options, refer to the **official documentation**.


---


### 🚀 Why use Findomain?

* ⚡ Extremely fast enumeration
* 🔍 Passive subdomain discovery
* 🐞 Great for bug bounty & recon
* 🔗 Integrates well with recon pipelines


