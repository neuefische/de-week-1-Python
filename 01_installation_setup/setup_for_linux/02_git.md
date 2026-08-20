# Git on Ubuntu/Debian — Install & Verify

> Target audience: Students using **Ubuntu** or **Debian** (including WSL).
> Goal: Install Git from the official repositories and verify it. Quick first-time config included.

---

## 1) Check if Git is already installed

```bash
git --version
command -v git
```

Expected: output like `git version 2.x.y` and a path (typically `/usr/bin/git`).

---

## 2) Install (or update) Git via apt

```bash
sudo apt update
sudo apt install -y git
```

That installs the distro-supported Git (recommended for most students).

---

## 3) Verify

```bash
git --version
which git
```

---

## 4) (Recommended) One-time user configuration

Set your name and email for commits:

```bash
git config --global user.name  "Your Name"
git config --global user.email "you@example.com"
```

Set the default branch name for new repos (many teams use `main`):

```bash
git config --global init.defaultBranch main
```

Confirm your settings:

```bash
git config --global --list
```

---

## 5) (Optional) Install a newer Git than the distro provides

Only if you specifically need the latest Git features/bugfixes. For Ubuntu/Debian, the Git project publishes a PPA (Ubuntu) and backports. Follow the instructions on the official Git site:

* [https://git-scm.com/download/linux](https://git-scm.com/download/linux)

---

## Notes

* These steps intentionally **focus on Ubuntu/Debian** to keep the course consistent.
* If you’re in a minimal container/VM and `sudo` isn’t available, run the commands as `root` (omit `sudo`).

---

## References (Official)

* Git — Linux download & install: [https://git-scm.com/download/linux](https://git-scm.com/download/linux)
* Ubuntu Manpage: `git(1)`: [https://manpages.ubuntu.com/manpages/latest/en/man1/git.1.html](https://manpages.ubuntu.com/manpages/latest/en/man1/git.1.html)
* Debian package `git`: [https://packages.debian.org/search?keywords=git](https://packages.debian.org/search?keywords=git)
