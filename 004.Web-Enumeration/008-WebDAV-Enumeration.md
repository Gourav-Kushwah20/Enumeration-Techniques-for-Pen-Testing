# WebDAV Enumeration

**WebDAV (Web Distributed Authoring and Versioning)** enumeration is the process of discovering accessible resources, capabilities, and potential vulnerabilities on a WebDAV-enabled server. This guide outlines techniques and tools used to interact with and test WebDAV services for security weaknesses.

```bash
nmap -v -sT -sV -A -O -p 80 192.168.1.20
```

```bash
dirsearch -u http://192.168.1.20/ -t 50
```

---

## WebDAV Enumeration Techniques

### 1. Identify WebDAV Support

Use the **OPTIONS** HTTP method via `curl` to check if WebDAV is enabled on the server.

```bash
curl -v -X OPTIONS http://192.168.1.20/webdav/
```

---

### Request

```http
OPTIONS /webdav/ HTTP/1.1
Host: 192.168.1.36
Cache-Control: max-age=0
Accept-Language: en-GB,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
```

## Response

```http
HTTP/1.1 200 OK
Date: Thu, 24 Apr 2025 10:50:01 GMT
Server: Apache/2.4.62 (CentOS Stream) OpenSSL/3.2.2
DAV: 1,2
DAV: <http://apache.org/dav/propset/fs/1>
MS-Author-Via: DAV
Allow: OPTIONS, GET, HEAD, POST, DELETE, TRACE, PROPFIND, PROPPATCH, COPY, MOVE, LOCK, UNLOCK
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
curl -v -X PUT -d "<?php phpinfo(); ?>" http://192.168.1.36/webdav/phpinfo.php
```

---

## 2. Use Nmap for Deeper Analysis

Run an Nmap script to enumerate HTTP methods:

```bash
nmap -p 80 --script=http-methods.nse --script-args http-methods.url-path='/webdav/' 192.168.1.36
```

### Full-feature scan with OS detection, service versioning, and aggressive scanning

```bash
nmap -v -sT -sV -A -O -p 80 \
--script=http-methods.nse \
--script-args http-methods.url-path='/webdav/' \
192.168.1.36
```

---

## 3. Test With Davtest

```bash
apt install davtest
```

* `davtest` evaluates if file uploads or command execution are allowed.

```bash
davtest -url http://192.168.1.36/webdav/
```

### With authentication

```bash
davtest -url http://192.168.1.36/webdav/ -auth username:password
```

```bash
davtest -url http://192.168.1.40/test/ -auth dev:123
```

```bash
davtest -url http://192.168.1.35/webdav/ -auth dev:1234
```

### This tool checks for:

* Writable directories
* Upload execution
* File validation bypasses

---

## 4. Use a WebDAV Client (Cadaver)

`cadaver` is an interactive CLI client for managing WebDAV resources.

### Installation examples

