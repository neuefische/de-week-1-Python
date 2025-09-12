# GitHub SSH on macOS — Configure & Verify

> Target audience: Students using **macOS** (Apple Silicon or Intel).
> Goal: Generate a secure SSH key, store the passphrase in **Keychain**, add the key to GitHub, and test the connection.

---

## 1) Check for existing SSH keys

```bash
ls -al ~/.ssh
```

Look for pairs like `id_ed25519`/`id_ed25519.pub` or `id_rsa`/`id_rsa.pub`. If you already have a usable key pair, skip to **Step 4** (Keychain + agent) or **Step 5** (add to GitHub). ([GitHub Docs][1])

---

## 2) Generate a new SSH key (recommended: Ed25519)

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

If your Mac can’t use Ed25519, fall back to RSA 4096:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Press **Enter** to accept the default save path, then set a passphrase when prompted. ([GitHub Docs][2])

---

## 3) Start the SSH agent

```bash
eval "$(ssh-agent -s)"
```

This launches the agent for the current shell session. ([GitHub Docs][2])

---

## 4) macOS Keychain + agent setup (one-time), then add your key

Create (or edit) `~/.ssh/config` with these lines so macOS **stores your passphrase in Keychain** and auto-loads your key:

```sshconfig
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

Now add your private key and store the passphrase in Keychain:

```bash
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
# If you created RSA instead:
# ssh-add --apple-use-keychain ~/.ssh/id_rsa
```

> Note: On older macOS versions the legacy flag was `-K`; modern docs use `--apple-use-keychain`. ([GitHub Docs][2])

---

## 5) Add your **public** key to your GitHub account

Copy the public key to your clipboard:

```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

Then in GitHub: **Settings → SSH and GPG keys → New SSH key** → paste → **Add SSH key**. ([GitHub Docs][3])

---

## 6) Test the connection

```bash
ssh -T git@github.com
```

On first connect, type **yes** to trust the host. Success looks like:

```
Hi <your-username>! You've successfully authenticated, but GitHub does not provide shell access.
```

(You’ll enter your key **passphrase** if you set one.) ([GitHub Docs][4])

---

## 7) (Optional) Switch an existing repo to SSH

```bash
cd /path/to/your/repo
git remote -v
git remote set-url origin git@github.com:OWNER/REPOSITORY.git
git remote -v
```

This changes `origin` from HTTPS to SSH. ([GitHub Docs][5])

---

## Troubleshooting

* **Permission denied (publickey)**
  Ensure the **public** key is on GitHub (Step 5) and the **private** key is loaded (`ssh-add -l`). See GitHub’s troubleshooting page. ([GitHub Docs][6])
* **Still prompted for passphrase every time**
  Recheck Step 4: `UseKeychain yes` in `~/.ssh/config` and you added the key with `ssh-add --apple-use-keychain`. ([GitHub Docs][2])

---

## References (Official)

* **Connecting to GitHub with SSH** (overview hub). ([GitHub Docs][7])
* **Generate a new SSH key & add to ssh-agent** (macOS Keychain instructions). ([GitHub Docs][2])
* **Add a new SSH key to your GitHub account** (includes `pbcopy`). ([GitHub Docs][3])
* **Test your SSH connection**. ([GitHub Docs][4])
* **Troubleshooting SSH / Permission denied (publickey)**. ([GitHub Docs][6])
* **Managing remote repositories** (switch to SSH URL). ([GitHub Docs][5])

---

### Scope

This page is macOS-specific and mirrors our Linux guide: check → generate → agent + Keychain → add to GitHub → test → optional repo switch.

[1]: https://docs.github.com/articles/checking-for-existing-ssh-keys "Checking for existing SSH keys"
[2]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent "Generating a new SSH key and adding it to the ssh-agent - GitHub Docs"
[3]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account "Adding a new SSH key to your GitHub account - GitHub Docs"
[4]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection "Testing your SSH connection - GitHub Docs"
[5]: https://docs.github.com/en/get-started/git-basics/managing-remote-repositories "Managing remote repositories"
[6]: https://docs.github.com/en/authentication/troubleshooting-ssh/error-permission-denied-publickey "Error: Permission denied (publickey)"
[7]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh "Connecting to GitHub with SSH"
