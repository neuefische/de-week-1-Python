# Bash on Windows — Install & Verify

> Target audience: Students on **Windows 10/11**.
> Goal: Get a reliable **Bash** shell on Windows. We recommend **WSL (Ubuntu)** for a real Linux environment; **Git Bash** is a lightweight alternative.

---

## Option A — WSL (Ubuntu) **recommended**

WSL lets you run a real Linux userland (Ubuntu, etc.) on Windows. Newer Windows builds install it with one command.

### 1) Install WSL (and Ubuntu)

Open **PowerShell as Administrator**, then run:

```powershell
wsl --install -d Ubuntu
```

* If you omit `-d Ubuntu`, WSL installs with the **default** Linux distro (usually Ubuntu). ([Microsoft Learn][1])
* If your Windows build doesn’t support `wsl --install`, use the **manual steps for older builds**. ([Microsoft Learn][2])
* You can list available distros with: `wsl --list --online`. Ubuntu also supports the new WSL distribution format. ([Microsoft Learn][1], [Ubuntu][3])

> The installer may enable required features and **reboot** your PC. After reboot, finish Ubuntu setup by creating a **username** and **password**.

### 2) (Optional) Ensure WSL 2

```powershell
wsl --set-default-version 2
wsl --status
wsl --update
```

WSL 2 is the default for new installs, but these commands confirm/update it. ([Microsoft Learn][1])

### 3) Open Bash and verify

Open **Ubuntu** from Start (or via **Windows Terminal**), then run:

```bash
bash --version
echo "$BASH_VERSION"
```

You should see GNU Bash (5.x). The WSL docs hub has more usage tips. ([Microsoft Learn][4])

> Tip: Install **Windows Terminal** for a great tabbed CLI experience:
>
> ```powershell
> winget install -e --id Microsoft.WindowsTerminal
> ```
>
> Then set your default profile to **Ubuntu** in Settings. ([Winget.run][5], [Microsoft Learn][6])

---

## Option B — Git Bash (lighter alternative)

**Git for Windows** ships a Bash emulation (“Git Bash”). It’s perfect for quick Bash usage without a full Linux environment.

### 1) Install Git for Windows

Using WinGet:

```powershell
winget install -e --id Git.Git
```

(Or download from the official Git site.) ([Microsoft Learn][7], [Git][8])

Git for Windows includes **Git Bash**. ([gitforwindows.org][9])

### 2) Launch & verify

Open **Git Bash** from Start, then:

```bash
bash --version
```

You’ll get the MSYS2-based Bash that ships with Git for Windows. ([gitforwindows.org][9])

---

## Notes & common gotchas

* If `wsl --install` fails, you may be on an **older Windows build**—follow the manual WSL steps. ([Microsoft Learn][2])
* For **multiple distros**, set defaults with:

  ```powershell
  wsl -l -v
  wsl --set-default <DistroName>
  ```

  ([Microsoft Learn][1])
* Use **Windows Terminal** to manage PowerShell, Command Prompt, Ubuntu (WSL), and Git Bash in tabs. ([Microsoft Learn][6])

---

## References (Official)

* **Install Linux on Windows with WSL** — Microsoft Learn (includes `wsl --install`, default/version commands). ([Microsoft Learn][1])
* **Manual WSL install (older Windows)** — Microsoft Learn. ([Microsoft Learn][2])
* **WSL docs hub** — Microsoft Learn. ([Microsoft Learn][4])
* **Ubuntu on WSL (new distro format)** — Canonical. ([Ubuntu][3])
* **Git for Windows (Git Bash)** — Official site & download. ([gitforwindows.org][9], [Git][8])
* **WinGet** — Microsoft Learn (install apps from CLI). ([Microsoft Learn][10])
* **Windows Terminal** — winget page & Microsoft Learn. ([Winget.run][5], [Microsoft Learn][6])

---

### Scope

This page keeps Windows setup simple: **WSL (Ubuntu)** for full Linux/Bash, or **Git Bash** for a lightweight shell—matching the consistency of your Linux and macOS guides.

[1]: https://learn.microsoft.com/en-us/windows/wsl/install "How to install Linux on Windows with WSL"
[2]: https://learn.microsoft.com/en-us/windows/wsl/install-manual "Manual installation steps for older versions of WSL"
[3]: https://ubuntu.com/blog/ubuntu-wsl-new-format-available "Ubuntu available in Microsoft's new WSL distribution format"
[4]: https://learn.microsoft.com/en-us/windows/wsl/ "Windows Subsystem for Linux Documentation"
[5]: https://winget.run/pkg/Microsoft/WindowsTerminal "Download and install Windows Terminal with winget"
[6]: https://learn.microsoft.com/en-us/windows/terminal/install "Install and get started setting up Windows Terminal"
[7]: https://learn.microsoft.com/en-us/windows/package-manager/winget/install "install command (winget)"
[8]: https://git-scm.com/downloads/win "Git - Downloading Package"
[9]: https://gitforwindows.org/ "Git for Windows"
[10]: https://learn.microsoft.com/en-us/windows/package-manager/winget/ "Use WinGet to install and manage applications"
