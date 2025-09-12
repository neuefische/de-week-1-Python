# GitHub SSH on Ubuntu/Debian — Configure & Verify

> Target audience: Students using **Ubuntu/Debian** (including WSL).
> Goal: Generate a secure SSH key, add it to the agent, attach it to your GitHub account, and test the connection.

---

## 1) Check for existing SSH keys

```bash
ls -al ~/.ssh
```

Look for pairs like `id_ed25519`/`id_ed25519.pub` or `id_rsa`/`id_rsa.pub`. If you already have a key pair you want to reuse, skip to **Step 4** (add to agent) or **Step 5** (add to GitHub). ([GitHub Docs][1])

---

## 2) Generate a new SSH key (recommended: Ed25519)

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

If your environment doesn’t support Ed25519, fall back to RSA 4096:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Press **Enter** to accept the default file location, and add a passphrase for security when prompted. ([GitHub Docs][2])

---

## 3) Start the SSH agent

```bash
eval "$(ssh-agent -s)"
```

This launches the agent in the background for the current session. ([GitHub Docs][2])

---

## 4) Add your private key to the agent

```bash
ssh-add ~/.ssh/id_ed25519
# or if you created RSA:
# ssh-add ~/.ssh/id_rsa
```

If prompted for a passphrase, enter the one you set in Step 2. ([GitHub Docs][2])

---

## 5) Add your **public** key to your GitHub account

1. Show the key and copy it (everything on one line, starting with `ssh-ed25519` or `ssh-rsa`):

```bash
cat ~/.ssh/id_ed25519.pub
```

2. In GitHub: **Settings → SSH and GPG keys → New SSH key** → paste the key → **Add SSH key**. ([GitHub Docs][3])

---

## 6) Test the connection

```bash
ssh -T git@github.com
```

Expected first-time message (type **yes** to continue):
`Hi <your-username>! You've successfully authenticated, but GitHub does not provide shell access.` ([GitHub Docs][4])

---

## 7) (Optional) Use SSH for an existing repository

Switch a cloned repo from HTTPS to SSH:

```bash
cd /path/to/your/repo
git remote -v                   # see current remotes
git remote set-url origin git@github.com:OWNER/REPOSITORY.git
git remote -v                   # verify the new SSH URL
```

Official reference: **Managing remote repositories**. ([GitHub Docs][5])

---

## 8) (Optional) Specify a key in `~/.ssh/config` (advanced)

If you manage multiple keys or non-default filenames, create/edit `~/.ssh/config`:

```sshconfig
Host github.com
  User git
  HostName github.com
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
```

This tells SSH which key to use when talking to GitHub. (Standard OpenSSH config; keep file permissions tight: `chmod 600 ~/.ssh/config`.)

---

## Troubleshooting

* **Permission denied (publickey)**: Ensure the **public** key is added to GitHub and the **private** key is loaded in the agent (`ssh-add -l`). See GitHub’s SSH troubleshooting guide. ([GitHub Docs][6])
* **“Agent admitted failure to sign”** on Linux: follow GitHub’s fix steps. ([GitHub Docs][7])

---

## References (Official)

* **Connecting to GitHub with SSH** (overview hub): ([GitHub Docs][8])
* **Check for existing keys**: ([GitHub Docs][1])
* **Generate a new SSH key & add to ssh-agent**: ([GitHub Docs][2])
* **Add the key to your GitHub account**: ([GitHub Docs][3])
* **Test your SSH connection**: ([GitHub Docs][4])
* **Manage remote URLs (HTTPS ↔ SSH)**: ([GitHub Docs][5])

---

**Scope**: This page targets **Ubuntu/Debian** and standard OpenSSH. If you’re on another distro or using a desktop keyring/agent, steps are similar but UI prompts may vary.

[1]: https://docs.github.com/articles/checking-for-existing-ssh-keys "Checking for existing SSH keys"
[2]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent "Generating a new SSH key and adding it to the ssh-agent"
[3]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account "Adding a new SSH key to your GitHub account"
[4]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection "Testing your SSH connection"
[5]: https://docs.github.com/en/get-started/git-basics/managing-remote-repositories "Managing remote repositories"
[6]: https://docs.github.com/en/authentication/troubleshooting-ssh "Troubleshooting SSH"
[7]: https://docs.github.com/enterprise-cloud%40latest/authentication/troubleshooting-ssh/error-agent-admitted-failure-to-sign "Error: Agent admitted failure to sign"
[8]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh "Connecting to GitHub with SSH"
