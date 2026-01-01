# 🐚 Upgrading to a Full Interactive Shell (with zsh or bash)

## 🔧 Step 1: Spawn a TTY Shell

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
````

Or alternatives:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

```bash
python -c 'import pty; pty.spawn("/bin/sh")'
```

---

## ⏸️ Step 2: Background the Shell

```text
Ctrl + Z
```

---

## 🖥️ Step 3: Set the Correct Terminal Settings

Check your terminal size:

```bash
stty -a | head -n1 | cut -d ';' -f 2-3 | cut -b2- | sed 's/; /\n/'
```

Set terminal to raw mode and bring shell back to foreground:

```bash
stty raw -echo; fg
```

---

## 🔄 Step 4: Reset Terminal

Once back in the shell:

```bash
reset
```

If you lose the shell, try:

```text
Ctrl + D
````

---

## 🛠️ Step 5: Environment Tweaks

Set environment variables to improve compatibility:

```bash
export SHELL=/bin/bash
export TERM=xterm-256color
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
stty rows 39 columns 158   # Adjust as per your terminal
bash -i
```

---

## 🎨 Step 6: Prompt + Environment Customization

Optionally set a custom prompt and inspect environment:

```bash
export PS1='[\u@\h \W]\$ '
cat /etc/profile
cat /etc/bashrc
cat ~/.bash_profile
cat ~/.bashrc
cat ~/.bash_logout
env
set
```

---

## ⭐ Bonus: If you prefer zsh instead of bash

If `zsh` is available:

```bash
python -c 'import pty; pty.spawn("/bin/zsh")'
export SHELL=zsh
zsh -i
```

