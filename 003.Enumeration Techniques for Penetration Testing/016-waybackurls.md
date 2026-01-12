# 🕰️ waybackurls

🔗 **waybackurls GitHub Repository**  
https://github.com/tomnomnom/waybackurls

**waybackurls** is a tool developed by **tomnomnom** that extracts URLs from the **Wayback Machine (Internet Archive)** for a given domain.  
It is widely used for **reconnaissance**, **subdomain enumeration**, and **discovering old or deprecated endpoints**.

---

## ⚙️ Installation

To install `waybackurls`, use the following command:

```bash
go install github.com/tomnomnom/waybackurls@latest
```

> ⚠️ Ensure your **Go environment** is properly set up before running this command.

---

## 🚀 Usage

### 🌐 Fetching URLs from the Wayback Machine

To retrieve historical URLs for a domain (e.g., `instagram.com`):

```bash
waybackurls instagram.com
```

### 💾 Save output to a file

```bash
waybackurls instagram.com > insta.com-waybackurls.txt
```

This will return a list of archived URLs for `instagram.com`.

---

## 🧩 Extracting Only Subdomains

Since `waybackurls` outputs **full URLs**, we use `unfurl` to extract only domain names:

```bash
waybackurls instagram.com | unfurl -u domains
```

---

## 📁 Saving the Output to a File

```bash
waybackurls instagram.com | unfurl -u domains > insta.com-domains.txt
```
