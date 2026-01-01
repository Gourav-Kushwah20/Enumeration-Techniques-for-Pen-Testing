<h1 align="center"> List of Common Ports and Protocols</h1>

# 🖥️ Application / Web Servers

| No. | Name                    | Port No.              | Protocol | Notes                                   |
|-----|-------------------------|-----------------------|----------|-----------------------------------------|
| 1   | HTTP                    | 80, 8080, 8081, 8000  | TCP      | Standard web traffic                    |
| 2   | HTTPS                   | 443, 8443, 4443       | TCP      | Secure web traffic                      |
| 3   | Tomcat Startup          | 8080                  | TCP      | Tomcat HTTP connector                   |
| 4   | Tomcat Startup (SSL)    | 8443                  | TCP      | Tomcat HTTPS connector                  |
| 5   | Tomcat Shutdown         | 8005                  | TCP      | Graceful shutdown port                  |
| 6   | Tomcat AJP Connector    | 8009                  | TCP      | Apache JServ Protocol                   |
| 7   | GlassFish HTTP          | 8080                  | TCP      | GlassFish HTTP service                  |
| 8   | GlassFish HTTPS         | 8181                  | TCP      | GlassFish HTTPS service                 |
| 9   | GlassFish Admin Server  | 4848                  | TCP      | Admin console                           |
| 10  | Jetty                   | 8080                  | TCP      | Lightweight Java server                 |
| 11  | Jonas Admin Console     | 9000                  | TCP      | Java EE administration                  |
| 12  | IHS Administration     | 8008                  | TCP      | IBM HTTP Server admin                   |
| 13  | JBoss Admin Console     | 8080                  | TCP      | JBoss management UI                     |
| 14  | WildFly Admin Console   | 9990                  | TCP      | WildFly management interface            |
| 15  | WebLogic Admin Console  | 7001                  | TCP      | Oracle WebLogic admin                   |
| 16  | WAS Admin Console (SSL) | 9043                  | TCP      | IBM WebSphere secure admin              |
| 17  | WAS Admin Console       | 9060                  | TCP      | IBM WebSphere admin                     |
| 18  | WAS JVM HTTP            | 9080                  | TCP      | Application traffic                     |
| 19  | WAS JVM HTTPS           | 9443                  | TCP      | Secure application traffic              |
| 20  | Alfresco Explorer       | 8080                  | TCP      | Content management UI                  |
| 21  | Apache Derby            | 1527                  | TCP      | Embedded database server                |
| 22  | OHS                     | 7777                  | TCP      | Oracle HTTP Server                     |
| 23  | OHS (SSL)               | 4443                  | TCP      | Secure Oracle HTTP Server               |
| 24  | Jenkins                 | 8080                  | TCP      | CI/CD automation server                 |

---

# 🧩 Panel

| No. | Name                                | Port No. | Protocol | Notes                                      |
|-----|-------------------------------------|----------|----------|--------------------------------------------|
| 1   | cPanel                              | 2082     | TCP      | Standard cPanel web interface               |
| 2   | cPanel - SSL                        | 2083     | TCP      | Secure cPanel access (HTTPS)                |
| 3   | WHM                                 | 2086     | TCP      | WebHost Manager administration              |
| 4   | WHM - SSL                           | 2087     | TCP      | Secure WHM administration                   |
| 5   | Webmail                             | 2095     | TCP      | Web-based email client                      |
| 6   | Webmail - SSL                       | 2096     | TCP      | Secure web-based email                      |
| 7   | Plesk Control Panel                 | 8880     | TCP      | Plesk admin interface                       |
| 8   | Plesk Control Panel - SSL           | 8443     | TCP      | Secure Plesk admin interface                |
| 9   | Plesk Linux Webmail                 | N/A*     | TCP      | Port assigned based on configuration        |
| 10  | Plesk Windows Webmail (SmarterMail) | 9998**   | TCP      | Windows-based webmail service               |
| 11  | Virtuozzo                           | 4643     | TCP      | VPS / container management panel            |
| 12  | DotNet Panel                        | 9001     | TCP      | Windows hosting control panel               |
| 13  | DotNet Panel Login                  | 80       | TCP      | Insecure HTTP login (not recommended)       |
| 14  | RDP (Remote Desktop Protocol)       | 4489     | TCP      | Alternative RDP port (default is 3389)      |
| 15  | SFTP Shared/Reseller Servers        | 2222     | TCP      | Secure file transfer for resellers          |
| 16  | Webdisk                             | 2077     | TCP      | Web-based file management                   |
| 17  | Webdisk - SSL                       | 2078     | TCP      | Secure web-based file management            |
| 18  | Plesk Control Panel                 | 8880     | TCP      | Duplicate entry (same as #7)                |
| 19  | Plesk Control Panel - SSL           | 8443     | TCP      | Duplicate entry (same as #8)                |
| 20  | Plesk Linux Webmail                 | N/A*     | TCP      | Duplicate entry (same as #9)                |
| 21  | Plesk Windows Webmail (SmarterMail) | 9998**   | TCP      | Duplicate entry (same as #10)               |
| 22  | Virtuozzo                           | 4643     | TCP      | Duplicate entry (same as #11)               |
| 23  | DotNet Panel                        | 9001     | TCP      | Duplicate entry (same as #12)               |
| 24  | DotNet Panel Login                  | 80       | TCP      | Duplicate entry (same as #13)               |
| 25  | RDP (Remote Desktop Protocol)       | 4489     | TCP      | Duplicate entry (same as #14)               |

---

# 📁 File Transfer

| No. | Name                        | Port No.                          | Protocol | Notes                                   |
|-----|-----------------------------|-----------------------------------|----------|-----------------------------------------|
| 1   | FTP                         | 21, 20, 2121                      | TCP      | Insecure file transfer                  |
| 2   | FTPS                        | 21, 20, 2121, 990, 989             | TCP      | FTP over SSL/TLS                        |
| 3   | RSCP                        | 514                               | TCP      | Remote copy protocol (legacy)           |
| 4   | OFTP                        | 6619                              | TCP/UDP  | Odette file transfer protocol           |
| 5   | CIFS / SMB / Samba          | 139, 445                          | TCP/UDP  | Network file sharing                    |
| 6   | SSH                         | 22, 2222                          | TCP      | Secure remote shell & file transfer     |
| 7   | NFS                         | 111, 2049, 4045, 1110              | TCP      | Network File System                     |
| 8   | TFTP                        | 69                                | UDP      | Trivial file transfer (no auth)         |
| 9   | HTTP                        | 80, 8080, 8081, 8000               | TCP      | File transfer over web                  |
| 10  | HTTPS                       | 443, 8443, 4443                   | TCP      | Secure file transfer over web           |
| 11  | Telnet                      | 23                                | TCP      | Insecure remote transfer                |
| 12  | Git                         | 9418                              | TCP      | Git native protocol                     |
| 13  | Apple Filing Protocol (AFP) | 548                               | TCP      | macOS file sharing                      |
| 14  | MooseFS                     | 9419, 9420, 9421, 9422, 9425       | TCP      | Distributed file system ports           |

---

# 🔐 Remote Connection

| No. | Name   | Port No.                     | Protocol | Notes                                  |
|-----|--------|------------------------------|----------|----------------------------------------|
| 1   | SSH    | 22, 2222                     | TCP      | Secure remote shell access              |
| 2   | Telnet | 23                           | TCP      | Insecure remote access (legacy)         |
| 3   | RDP    | 3389                         | TCP      | Windows remote desktop                  |
| 4   | VNC    | 5900, 5902, 5903, 6002, 6003 | TCP/UDP  | Remote graphical desktop sharing        |

---

# 📂 Directory Access

| No. | Name        | Port No. | Protocol | Notes                                   |
|-----|-------------|----------|----------|-----------------------------------------|
| 1   | LDAP        | 389      | TCP      | Directory authentication & queries      |
| 2   | LDAP (SSL)  | 636      | TCP      | Secure directory authentication (LDAPS) |

---

# 🗄️ Database / Datastore

| No. | Name        | Port No. | Protocol | Notes                                   |
|-----|-------------|----------|----------|-----------------------------------------|
| 1   | DB2         | 50000    | TCP      | IBM database server                     |
| 2   | Redis       | 6379     | TCP      | In-memory key-value store               |
| 3   | Oracle DB   | 1521     | TCP      | Oracle database listener                |
| 4   | MongoDB     | 27017    | TCP      | NoSQL document-oriented database        |
| 5   | MySQL       | 3306     | TCP      | Popular relational database             |
| 6   | MS SQL      | 1433     | TCP      | Microsoft SQL Server                    |
| 7   | Memcached   | 11211    | TCP      | Distributed memory caching              |
| 8   | MariaDB     | 3306     | TCP      | MySQL-compatible database               |
| 9   | PostgreSQL  | 5432     | TCP      | Advanced open-source SQL database       |

---

# 📬 Messaging / Transfer

| No. | Name                | Port No. | Protocol | Notes                                      |
|-----|---------------------|----------|----------|--------------------------------------------|
| 1   | MQ Listener         | 1414     | TCP/UDP  | IBM MQ message queue listener               |
| 2   | IBM Connect:Direct  | 1364     | TCP/UDP  | Managed file transfer protocol              |
| 3   | RabbitMQ Web UI     | 15672    | TCP/UDP  | RabbitMQ management web interface           |
| 4   | Tibco RV Daemon     | 7474     | TCP/UDP  | TIBCO Rendezvous messaging daemon           |
| 5   | GoToMyPC            | 8200     | TCP/UDP  | Remote access and support service           |

---

# ✉️ Mail Transfer

| No. | Name           | Port No. | Protocol | Notes                                      |
|-----|----------------|----------|----------|--------------------------------------------|
| 1   | POP3           | 110      | TCP/UDP  | Email retrieval (unencrypted)               |
| 2   | POP3 - SSL     | 995      | TCP/UDP  | Secure email retrieval                      |
| 3   | IMAP           | 143      | TCP/UDP  | Email synchronization                       |
| 4   | IMAP - SSL     | 993      | TCP/UDP  | Secure email synchronization                |
| 5   | SMTP           | 25       | TCP/UDP  | Email transfer between mail servers         |
| 6   | SMTP Alternate | 26       | TCP/UDP  | Alternate SMTP relay                        |
| 7   | SMTP (TLS)     | 587      | TCP/UDP  | Secure email submission (STARTTLS)          |
| 8   | SMTP - SSL     | 465      | TCP/UDP  | Secure SMTP over SSL                        |

---

# 🔐 VPN / Secure Tunneling

| Name        | Port No.  | Protocol | Notes                    |
|-------------|-----------|----------|--------------------------|
| OpenVPN     | 1194      | UDP/TCP  | SSL-based VPN            |
| IPsec / IKE | 500, 4500 | UDP      | VPN tunneling            |
| L2TP        | 1701      | UDP      | VPN tunneling            |
| PPTP        | 1723      | TCP      | Legacy VPN tunneling     |
| WireGuard   | 51820     | UDP      | Modern VPN tunneling     |

---

# 📞 VoIP / Conferencing

| Name  | Port No.       | Protocol | Notes                     |
|-------|----------------|----------|---------------------------|
| SIP   | 5060, 5061     | TCP/UDP  | VoIP signaling            |
| RTP   | 5004, 5005     | UDP      | Real-time media transport |
| H.323 | 1720           | TCP      | Video conferencing        |
| Jitsi | 5280, 5347     | TCP/UDP  | Open-source conferencing  |
| Zoom  | 8801–8810      | TCP      | Video conferencing        |

---

# 🧰 Miscellaneous

| Name            | Port No.        | Protocol | Notes                     |
|-----------------|-----------------|----------|---------------------------|
| SNMP            | 161, 162        | UDP      | Network monitoring        |
| NTP             | 123             | UDP      | Network time protocol     |
| Syslog          | 514             | UDP      | Logging                   |
| DNS             | 53              | UDP/TCP  | Domain name resolution    |
| mDNS            | 5353            | UDP      | Multicast DNS             |
| LPD             | 515             | TCP      | Line printer daemon       |
| Docker API      | 2375, 2376      | TCP      | Container management      |
| Kubernetes API  | 6443            | TCP      | Cluster management        |
| Consul          | 8500            | TCP      | Service discovery         |
