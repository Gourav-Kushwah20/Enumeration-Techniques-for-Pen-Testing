# 🔐 Offline Password Cracking

> **Offline password cracking** is an attack method where the attacker obtains one or more password hashes and attempts to recover the original plaintext passwords — without interacting with the authentication server. ⚠️

---

## ⚙️ How Offline Attacks Work

1. 🧠 The attacker acquires **hashed passwords** from a compromised system or leaked database.
2. 🔁 Since hashes are **non-reversible**, the attacker **guesses a password**, hashes it, and compares it against the stolen hash.
3. 🔍 This process repeats until a **match is found** or the **attacker gives up**.

---

## 🧩 Common Hashing Algorithms

### 🧮 MD (Message Digest) Family

* MD2
* MD4
* MD5
* MD6

### 🧠 SHA (Secure Hash Algorithm) Family

* SHA-1
* SHA-256
* SHA-512

### 💻 Windows Hashes

* LM (Lan Manager)
* NTLM (NT Lan Manager)

---

## 📊 Characteristics of Hash Algorithms

| 🔢 **Algorithm** | 📏 **Output Length** | 📝 **Notes**                      |
| ---------------- | -------------------- | --------------------------------- |
| MD5              | 128 bits             | ⚡ Fast, now considered insecure   |
| SHA1             | 160 bits             | 🔒 More secure than MD5 but weak  |
| SHA256           | 256 bits             | 🧩 Modern, secure hash            |
| SHA512           | 512 bits             | 🛡️ More secure, slower           |
| NTLM             | 128 bits             | 💼 Used in Windows authentication |

---

## 🧂 Salted Password Hashing

### 🔑 What is Salting?

**Salt** is random data added to passwords before hashing to prevent **rainbow table attacks** 🌈.

### ⚙️ How It Works

* 🧩 **Password + Salt:** Combines the password and salt, then hashes the result.
* 🧩 **Salt + Password:** Concatenates the salt before the password, then hashes.
* 🔄 This increases the **complexity** and **uniqueness** of each hash — even if passwords are identical! 🔐

---

## 🧪 Examples
Plain Text password: @rmour123 
| 🔢 **Hash Type**                  | 💻 **Example Output**                                                                                                              |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| MD5                               | `97491186f344929a010d093ada3daea`                                                                                                  |
| SHA1                              | `f37b240f8e516bc55d32f12d391221b6c03b2e8`                                                                                          |
| NTLM                              | `E41B0D19802C1FCD3B0DFF20D97090`                                                                                                   |
| Password + Salt (`123456 + salt`) | `91ff5ecbad84fbbf13b3561580106aac`                                                                                                 |
| Salt + Password (`salt + 123456`) | `9366223266b3dc5170a18036dac52ba`                                                                                                  |
| MD5(MD5(password))                | `19cfe260f714a9b82f4d544d1fab9d2`                                                                                                  |
| SHA512(MD5(password))             | `e312007ac0226abbc88bd9733fa9d35537c73c975a9686a2b87e360456c9ee5cb400b1db3484abb06648caa2c2b993054e7e676ed8d4d377610064aaaf816784` |

---

## 🐢 Slow Hashes and Custom Hashing

* ⏳ **Slow hashing algorithms** (e.g., `bcrypt`, `scrypt`) are designed to be **computationally expensive**, slowing down attackers.
* 🧠 **Custom hashing** may combine multiple algorithms and salts for added security.

---

## 🧰 Hash Identification Tools

* 🕵️ **`hash-identifier`** — Tool to identify hash type from its value.
* 🔍 **`hashid`** — Another tool for hash identification that supports many hash types.

---
## 💻 Example Usage

```bash
# 🕵️ Identify hash type using hash-identifier
hash-identifier '97491186f344929a010d093ada3daea'

# 🔍 Identify hash type using hashid
hashid -m '6885858486f31043e5839c735d99457f045affd0'
```

---

## 🛡️ Defense Against Offline Attacks

### ✅ Best Practices

* 🔒 Use **strong, slow hashing algorithms** (e.g., bcrypt, scrypt, Argon2) with **unique salts** 🧂
* 🔐 Enforce **complex passwords** to increase guessing difficulty 💪
* 🔁 **Regularly update** and **monitor** password storage schemes for vulnerabilities 🧠

---

# 🧠 Password Cracking Rack

![alt text](./img/image-9.png)

A **password cracking rack** refers to a **distributed system infrastructure** designed to efficiently perform large-scale password cracking operations 💥 by leveraging multiple **GPU/CPU machines**.

---

## ⚙️ How It Works

* 🖥️ Consists of **multiple high-performance machines** (often GPUs like *NVIDIA 3090, 1080 Ti*) working in parallel.
* 🔄 Tasks are **distributed** across the rack to maximize cracking speed.
* 🔐 Commonly used by **security teams** and **red/blue teams** for password recovery and auditing.
* ⚠️ Also used by **attackers** for large-scale offline password cracking.

---

## 🧰 Example: GoCrack Managed Cracking Tool

* 🧑‍💻 Developed by **FireEye’s ICE team**.
* 🌐 Provides a **web-based UI** to manage cracking tasks in real-time.
* ⚙️ **Automatically distributes** cracking tasks across all machines in the rack.
* 🔒 Features include **user access controls**, **task auditing**, and **shared engine files** for secure collaboration.
* 🧩 Supports various cracking methods and engine files like **dictionaries** and **mangling rules**.

---

## 💡 Benefits

* ✅ **Dramatically increases** password cracking throughput.
* ⚡ **Simplifies management** and automation of cracking campaigns.
* 👥 Enables **team-based collaboration** with fine-grained access controls.
* 🧾 Centralizes **logging and monitoring** for compliance and auditing.

---

## 🧪 Use Cases

* 🧰 Auditing **password strength** in corporate environments.
* 🔑 Recovering **lost passwords** from hash dumps.
* 🧱 Performing **security assessments** for compliance and research.

---
## 🧱 Hardware Commonly Used

To build or operate a **password cracking rack**, high-performance hardware is essential ⚙️💪

* 🖥️ **Multiple GPUs** with large VRAM (e.g., *NVIDIA GeForce 3090*, *1080 Ti*) for massive parallel computation.
* 🧮 **High-core count CPUs** (*Intel Xeon*, *AMD EPYC*) for managing distributed workloads efficiently.
* 💾 **Large RAM** and **fast SSD storage** for handling large **dictionary files** and **hash databases**.

---

### 💡 Example Use :

These setups are typically used in:

* 🔍 **Penetration testing** to identify weak credentials.
* 🧠 **Research and development** of new password cracking techniques and tools.
