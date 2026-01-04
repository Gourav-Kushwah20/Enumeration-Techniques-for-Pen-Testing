# 🕵️ Passive Subdomain Enumeration

Passive subdomain enumeration involves gathering subdomain information **`without directly querying the target’s infrastructure`**. This reduces the chance of detection.

---

## 🔍 WHOIS Lookup

Used to gather information about the **registrant**, **name servers**, and **contact details**.

### 🔥 Command:

```bash
whois armourinfosec.com
```

### 🌐 Web Tools for search Domains:

* [**who.is**](https://who.is/whois)
* [**GoDaddy WHOIS**](https://www.godaddy.com/en-in/whois)
* [**Whoxy Reverse WHOIS**](https://www.whoxy.com/keyword/itgeeks)

---

## 🔄 Reverse WHOIS

Find all domains registered with the **same registrant or contact details**.

### 🌐 Web Tools:

* [**ViewDNS Reverse WHOIS**](https://viewdns.info/reversewhois/)
* [**ReverseWHOIS**](https://www.reversewhois.io/)


---

## 📊 Google Analytics Relationship

Use **Google Analytics IDs** to find related domains.
* [**Google Analytics**](https://analytics.google.com/analytics/web/provision/#/provision)


* [**BuildWith**](https://builtwith.com/relationships/tesla.com)

---



## 📜 Certificate Transparency (CT) Logs

* Collect subdomains from **SSL/TLS certificates**.

---

## 🌐 Web Tools

* [**crt.sh**](https://crt.sh/)
* [**censys.io**](https://search.censys.io/)
* **developers.facebook.com**
* **Google Transparency Report**
* [**sslmate certspotter**](https://sslmate.com/certspotter/)

---

## 🧪 Example using `crt.sh`

```bash
curl -s "https://crt.sh/?q=%.tesla.com&output=json" | jq -r '.[].name_value' | sed 's/\*\.//g' | sort -u
```
```bash
curl "https://crt.sh/?q=%.tesla.com&output=json" -o tesla.com.json
```
```bash
cat tesla.com.json | jq .
```
---

## 🧪 Example using `jq` and `unfurl`

```bash
cat tesla.com.json | jq -r '.[].name_value' | unfurl -u domains
```

---

## 🔍 Extract Subdomains from SAN (Subject Alternative Names)

* Extract **SAN data** from certificates.

---

## 🛠️ Example using Nmap

```bash
nmap --script targets-asn --script-args targets-asn.asn=24560
```

---

## 🐍 Python Script

```bash
python san_subdomain_enum.py google.com
```

---


## 🦠 VirusTotal

* Search for **subdomain relationships** in VirusTotal.

🔗 Example:


https://www.virustotal.com/gui/domain/www.tesla.com/relations


---

## 🔍 Google Dorks

Find subdomains using **advanced search operators**.

### 🔎 Examples:Search browser

```text
site:tesla.*
```
```bash
site:*tesla.*
```
```bash
site:tesla.com -www -shop -xapps -autodiscover
```

---

## 🌐 Shodan and Censys

* Find **exposed services and subdomains**.

## 🌐 Web Tools:

* [**censys**](https://search.censys.io/)
* [**shodan**](https://www.shodan.io/)
* [**dnsdumpster**](https://dnsdumpster.com/)

---

## 📡 Rapid7 Sonar Datasets

* Use **Sonar datasets** to find subdomains.
https://opendata.rapid7.com/

---

Here is the **Markdown transcription** of the content shown in the image:

---

## 🌪️ Chaos Project Discovery

* Discover subdomains using **ProjectDiscovery Chaos datasets**.

---

### 🧪 Example Script

```bash
vim chaos-data.sh
```
```bash
chmod +x chaos-data.sh
```
```bash
#!/bin/bash
Outputdir=/tmp/d1
mkdir -p $Outputdir/zipfiles
mkdir -p $Outputdir/txtfiles
wget "https://chaos-data.projectdiscovery.io/index.json" -O $Outputdir/index.json
grep "URL" $Outputdir/index.json | sed 's/.*"URL": "//;s/".*//' > $Outputdir/alltargets-zip.txt
wget -P $Outputdir/zipfiles -i $Outputdir/alltargets-zip.txt
unzip -d $Outputdir/txtfiles $Outputdir/zipfiles/*.zip
cat $Outputdir/txtfiles/*.txt > $Outputdir/alltargets.txt
rm -rf $Outputdir/zipfiles $Outputdir/txtfiles
```

* Another way to `Configure the API`
---

## 🐙 GitHub Subdomain Enumeration

* Use **GitHub** to extract subdomains.

🔗 **Tool:** [`github-subdomains`](https://github.com/gwen001/github-subdomains)

---

### 🧪 Example using `github-subdomains`

```bash
github-subdomains -d tesla.com -t <TOKEN>
```

---

## 🤖 Complete Automation Script

Example of a **full subdomain enumeration automation script** 🛠️:

```bash
#!/bin/bash

DOMAIN=$1

# Passive subdomain enumeration using Amass
amass enum -passive -d $DOMAIN > $DOMAIN-subdomains.txt

# Find subdomains using Subfinder
subfinder -d $DOMAIN >> $DOMAIN-subdomains.txt

# Find subdomains using Assetfinder
assetfinder --subs-only $DOMAIN >> $DOMAIN-subdomains.txt

# Remove duplicates and create final list
sort -u $DOMAIN-subdomains.txt > $DOMAIN-final.txt

# Display final output
cat $DOMAIN-final.txt
```