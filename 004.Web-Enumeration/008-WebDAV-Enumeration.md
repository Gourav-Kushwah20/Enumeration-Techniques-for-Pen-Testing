# WebDAV Enumeration

**WebDAV (Web Distributed Authoring and Versioning)** enumeration is the process of discovering accessible resources, capabilities, and potential vulnerabilities on a WebDAV-enabled server. This guide outlines techniques and tools used to interact with and test WebDAV services for security weaknesses.

> We create a new machine **centos9 mini** and configure ssh,ssh-server,http,httpd,vim ,yum install epel-release yum-utils mod_ssl,bash* and you needed.

[017-Apache Web Server Configuration/013-Webdav-with-Apache.md](<017-Apache Web Server Configuration/013-Webdav-with-Apache.md>)

```bash
nmap -v -sT -sV -A -O -p 80 192.168.1.25
```

```bash
dirsearch -u http://192.168.1.25/ -t 50
```

---

## WebDAV Enumeration Techniques

### 1. Identify WebDAV Support

Use the **OPTIONS** HTTP method via `curl` to check if WebDAV is enabled on the server.

```bash
curl -v -X OPTIONS http://192.168.1.25/webdav/
```

---

### Request

```http
OPTIONS /webdav/ HTTP/1.1
Host: 192.168.1.25
Cache-Control: max-age=0
Accept-Language: en-GB,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/138.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

## Response

```http
HTTP/1.1 200 OK
Date: Wed, 11 Feb 2026 16:30:03 GMT
Server: Apache/2.4.62 (CentOS Stream)
DAV: 1,2
DAV: <http://apache.org/dav/propset/fs/1>
MS-Author-Via: DAV
Allow: OPTIONS,GET,HEAD,POST,DELETE,TRACE,PROPFIND,PROPPATCH,COPY,MOVE,LOCK,UNLOCK
Content-Length: 0
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
Content-Type: httpd/unix-directory
```

---

### Look for WebDAV-related HTTP methods in the `Allow` header:

* `PUT`
* PROPFIND
* PROPPATCH
* MKCOL
* COPY
* MOVE
* LOCK
* UNLOCK

> Presence of these methods confirms **WebDAV support**.

---

### Example: Uploading a file using `PUT`

```bash
curl -v -X PUT -d "<?php phpinfo(); ?>" http://192.168.1.25/webdav/phpinfo.php
```

---

## 2. Use Nmap for Deeper Analysis

Run an Nmap script to enumerate HTTP methods:

```bash
nmap -p 80 --script=http-methods.nse --script-args http-methods.url-path='/webdav/' 192.168.1.25
```

### Full-feature scan with OS detection, service versioning, and aggressive scanning

```bash
nmap -v -sT -sV -A -O -p 80 --script=http-methods.nse --script-args http-methods.url-path='/webdav/' 192.168.1.25
```

---

## 3. Test With Davtest

```bash
apt install davtest
```

* `davtest` evaluates if file uploads or command execution are allowed.

```bash
davtest -url http://192.168.1.25/webdav/
```

### With authentication

```bash
davtest -url http://192.168.1.25/webdav/ -auth username:password
```

```bash
davtest -url http://192.168.1.25/test/ -auth dev:123
```

```bash
davtest -url http://192.168.1.25/webdav/ -auth dev:1234
```

### This tool checks for:

* Writable directories
* Upload execution
* File validation bypasses

---

## 4. Use A WebDAV Client (Cadaver)

`cadaver` is an interactive CLI client for managing WebDAV resources.

### Installation examples:

#### Debian/Ubuntu

```bash
apt install cadaver
```

#### RHEL/CentOS

```bash
yum install cadaver
```

### Connect to WebDAV server

```bash
cadaver http://192.168.1.25/webdav/
```

---

### In the shell:

```bash
ls              # List contents
put file.txt    # Upload file
get file.txt    # Download file
delete file.txt # Delete file
mkdir dir       # Create new directory
```

---

## 5. Brute Force Authentication (If Protected)

Use `hydra` to test for weak credentials:

```bash
hydra -l username -P /path/to/passwords.txt -s 80 -f target-ip http-head "/webdav"
```

```bash
hydra -L users.txt -P /usr/share/seclists/Passwords/darkweb2017-top1000.txt -s 80 -f 192.168.1.106 http-head "/webdav"
```

This is useful when encountering HTTP Basic/Digest authentication.

---

## 6. Manual Upload And Deletion (Test Writable Access)

### Test file uploads with `curl`: 192.168.1.25

```bash
curl -T test.txt http://target-ip/webdav/test.txt
```

### Test deletion:

```bash
curl -X DELETE http://target-ip/webdav/test.txt
```

### Authenticated uploads and deletions:

```bash
curl -u username:password -T test.txt http://target-ip/webdav/
```

```bash
curl -u username:password -X DELETE http://target-ip/webdav/test.txt
```

---

## 7. Check For Misconfigured Access Controls

### Indicators of weak access control:

* Anonymous upload or delete access
* File execution of `.php`, `.asp`, or `.aspx`
* No authentication prompt
* Directory browsing enabled

**Potential impact:** Remote Code Execution (RCE)

---

## Basic WebDAV Interaction Using Curl


## 1. Send OPTIONS Requests

```bash
curl -v -X OPTIONS http://192.168.1.40/webdav/
```

```bash
curl -i -k -X OPTIONS https://192.168.1.40/webdav/
```

---

## 2. Upload Files Using PUT

```bash
curl -T tesla_com_ips.txt http://192.168.1.30/webdav/tesla_com_ips.txt
```

```bash
curl -X PUT -d "hi" http://192.168.1.40/webdav/1.txt
```

```bash
curl -v -u dev:1234 -d "Test" -X PUT http://192.168.1.35/webdav/test.txt
```

---

## 3. Delete Files Using DELETE

```bash
curl -v -u dev:1234 -X DELETE http://192.168.1.35/webdav/test.txt
```

```bash
curl -u admin:123 -X DELETE http://192.168.1.106/webdav/phpinfo.php
```

---

## 4. Send Authenticated OPTIONS Requests

```bash
curl -v -u dev:123 -X OPTIONS http://192.168.1.40/test/
```

---

## Reconnaissance And Enumeration

### 1. Nmap With HTTP Methods Script

```bash
nmap -v -sT -sV -A -O -p 80 --script=http-methods.nse --script-args http-methods.url-path='/webdav/' 192.168.1.40
```

---

### 2. Brute Force Login With Hydra

```bash
hydra -l dev -P /opt/top-passwords-shortlist.txt -s 80 -f 192.168.1.30 http-head "/webdav"
```

---

### What To Look For

* Writable directories (test with upload)
* Executable file types supported
* Directory listing exposed
* Anonymous or unauthenticated access
* Weak, guessable login credentials
* Permissions allowing too much access (e.g., `chmod 777`)

---
