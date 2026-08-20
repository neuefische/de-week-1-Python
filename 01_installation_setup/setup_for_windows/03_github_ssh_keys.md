# GitHub SSH on Windows — Configure & Verify

> Target audience: Students on **Windows 10/11**.
> Goal: Create a GitHub account, generate an SSH key (Ed25519), add it to the
> **Windows OpenSSH agent**, attach the public key to GitHub, and test the
> connection.

---

## 0) Create a GitHub account (skip if you have one)

1. Go to [github.com](https://github.com) → **Sign up**.
2. Enter an email, password, and username; verify your email; choose the
   **Free** plan — that's all you need for this course.

> Note: the email in `ssh-keygen -C "..."` below is only a **label** on the
> key — it does not have to match your GitHub account email. ([GitHub Docs][9])

---

## 1) Prerequisites

* **Git for Windows** installed → see the separate Git setup guide (`git` is
  not installed by uv and does not come with Windows).
* **OpenSSH Client** — included in Windows 10/11. Check in PowerShell:

```powershell
ssh -V
```

If `ssh` isn't found, install it via **Settings → System → Optional features
→ View features → OpenSSH Client**. ([Microsoft Learn][1])

---

## 2) Check for existing SSH keys

```powershell
ls ~/.ssh
```

Look for pairs like `id_ed25519`/`id_ed25519.pub` or `id_rsa`/`id_rsa.pub`.
If you already have a key you want to use, skip to **Step 5**. ([GitHub Docs][2])

---

## 3) Generate a new SSH key (recommended: Ed25519)

```powershell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

If Ed25519 isn't supported on your system, fall back to RSA 4096:

```powershell
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Press **Enter** to accept the default file path, then set a passphrase when
prompted. ([GitHub Docs][3])

---

## 4) Start the SSH agent, add your key, point Git at it

**4a.** Open PowerShell **as Administrator** (right-click → *Run as
administrator*) and run these two lines:

```powershell
Get-Service ssh-agent | Set-Service -StartupType Automatic
Start-Service ssh-agent
```

**4b.** Back in a **normal** (non-admin) PowerShell:

```powershell
ssh-add $env:USERPROFILE\.ssh\id_ed25519
# or, if you created RSA:
# ssh-add $env:USERPROFILE\.ssh\id_rsa
```

Enter the passphrase from Step 3 when prompted.

> Use `$env:USERPROFILE\...` instead of `~/...` here — Windows PowerShell
> does not expand `~` in native commands.

**4c.** Tell Git to use Windows' OpenSSH (so it shares this agent):

```powershell
git config --global core.sshCommand "C:/Windows/System32/OpenSSH/ssh.exe"
```

Without this, Git uses its own bundled SSH and will ignore the agent —
asking for your passphrase on every push/pull. ([GitHub Docs][3])

---

## 5) Add your **public** key to your GitHub account

Copy the public key to the clipboard:

```powershell
Get-Content $env:USERPROFILE\.ssh\id_ed25519.pub | Set-Clipboard
```

Then in GitHub: **Settings → SSH and GPG keys → New SSH key** → paste
(Key type: *Authentication Key*) → **Add SSH key**. ([GitHub Docs][4])

---

## 6) Test the connection

```powershell
ssh -T git@github.com
```

On first connect, type **yes** to continue. Success looks like:

```
Hi <your-username>! You've successfully authenticated, but GitHub does not provide shell access.
```

(Enter your key **passphrase** if prompted.) ([GitHub Docs][2])

---

## 7) (Optional) Use SSH for an existing repository

Switch a cloned repo from HTTPS to SSH:

```powershell
cd path\to\your\repo
git remote -v
git remote set-url origin git@github.com:OWNER/REPOSITORY.git
git remote -v
```

([GitHub Docs][5])

---

## 8) (Optional) Specify a key in `~/.ssh/config` (advanced)

Useful if you maintain multiple keys:

```sshconfig
Host github.com
  User git
  HostName github.com
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
```

Save as `C:\Users\<you>\.ssh\config`. Inside this file `~` is fine — OpenSSH
expands it itself, independent of PowerShell. ([GitHub Docs][2])

---

## Troubleshooting

* **`Access denied` on `Set-Service`/`Start-Service`** → those two commands
  need an **Administrator** PowerShell (Step 4a); `ssh-add` itself must run
  in a normal window.
* **`Permission denied (publickey)`** → ensure the **public** key is on
  GitHub (Step 5) and the **private** key is loaded (`ssh-add -l`).
  ([GitHub Docs][6])
* **Passphrase asked on every git operation** → Step 4c is missing, or you
  loaded the key into Git Bash's agent instead of the Windows service. Pick
  one agent — this guide standardizes on the Windows OpenSSH service.
* **`ssh-add : No such file or directory`** → you used `~/...` in
  PowerShell; use `$env:USERPROFILE\.ssh\id_ed25519` (Step 4b).

---

## References (Official)

* **Creating an account on GitHub**. ([GitHub Docs][9])
* **Connecting to GitHub with SSH** — overview hub. ([GitHub Docs][2])
* **Generate a new SSH key & add to ssh-agent (Windows commands).** ([GitHub Docs][3])
* **Add a new SSH key to your GitHub account.** ([GitHub Docs][4])
* **Manage remote URLs (HTTPS ↔ SSH).** ([GitHub Docs][5])
* **Microsoft Learn: OpenSSH on Windows (install/optional features).** ([Microsoft Learn][1])

---

### Scope

This page mirrors the Linux/macOS guides: account → check → generate →
agent → GitHub → test. It standardizes on **Windows' built-in OpenSSH +
PowerShell**; the Git Bash agent approach is intentionally not mixed in.

[1]: https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse "Get started with OpenSSH for Windows"
[2]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh "Connecting to GitHub with SSH"
[3]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent "Generating a new SSH key and adding it to the ssh-agent"
[4]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account "Adding a new SSH key to your GitHub account"
[5]: https://docs.github.com/en/get-started/git-basics/managing-remote-repositories "Managing remote repositories"
[6]: https://docs.github.com/en/authentication/troubleshooting-ssh "Troubleshooting SSH"
[9]: https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github "Creating an account on GitHub"
