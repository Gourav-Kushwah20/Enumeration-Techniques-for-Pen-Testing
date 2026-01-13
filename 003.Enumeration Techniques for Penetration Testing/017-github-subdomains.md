# 🐙 github-subdomains

🔗 **GitHub Subdomains – Official Repository**  
https://github.com/gwen001/github-subdomains

**github-subdomains** is a reconnaissance tool developed by **gwen001** that searches public GitHub repositories for subdomains related to a given target domain.  
It is particularly useful during **asset discovery** and **security assessments**.

---

## 🎯 Use Cases

- 🔎 Discover subdomains exposed in public GitHub repositories  
- 🚨 Identify assets accidentally leaked by developers  
- 🗺️ Enhance reconnaissance and attack surface mapping  

---

## ⚙️ Installation

Install `github-subdomains` using Go:

```bash
go install github.com/gwen001/github-subdomains@latest
```

> ⚠️ Ensure that **Go** is installed and properly configured in your environment before running this command.

---

## 🚀 Usage

### 📖 Display Help

To view all available options and flags:

```bash
github-subdomains -h
```

---

### 🌐 Find Subdomains for a Target Domain

To search for subdomains related to a domain using GitHub API tokens:

```bash
github-subdomains -d example.com -t tokens.txt -o output.txt
```

* `-d` → Target domain
* `-t` → File containing GitHub API tokens
* `-o` → Output file to save discovered subdomains

---

## 🌍 Real-World Example (Tesla)

```bash
github-subdomains -d tesla.com -t github-tokens.txt -o tesla.com-github-subdomains-output.txt
```

> This command searches public GitHub repositories for any subdomains related to `tesla.com`.

---

## 📄 Example Output

Running the tool may produce results such as:
```bash
cat insta.com-github-subdomains-output.txt
```
```bash
cat insta.com-github-subdomains-output.txt | unfurl -u domain | wc -l
```

```text
www.instagram.com
instagram.com
api.instagram.com
i.instagram.com
m.instagram.com
blog.instagram.com
```

> These subdomains may have been exposed in configuration files, source code, or documentation hosted on GitHub.

---

## 🔑 Importance of Using GitHub Tokens

* 🚦 GitHub enforces strict rate limits on unauthenticated searches
* ⚡ To maximize results and reduce the likelihood of being blocked, use **personal access tokens** stored in a file (e.g., `tokens.txt`)

🔗 **GitHub token creation page:**
[https://github.com/settings/tokens](https://github.com/settings/tokens)

---

## 🛡️ Recommended Token Scopes

* `repo`
* `read:public_key`
* `read:org`

---

## ✅ Conclusion

**`github-subdomains`** is a powerful tool for identifying subdomains leaked in public GitHub repositories.
When combined with other enumeration techniques, it significantly improves **asset discovery** and **reconnaissance workflows**.

