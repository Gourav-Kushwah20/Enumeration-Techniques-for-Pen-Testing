# 🔎 Sublist3r – Subdomain Enumeration Tool

**Sublist3r** is a Python-based tool designed to enumerate subdomains of websites using **OSINT (Open Source Intelligence)**.  
It gathers subdomains using search engines like **Google, Yahoo, Bing, Baidu**, and more.

---

## 🛠️ Installation

Clone the Sublist3r GitHub repository and install the dependencies:

```bash
git clone https://github.com/aboul3la/Sublist3r.git
````

Navigate into the tool’s directory:

```bash
cd Sublist3r/
```

Install required Python packages:

```bash
pip install -r requirements.txt
```

> ⚠️ **Note (Kali / Parrot / PEP 668 users):**
> If you get an `externally-managed-environment` error, use:
>
> ```bash
> python3 -m venv venv
> source venv/bin/activate
> pip install -r requirements.txt
> ```

---

## ❓ Help Menu

To view help and usage instructions:

```bash
python sublist3r.py -h
```

---

## 🚀 Basic Usage

### 1️⃣ Enumerate Subdomains for a Target

```bash
sublist3r -d instagram.com 
```

This command runs subdomain enumeration on the target domain **tesla.com** using passive OSINT sources.

---

### 🔓 Enable Bruteforce Mode

```bash
sublist3r -d instagram.com -b
```

> This enables **bruteforce mode** in addition to using search engines.

> It can be **more thorough**, but is usually **slower**.

---

## ⚙️ Additional Useful Options

| Option         | Description                                    |
| -------------- | ---------------------------------------------- |
| `-d`           | Target domain to enumerate                     |
| `-b`           | Enable bruteforce mode                         |
| `-t`           | Number of threads to use (default: 10)         |
| `-v`           | Enable verbose output                          |
| `-o`           | Output file to save the discovered subdomains  |
| `-p`           | Scan discovered subdomains for open ports      |
| `--enable-dns` | Enable DNS resolution of discovered subdomains |

---

## 💾 Example: Save Output and Enable DNS Resolution

```bash
python sublist3r.py -d tesla.com -o tesla_subs.txt --enable-dns
```

This command:

* Enumerates subdomains for **tesla.com**
* Saves results to `tesla_subs.txt`
* Resolves discovered subdomains via DNS

---

## 💡 Tips

* **Sublist3r** is ideal for **quick, passive reconnaissance**.
* Combine it with tools like **Amass**, **Findomain**, or **MassDNS** for deeper enumeration.
* Some search engines may **rate-limit or block aggressive scanning** — use with caution and within scope.


