# Git on Windows — Install & Verify

> Target audience: Students on **Windows 10/11**.
> Goal: Install **Git for Windows**, verify it, and do the essential first-time configuration. (Git for Windows includes **Git Bash** and **Git Credential Manager**.)

---

## Option A — Install with WinGet (fastest)

Open **PowerShell** or **Windows Terminal**, then run:

```powershell
winget install -e --id Git.Git
```

This installs the official **Git for Windows** package via Windows Package Manager. ([Git][1], [Microsoft Learn][2])

---

## Option B — Install with the official installer (GUI)

1. Download **Git for Windows**: [https://git-scm.com/download/win](https://git-scm.com/download/win)
2. Run the installer and accept the defaults (they’re fine for most students).

   * The installer provides **Git Bash** and offers **Git Credential Manager** for HTTPS auth to GitHub/Azure/etc. Leave these enabled. ([Git][3], [Microsoft Learn][4])

> FYI: Git for Windows includes a **Bash** emulation (Git Bash) so you can use Unix-style commands on Windows. ([gitforwindows.org][5])

---

## Verify

Open **Git Bash**, **PowerShell**, or **Command Prompt** and run:

```bash
git --version
where git   # on PowerShell/CMD
```

You should see `git version 2.x.y` and a path under `C:\Program Files\Git\...`. The Git website lists current releases. ([Git][6])

---

## Recommended: First-time Git configuration

Set your identity (used in every commit):

```bash
git config --global user.name  "Your Name"
git config --global user.email "you@example.com"
```

Set the default branch name for new repos (teams often use `main`):

```bash
git config --global init.defaultBranch main
```

Check your settings:

```bash
git config --global --list
```

These are the official first-time setup steps from the Git book; `init.defaultBranch` is supported and referenced in the docs. ([Git][7])

---

## (Optional) Use VS Code as the default Git editor

If you have VS Code installed:

```bash
git config --global core.editor "code --wait"
```

This opens commit messages and merges in VS Code and waits for you to finish. (See Git reference docs for config options.) ([Git][8])

---

## Notes & tips

* **Credential Manager (GCM):** The Git for Windows installer includes **Git Credential Manager**, which securely stores credentials and supports 2FA/OAuth for GitHub/Azure/etc. Keep it enabled during install. ([Microsoft Learn][4], [Git][9])
* **Git Bash vs WSL:** Git Bash is included with Git for Windows. If you need a full Linux environment, consider **WSL** and install Git inside the Linux distro. ([gitforwindows.org][5])
* **Updates:** With WinGet you can later run `winget upgrade Git.Git`. With the installer, download a new version from git-scm.com as needed. ([Microsoft Learn][10])

---

## References (Official)

* **Git for Windows — Download / Installing on Windows** (Git book & downloads). ([Git][3])
* **Git for Windows** (Git Bash included). ([gitforwindows.org][5])
* **WinGet — install command** (Windows Package Manager). ([Microsoft Learn][2])
* **First-time Git setup** (user.name, user.email, default branch). ([Git][7])
* **GCM included in Git for Windows**. ([Microsoft Learn][4])

---

### Scope

This page mirrors our macOS/Linux guides: **install (WinGet or GUI) → verify → first-time config**. It’s focused on classroom-friendly defaults and official documentation.

[1]: https://git-scm.com/downloads/win "Git - Downloading Package"
[2]: https://learn.microsoft.com/en-us/windows/package-manager/winget/install "install command (winget)"
[3]: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git "1.5 Getting Started - Installing Git"
[4]: https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git "Get started using Git on WSL - Windows"
[5]: https://gitforwindows.org/ "Git for Windows"
[6]: https://git-scm.com/downloads "Downloads"
[7]: https://git-scm.com/book/ms/v2/Getting-Started-First-Time-Git-Setup "1.6 Getting Started - First-Time Git Setup"
[8]: https://git-scm.com/doc "Documentation"
[9]: https://git-scm.com/book/en/v2/Git-Tools-Credential-Storage "7.14 Git Tools - Credential Storage"
[10]: https://learn.microsoft.com/en-us/windows/package-manager/winget/ "Use WinGet to install and manage applications"
