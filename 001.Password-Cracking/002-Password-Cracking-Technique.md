# Password-Cracking Techniques 🔑🕵️‍♂️

Offline and online password cracking are two distinct approaches attackers use to gain unauthorized access by discovering passwords.

---

## Offline Password Cracking 🖥️🔓

* 📥 **Involves** obtaining encrypted password hashes from a compromised system or database.
* ⚙️ **Attackers work locally** on these password hashes using powerful hardware (e.g., GPUs) and specialized tools (Hashcat, John the Ripper).
* ⚡ **High speed:** without interacting with the target system, attackers can try billions of guesses rapidly without triggering alerts or lockouts.
* 🔐 **Requires** prior access to password hash files (credential dumping, data breaches).
* ❗ **Effective** against weak hashing algorithms or unsalted hashes.
* 🕵️‍♀️ **Used by** both attackers and forensic investigators to crack passwords covertly.

---

## Online Password Cracking 🌐🚨

* ⏱️ **Happens in real-time** by attempting to authenticate directly on the live system (website login, application, remote access).
* 🤖 **Attackers try guessing** passwords by sending login requests manually or via automated bots.
* 🛑 **Limited by** network speed, rate-limiting, account lockouts, and monitoring (which can detect/block many attempts).
* 🔁 **Common techniques:** brute force, credential stuffing, password spraying.
* 👀 **Easier to detect** due to authentication attempts logged by servers.
* 🔍 **Often used when** password hashes are not available to the attacker.

---

# Compare offline vs online password cracking techniques

Here is a focused comparison of offline vs online password cracking techniques:

| **Aspect**             | **Offline Password Cracking**                                      | **Online Password Cracking**                                     |
| ---------------------- | ------------------------------------------------------------------ | ---------------------------------------------------------------- |
| **Attack Environment** | Password hashes obtained and cracked locally on attacker’s machine | Attacks target live authentication systems over a network        |
| **Speed**              | Very fast – uses high-performance hardware (GPUs, ASICs)           | Slower due to network latency, server response times, and limits |
| **Detection**          | Hard to detect, no direct interaction with the target system       | Easier to detect due to multiple failed login attempts           |
| **Rate Limiting**      | Not limited by server, can try billions of guesses                 | Throttled by server controls like account lockouts and CAPTCHAs  |
| **Access Needed**      | Hashes from databases, memory dumps, or breach data                | Valid access point for login interface                           |
| **Tools Used**         | Hashcat, John the Ripper, Rainbow tables                           | Automated scripts, bots, credential stuffing tools               |
| **Attack Vector**      | Focus on crackable hashes, weak or reused passwords                | Direct password guessing, credential reuse, social engineering   |
| **Success Likelihood** | Depends on hash strength, salting, and offline resources           | Limited by effective monitoring and account lockout policies     |
| **Use Scenario**       | After compromise or breach to recover passwords                    | Reconnaissance or direct brute force attacks in real-time        |

---

**Summary:**
Offline cracking offers speed and stealth but requires hash access, while online cracking is slower and noisy but requires live system access. Both exploit weak passwords, but mitigation strategies differ—focusing on hashing strength for offline attacks and monitoring/rate limiting for online attacks.

---
