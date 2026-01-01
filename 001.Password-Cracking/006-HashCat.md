# 🧩 **Hashcat**

![Hashcat Logo](./img/Image-10.jpg)

---

## ⚙️ **Quick Help & Device Info**

### 🧰 Install Hashcat
```bash
apt install hashcat
```

### 📖 Show Full Help
```bash
hashcat -h
```

### 🔍 Filter Help Output
```bash 
hashcat -hh | grep -i "mysql"
```
```bash
hashcat -hh | grep -i "linux"
```
```bash
hashcat -hh | grep -i "unix"
```

### 🧠 List Detected OpenCL / CUDA Devices
```bash
hashcat -I
```

### 🎮 GPU Status
```bash
nvidia-smi
```

### ⏱️ Watch GPU Usage (refresh frequently)
```bash
watch -n 0.5 nvidia-smi
```

---

## 🧪 **Benchmarks**

### ⚡ Run Quick Benchmark
```bash
hashcat -b
```

### 🧩 Benchmark All Kernels
```bash
hashcat -b --benchmark-all
```

## 🧪 **Benchmark Command**

```bash
hashcat -b --benchmark-all --backend-devices 1
```

---

## 🧰 **Useful Utilities**

### 🔐 Show Example Hashes Shipped with Hashcat

```bash
hashcat --example-hashes
```

---

### 🧹 Show or Clear Potfile

- 👀 Show potfile
```bash
cat ~/.hashcat/hashcat.potfile
```
- 🧽 Remove potfile (start fresh)
```bash
rm -f ~/.hashcat/hashcat.potfile
```

---

### 💾 Sessions & Restore

- ▶️ Start with session name
```bash
hashcat --session=myrun -m 0 -a 0 hashes.txt wordlist.txt
```
- ⏪ Later restore
```bash
hashcat --session=myrun --restore
```

---

## 📘 **Basic Command Parts (Quick Reference)**

| 🧱 Component                     | 🧩 Option                 | 💬 Description                                                       |
| -------------------------------- | ------------------------- | -------------------------------------------------------------------- |
| 🔢 **Hash Mode (type)**          | `-m <mode>`               | e.g., `0 = MD5`                                                      |
| 🎯 **Attack Mode**               | `-a <attack>`             | `0 = straight`, `3 = mask`, `6 = wordlist+mask`, `7 = mask+wordlist` |
| 📄 **Output File**               | `-o <file>`               | Save cracked results                                                 |
| 🔍 **Show Cracked from Potfile** | `--show`                  | Display recovered hashes                                             |
| ⚙️ **Rules**                     | `-r rules/<file>`         | Apply rule-based transformations                                     |
| 💻 **Devices**                   | `--backend-devices <ids>` | Specify GPU/CPU devices                                              |
| 🧩 **Remove Cracked as Found**   | `--remove`                | Deletes cracked hashes automatically                                 |

---

## 🔐 **Brute-force (Mask) Examples**

### 🧾 **Create MD5 and Verify**

```bash
echo -n "1234" | md5sum
```

```bash
vim md5-hash.txt
```

🧩 **Output:**

```
81dc9bdb52d04dc20036dbd8313ed055
```

---

### 🔢 **Brute-force 4 Digits (MD5)**

```bash
hashcat -m 0 -a 3 md5-hash.txt ?d?d?d?d -o md5-1-output.txt
```

---

### 🔟 **10-digit Numeric Mask**

```bash
echo -n "5864792564" | md5sum
```

```bash
echo -n "5864792564" | md5sum > md5-hash-2.txt
```
- Remove Dash (-)
```bash
vim md5-hash-2.txt
```

```bash
hashcat -m 0 -a 3 md5-hash-2.txt ?d?d?d?d?d?d?d?d?d?d
```

---

## 🧩 Hashcat — Charset Placeholders & Attack Examples 🎯

## 🔣 Hashcat Charset Placeholders for Mask Attack

| Placeholder | Characters Included             | Description                     |                       |
| ----------- | ------------------------------- | ------------------------------- | --------------------- |
| `?l`        | `abcdefghijklmnopqrstuvwxyz`    | Lowercase letters (a–z)         |                       |
| `?u`        | `ABCDEFGHIJKLMNOPQRSTUVWXYZ`    | Uppercase letters (A–Z)         |                       |
| `?d`        | `0123456789`                    | Digits (0–9)                    |                       |
| `?h`        | `0123456789abcdef`              | Hex digits lowercase (0–9, a–f) |                       |
| `?H`        | `0123456789ABCDEF`              | Hex digits uppercase (0–9, A–F) |                       |
| `?s`        | `!"#$%&'()*+,-./:;<=>?@[\]^_\`{ | }~`                             | Special (punctuation) |
| `?a`        | Combination of `?l?u?d?s`       | All letters, digits, specials   |                       |
| `?b`        | `0x00 - 0xff`                   | All 256 possible bytes          |                       |

> ✅ **Tip:** combine tokens to build complex masks (e.g., `?u?l?l?d?s`).

---

### 🔒 Mixed mask example (digit + special + lower)

```bash
hashcat -m 0 -a 3 md5-hash.txt ?d?s?l?l?l
```

This tries: digit, special, lowercase, lowercase, lowercase.

---

## 📚 Dictionary (Straight) Attack Examples


* **Copy compressed file to another location and extract**

```bash
cp -v /usr/share/wordlists/rockyou.txt.gz rockyou.txt.gz
```

* **Unpack rockyou (Debian/Ubuntu path)**

```bash
gunzip /opt/rockyou.txt.gz
```

* **View contents of the wordlist**

```bash
cat /opt/rockyou.txt
```

### 🧾 Straight dictionary (MD5 + rockyou)

```bash
echo -n "##password##" | md5sum | cut -d ' ' -f 1
```
- 22bf5101f44980b9bfd51d15ee51fbba

- Copy and paste in `md5-hash.txt` file:
```bash
vim md5-hash.txt
```

```bash
hashcat -m 0 -a 0 md5-hash.txt rockyou.txt
```

### 🔐 Straight dictionary (SHA1)

```bash
echo -n "##password##" | sha1sum | cut -d ' ' -f 1 
```
```bash
echo -n "##password##" | sha1sum | cut -d ' ' -f 1 > sha1-hast.txt
```
```bash
cat sha1-hast.txt
```
- Straight Dictionary(SHA1)
```bash
hashcat -m 100 -a 0 sha1-hast.txt rockyou.txt
```
```bash
hashcat -m 100 -a 0 sha1-1.txt /usr/share/wordlists/rockyou.txt
```

- Apply Rules:
```bash
Double MD5 Hash:

echo -n "##password##" | md5sum |cut -d ' ' -f 1 | md5sum |cut -d ' ' -f 1

echo -n "##password##" | md5sum |cut -d ' ' -f 1 | md5sum |cut -d ' ' -f 1 > md5-2.txt