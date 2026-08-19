# GitHub SSH on macOS — Configure & Verify

> Target audience: Students using **macOS** (Apple Silicon or Intel).
> Goal: Create a GitHub account, generate a secure SSH key, store its
> passphrase in the Apple Keychain, attach it to your GitHub account, and
> test the connection.

---

## 0) Create a GitHub account (skip if you have one)

1. Go to [github.com](https://github.com) → **Sign up**.
2. Enter an email, password, and username; verify your email; choose the
   **Free** plan — that's all you need for this course.

> Note: the email in `ssh-keygen -C "..."` below is only a **label** on the
> key — it does not have to match your GitHub account email. ([GitHub Docs][9])

---

## 1) Prerequisites

* **Git** installed → see the separate Git setup guide. `git` is not
  installed by uv; on a fresh Mac, running `git --version` triggers macOS to
  offer the **Xcode Command Line Tools** install — accept it (this also
  provides the `ssh` tools used below).
* **OpenSSH** — preinstalled on macOS. Check: `ssh -V`

---

## 2) Check for existing SSH keys

```bash
ls -al ~/.ssh
```

Look for pairs like `id_ed25519`/`id_ed25519.pub` or `id_rsa`/`id_rsa.pub`.
If you already have a key pair you want to reuse, skip to **Step 5** (add to
agent) or **Step 6** (add to GitHub). ([GitHub Docs][1])

---

## 3) Generate a new SSH key (recommended: Ed25519)

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

If your environment doesn't support Ed25519, fall back to RSA 4096:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Press **Enter** to accept the default file location, and add a passphrase
for security when prompted. ([GitHub Docs][2])

---

## 4) Configure SSH to use the Apple Keychain

On macOS Sierra 10.12.2 and later (all current Macs), create or edit
`~/.ssh/config` so keys load automatically and passphrases are stored in the
Keychain:

```bash
touch ~/.ssh/config
open ~/.ssh/config        # or use any editor
```

Add these lines and save:

```sshconfig
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

Keep permissions tight: `chmod 600 ~/.ssh/config`. ([GitHub Docs][2])

---

## 5) Add your private key to the agent & Keychain

```bash
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

Enter the passphrase from Step 3 — it is now stored in the Keychain, so you
won't be asked again after restarts.

> Use the macOS built-in `ssh-add` (as above), not one installed via
> Homebrew/MacPorts. If you get `illegal option -- apple-use-keychain`, call
> it explicitly: `/usr/bin/ssh-add --apple-use-keychain ~/.ssh/id_ed25519`.
> ([GitHub Docs][7])

---

## 6) Add your **public** key to your GitHub account

1. Copy the key to the clipboard:

```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

2. In GitHub: **Settings → SSH and GPG keys → New SSH key** → paste the key
   (Key type: *Authentication Key*) → **Add SSH key**. ([GitHub Docs][3])

---

## 7) Test the connection

```bash
ssh -T git@github.com
```

Expected first-time message (type **yes** to continue):
`Hi <your-username>! You've successfully authenticated, but GitHub does not provide shell access.` ([GitHub Docs][4])

---

## 8) (Optional) Use SSH for an existing repository

Switch a cloned repo from HTTPS to SSH:

```bash
cd /path/to/your/repo
git remote -v                   # see current remotes
git remote set-url origin git@github.com:OWNER/REPOSITORY.git
git remote -v                   # verify the new SSH URL
```

Official reference: **Managing remote repositories**. ([GitHub Docs][5])

---

## Troubleshooting

* **Permission denied (publickey)**: Ensure the **public** key is on GitHub
  and the **private** key is loaded (`ssh-add -l`). If empty after a
  restart, re-run Step 5 and check Step 4's config. ([GitHub Docs][6])
* **`illegal option -- apple-use-keychain`**: a non-Apple `ssh-add` is first
  on your `PATH` — use `/usr/bin/ssh-add ...` instead. ([GitHub Docs][7])
* **Passphrase asked every time**: the `UseKeychain yes` /
  `AddKeysToAgent yes` lines in `~/.ssh/config` (Step 4) are missing or
  misnamed.

---

## References (Official)

* **Creating an account on GitHub**: ([GitHub Docs][9])
* **Connecting to GitHub with SSH** (overview hub): ([GitHub Docs][8])
* **Check for existing keys**: ([GitHub Docs][1])
* **Generate a new SSH key & add to ssh-agent (macOS steps)**: ([GitHub Docs][2])
* **Add the key to your GitHub account**: ([GitHub Docs][3])
* **Test your SSH connection**: ([GitHub Docs][4])
* **Manage remote URLs (HTTPS ↔ SSH)**: ([GitHub Docs][5])

---

**Scope**: This page targets **macOS** with its built-in OpenSSH and
Keychain integration. If you manage multiple GitHub accounts or non-default
key names, extend the `Host` blocks in `~/.ssh/config`.

[1]: https://docs.github.com/articles/checking-for-existing-ssh-keys "Checking for existing SSH keys"
[2]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent "Generating a new SSH key and adding it to the ssh-agent"
[3]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account "Adding a new SSH key to your GitHub account"
[4]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection "Testing your SSH connection"
[5]: https://docs.github.com/en/get-started/git-basics/managing-remote-repositories "Managing remote repositories"
[6]: https://docs.github.com/en/authentication/troubleshooting-ssh "Troubleshooting SSH"
[7]: https://docs.github.com/en/authentication/troubleshooting-ssh/error-ssh-add-illegal-option----apple-use-keychain "Error: ssh-add: illegal option -- apple-use-keychain"
[8]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh "Connecting to GitHub with SSH"
[9]: https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github "Creating an account on GitHub"
