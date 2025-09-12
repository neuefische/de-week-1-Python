# GitHub SSH on Windows — Configure & Verify

> Target audience: Students on **Windows 10/11**.
> Goal: Generate an SSH key (Ed25519), add it to the **Windows OpenSSH agent**, attach the public key to GitHub, and test the connection.

---

## 1) Prerequisite: OpenSSH Client

Windows 10/11 normally includes **OpenSSH Client**. If `ssh` isn’t found, install it via **Settings → System → Optional features → Add a feature → OpenSSH Client**. ([Microsoft Learn][1])

---

## 2) Check for existing SSH keys

Open **PowerShell** (or **Git Bash**) and list keys:

```powershell
ls ~/.ssh
```

Look for pairs like `id_ed25519`/`id_ed25519.pub` or `id_rsa`/`id_rsa.pub`. If you already have a key you want to use, skip to **Step 5** (add to GitHub). ([GitHub Docs][2])

---

## 3) Generate a new SSH key (recommended: Ed25519)

```powershell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

If Ed25519 isn’t supported on your system, fall back to RSA 4096:

```powershell
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Press **Enter** to accept the default file path, then set a passphrase when prompted. ([GitHub Docs][3])

---

## 4) Start the SSH agent and add your key

Start and enable the **OpenSSH Authentication Agent** service, then add your private key:

```powershell
Get-Service ssh-agent | Set-Service -StartupType Automatic
Start-Service ssh-agent
ssh-add ~/.ssh/id_ed25519
# or, if you created RSA:
# ssh-add ~/.ssh/id_rsa
```

You’ll be prompted for the key’s passphrase (if set). ([GitHub Docs][3])

---

## 5) Add your **public** key to your GitHub account

Copy the public key to the clipboard:

```powershell
Get-Content ~/.ssh/id_ed25519.pub | Set-Clipboard
# (Git Bash alternative):  cat ~/.ssh/id_ed25519.pub | clip
```

Then in GitHub: **Settings → SSH and GPG keys → New SSH key** → paste → **Add SSH key**. ([GitHub Docs][4])

---

## 6) Test the connection

```powershell
ssh -T git@github.com
```

On first connect, type **yes** to continue. A successful message looks like:

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

(See GitHub’s SSH overview/“Managing remote repositories” for details.) ([GitHub Docs][2])

---

## 8) (Optional) Specify a key in `~/.ssh/config` (advanced)

Useful if you maintain multiple keys:

```
Host github.com
  User git
  HostName github.com
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
```

Save as `C:\Users\<you>\.ssh\config`. OpenSSH on Windows uses the same format as Linux/macOS. ([GitHub Docs][2])

---

## Troubleshooting

* **`Permission denied (publickey)`**
  Ensure the **public** key is added on GitHub (Step 5) and the **private** key is loaded (`ssh-add -l`). See GitHub’s SSH docs for more tips. ([GitHub Docs][2])
* **`ssh` not found / agent not running**
  Revisit **Step 1** to install OpenSSH Client; in **Step 4**, confirm the `ssh-agent` service is **Running** and **Automatic**. ([Microsoft Learn][1])

---

## References (Official)

* **Connecting to GitHub with SSH** — overview hub (check → generate keys → add to account → test). ([GitHub Docs][2])
* **Generate a new SSH key & add to ssh-agent (Windows commands).** ([GitHub Docs][3])
* **Add a new SSH key to your GitHub account.** ([GitHub Docs][4])
* **Microsoft Learn: OpenSSH on Windows (install/optional features).** ([Microsoft Learn][1])

---

### Scope

This page mirrors our Linux/macOS guides: check → generate → agent → add to GitHub → test. It uses **built-in OpenSSH on Windows** or **Git Bash** commands where equivalent.

[1]: https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse "Get started with OpenSSH for Windows"
[2]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh "Connecting to GitHub with SSH"
[3]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent "Generating a new SSH key and adding it to the ssh-agent"
[4]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account "Adding a new SSH key to your GitHub account"
