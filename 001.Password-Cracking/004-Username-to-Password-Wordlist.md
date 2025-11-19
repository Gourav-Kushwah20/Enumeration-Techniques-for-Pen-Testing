# 🔐 Username → Password Wordlist Generator (Python) — Cheat-Sheet

This small Python script reads usernames from a file and generates a comprehensive candidate **password** wordlist using common mangles:

- original, lowercase, Capitalized, UPPERCASE variants  
- reversed versions  
- common suffix/prefix patterns (`123`, `@123`, `2024`, etc.)  
- optional case-sensitive output (keeps variants distinct)  
- deduplicated output, written to a file
---

## 📥 Input: `users.txt` (example)
```bash
vim users.txt
```
```bash
Harry
Elly
John
Kathy
Fred
Abby
Tim
```

---
Here’s the **content from your image**, formatted cleanly in **Markdown**:

---

## 🐍 Python Script — `generate_passwords.py`

```python
vim generate_passwords.py
```

```python
#!/usr/bin/env python3
# generate_passwords.py
# Usage:
#   python3 generate_passwords.py users.txt passwords.txt

import sys
from pathlib import Path

def generate_passwords(input_file, output_file):
    with open(input_file, 'r', encoding='utf-8', errors='ignore') as f:
        names = [line.strip() for line in f if line.strip()]

    with open(output_file, 'w', encoding='utf-8') as f:
        for name in names:
            original = name
            lower = name.lower()
            capital = name.capitalize()
            upper = name.upper()
            reverse = name[::-1]
            reverse_lower = lower[::-1]
            reverse_capital = capital[::-1]

            patterns = []

            for base in [original, lower, capital, upper, reverse, reverse_lower, reverse_capital]:
                patterns += [
                    base,
                    base + "123",
                    base + "1234",
                    base + "2024",
                    base + "0123",
                    base + "!",
                    base + "01",
                    base + "321",
                    base + "@",
                    base + "#",
                    base + "@" + base,
                    base + base[::-1]
                ]

            # deduplicate while preserving order
            seen = set()
            unique_patterns = []
            for pwd in patterns:
                if pwd not in seen:
                    seen.add(pwd)
                    unique_patterns.append(pwd)

            # write each unique pattern to the output file
            for pwd in unique_patterns:
                f.write(pwd + '\n')

    print(f"[+] Generated wordlist with case-sensitive and reversed variants into: {output_file}")

if __name__ == "__main__":
    if len(sys.argv) != 3:
        print("Usage: ./generate_passwords.py users.txt passwords.txt")
        sys.exit(1)

    input_file = sys.argv[1]
    output_file = sys.argv[2]

    generate_passwords(input_file, output_file)
```
---

## ⚙️ How to Make It Executable

```bash
chmod +x generate_passwords.py
```

Then run it like this:

```bash
./generate_passwords.py users.txt passwords.txt
```

---

## 🧩 Usage

```bash
python3 generate_passwords.py users.txt passwords.txt
```

---

## 🧾 Example Output for `Harry`

*(Sample output will include variants like lowercase, uppercase, reversed, and with suffixes such as numbers or symbols.)*

```text
Harry
harry
HARRY
yarraH
harry123
harry2024
123harry
harry!
harry01
harry321
harry@
harry# 
@harry
harryyrrah
```
---

