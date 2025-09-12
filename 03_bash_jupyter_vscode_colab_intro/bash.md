# Bash Introduction

> This handout gives you just enough Bash to be productive today, plus the **Bandit** game to level up quickly. Installation for every OS is already done — see the repo’s **`02_Installation_and_setup/`** folder for Linux, macOS, and Windows setup guides.

---

## 1) What is Bash (and why should you care)?

* **Bash** = *Bourne Again SHell* — a command-line interface and scripting language used on Linux/macOS and available on Windows (via **WSL** or **Git Bash**).
* Why it matters for data engineers:

  * Work faster than clicking around.
  * Automate repeatable tasks & data pipelines.
  * Operate servers, notebooks, containers, and CLIs used across the stack.

### Open a Bash terminal

* **Linux:** Terminal (often `Ctrl+Alt+T`)
* **macOS:** Terminal (default shell could be `zsh`; type `bash` to switch if you installed Bash 5)
* **Windows:** **Ubuntu (WSL)** or **Git Bash**
* If you don’t have Bash yet, see **`02_Installation_and_setup/`** in this repo for OS-specific instructions.

---

## 2) Core concepts, fast

### Prompt anatomy (typical)

```
user@host:~/path $ command arg1 arg2
```

* `command` = program or built-in
* `arg` = inputs
* `options` often start with `-` or `--` (e.g., `ls -l`)

### Filesystem moves

```bash
pwd                 # where am I?
ls -la              # list (including hidden)
cd myproject        # go into folder
cd ..               # up one
cd ~                # home
mkdir data logs     # make folders
touch notes.txt     # make empty file
```

### Looking at data

```bash
cat file.txt
less file.txt       # page through (q quits)
head -n 20 file.txt
tail -n 50 file.txt
wc -l file.txt      # line count
```

### Copy / move / delete

```bash
cp src.txt dst.txt
mv old.txt new.txt
rm file.txt
rm -r folder/       # recursive (careful!)
```

### Pipes & redirection (compose commands)

```bash
grep error app.log | sort | uniq -c | sort -nr
echo "hello" > out.txt       # overwrite
echo "again" >> out.txt      # append
ls nofile 2> errors.txt      # send errors to file
```

### Environment & PATH

```bash
echo "$PATH"         # where shells look for programs
export MY_VAR=42
echo "$MY_VAR"
printenv             # show all env vars
```

### Exit codes (for scripting & checks)

```bash
somecommand
echo $?              # 0 = success, non-zero = failure
```

---

## 3) Minimal script you’ll actually write today

```bash
# hello.sh
#!/usr/bin/env bash
set -euo pipefail
echo "Hello, $USER!"
```

```bash
chmod +x hello.sh
./hello.sh
```

* `set -euo pipefail` makes scripts safer (stop on errors, unset vars, and pipe failures).

---

## 4) Practice game: **Bandit** (OverTheWire)

A fun way to learn real CLI skills.

### Connect

1. Open a Bash-capable terminal (**Git Bash** / **WSL** / macOS / Linux).
2. SSH into Level 0:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

* If asked to trust the host, type `yes`.
* Password for **bandit0** is **`bandit0`**.

### Goal

* Each level hides the password for the next level somewhere in files/directories.
* You’ll use basic commands to locate, read, decode, or extract it.

### Starter toolbox (common Bandit moves)

* **Navigation & listing:** `ls -la`, `cd`, `pwd`
* **Reading files:** `cat`, `less`, `head`, `tail`
* **Hidden & weird filenames:** wrap in quotes or escape spaces:

  ```bash
  cat "spaces in this filename"
  ```
* **Find by name/size/perm:** `find . -name NAME`, `find . -size 1033c`, `find . -user bandit7 -group bandit6`
* **Search content:** `grep -R "needle" .`, `grep -E`, `grep -v` (exclude)
* **File type:** `file mystery.bin`
* **Hex & binary peeks:** `xxd`, `strings`
* **Decoding:** `base64 -d`, `tr`, `sort`, `uniq -c`, `cut`, `rev`
* **Archives:** `tar -xvf`, `gzip/gunzip`, `bzip2 -d`, `xz -d`
* **Permissions:** `chmod`, `sudo` (rare in Bandit)
* **Networking in later levels:** `nc`, `telnet` (read instructions per level)

### Tips for success

* Read each level page carefully; it tells you exactly what’s allowed and expected.
* Keep a scratchpad of commands you used and what worked.
* Prefer **pipes** to chain simple tools; don’t overthink it.
* When stuck: try `man <command>` or `<command> --help`.

**Link:** [https://overthewire.org/wargames/bandit/](https://overthewire.org/wargames/bandit/)

---

## 5) Quick reference tables

### Daily commands

| Command         | What it does           | Example                |
| --------------- | ---------------------- | ---------------------- |
| `pwd`           | Show current directory | `pwd`                  |
| `ls`            | List entries           | `ls -la`               |
| `cd`            | Change directory       | `cd ~/projects`        |
| `mkdir`         | Make directory         | `mkdir logs`           |
| `touch`         | New empty file         | `touch notes.txt`      |
| `cat` / `less`  | Print or page file     | `less data.csv`        |
| `cp` / `mv`     | Copy / move/rename     | `cp a b`, `mv a b`     |
| `rm`            | Remove file/dir        | `rm -r old/`           |
| `grep`          | Search by text         | `grep "error" app.log` |
| `head` / `tail` | First/last lines       | `tail -n 100 app.log`  |
| `find`          | Find files             | `find . -name "*.csv"` |

### Redirection & composition

| Operator | Meaning          | Example            |            |         |
| -------- | ---------------- | ------------------ | ---------- | ------- |
| `>`      | Overwrite output | `cmd > out.txt`    |            |         |
| `>>`     | Append output    | `cmd >> out.txt`   |            |         |
| `2>`     | Redirect errors  | `cmd 2> errs.txt`  |            |         |
| \`       | \`               | Pipe into next cmd | \`cat file | wc -l\` |

---
**Remember:** If anything doesn’t work on your machine, first re-check the relevant page under **`02_Installation_and_setup/`** in this repo for your OS.
