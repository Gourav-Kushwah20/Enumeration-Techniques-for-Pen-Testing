# 🔐 Username-to-Password-Wordlist

## 🧰 Username to Password Wordlist Generator (Python Script)

This Python script reads usernames from a file and generates a comprehensive password wordlist using:

- Original, lowercase, capitalized, uppercase variants
- Reversed versions
- Common patterns like `123`, `@123`, `2024`, etc.
- Case-sensitive output

---

## 📥 Input: users.txt

```bash
vim users.txt
````

```text
Harry
Elly
John
Kathy
Fred
Abby
Tim
```

---

## 🐍 Python Script: generate_passwords.py

```bash
vim generate_passwords.py
```

```python
#!/usr/bin/env python3
# generate_passwords.py

def generate_passwords(input_file, output_file):
    with open(input_file, 'r') as f:
        names = [line.strip() for line in f if line.strip()]

    with open(output_file, 'w') as f:
        for name in names:
            original = name
            lower = name.lower()
            capital = name.capitalize()
            upper = name.upper()
            reverse = name[::-1]
            reverse_lower = lower[::-1]
            reverse_capital = capital[::-1]

            patterns = []

            for base in [
                original,
                lower,
                capital,
                upper,
                reverse,
                reverse_lower,
                reverse_capital
            ]:
                patterns += [
                    base,
                    base + "123",
                    base + "1234",
                    base + "2024",
                    base + "@123",
                    base + "!",
                    base + "01",
                    base + "321",
                    base + "@",
                    base + "#",
                    "@" + base,
                    base + base[::-1]
                ]

            seen = set()
            unique_patterns = []

            for pwd in patterns:
                if pwd not in seen:
                    seen.add(pwd)
                    unique_patterns.append(pwd)

            for pwd in unique_patterns:
                f.write(pwd + "\n")

    print(f"[+] Generated wordlist with case-sensitive and reversed variants into: {output_file}")


if __name__ == "__main__":
    import sys

    if len(sys.argv) != 3:
        print("Usage: ./generate_passwords.py users.txt passwords.txt")
        sys.exit(1)

    input_file = sys.argv[1]
    output_file = sys.argv[2]

    generate_passwords(input_file, output_file)
```

## how to Make it Excutable

```bash
chmod +x generate_passwords.py
````

Then run it like this:

```bash
./generate_passwords.py users.txt passwords.txt
```

---

## ▶️ Usage

```bash
python3 generate_passwords.py users.txt passwords.txt
```

---

## 📦 Example Output for Harry

```text
Harry
Harry123
Harry1234
Harry2024
Harry@123
Harry!
Harry01
Harry321
Harry@
Harry#
Harry@Harry
HarryyrraH
harry
harry123
harry@123
YrraH
YrraH123
...
```

---

## ✅ Features

* Case-sensitive variants (Harry, harry, HARRY, etc.)
* Reversed names (yrraH, yrrah, etc.)
* Common patterns (123, 2024, @123, !)
* Duplicate-free output