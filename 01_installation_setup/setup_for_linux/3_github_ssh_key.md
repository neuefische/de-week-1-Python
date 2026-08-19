# GitHub SSH on Ubuntu/Debian — Configure & Verify

> Target audience: Students using **Ubuntu/Debian** (including WSL).
> Goal: Create a GitHub account, generate a secure SSH key, add it to the
> agent, attach it to your GitHub account, and test the connection.

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
  installed by uv and is missing on fresh Ubuntu/WSL installs:

```bash
sudo apt update && sudo apt install git -y
```

* **OpenSSH client** — preinstalled on Ubuntu/Debian. Check: `ssh -V`

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

## 4) Start the SSH agent

```bash
eval "$(ssh-agent -s)"
```

This launches the agent in the background **for the current session only** —
see Step 9 for auto-start. ([GitHub Docs][2])

---

## 5) Add your private key to the agent

```bash
ssh-add ~/.ssh/id_ed25519
# or if you created RSA:
# ssh-add ~/.ssh/id_rsa
```

If prompted for a passphrase, enter the one you set in Step 3. ([GitHub Docs][2])

---

## 6) Add your **public** key to your GitHub account

1. Show the key and copy it (everything on one line, starting with
   `ssh-ed25519` or `ssh-rsa`):

```bash
cat ~/.ssh/id_ed25519.pub
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

## 9) (Optional) Auto-start the agent & specify a key (advanced)

The agent from Step 4 dies when the terminal closes. To start it
automatically, add GitHub's official snippet to `~/.bashrc`:

```bash
env=~/.ssh/agent.env

agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }

agent_start () {
    (umask 077; ssh-agent >| "$env")
    . "$env" >| /dev/null ; }

agent_load_env

# agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2=agent not running
agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)

if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
    agent_start
    ssh-add
elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
    ssh-add
fi

unset env
```

If you manage multiple keys or non-default filenames, create/edit
`~/.ssh/config`:

```sshconfig
Host github.com
  User git
  HostName github.com
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
```

Keep permissions tight: `chmod 600 ~/.ssh/config`. ([GitHub Docs][10])

---

## Troubleshooting

* **Permission denied (publickey)**: Ensure the **public** key is added to
  GitHub and the **private** key is loaded in the agent (`ssh-add -l`).
  ([GitHub Docs][6])
* **Worked yesterday, "Permission denied" today**: the agent only lives per
  session — re-run Steps 4–5, or set up the auto-start snippet (Step 9).
* **"Agent admitted failure to sign"** on Linux: follow GitHub's fix steps.
  ([GitHub Docs][7])

---

## References (Official)

* **Creating an account on GitHub**: ([GitHub Docs][9])
* **Connecting to GitHub with SSH** (overview hub): ([GitHub Docs][8])
* **Check for existing keys**: ([GitHub Docs][1])
* **Generate a new SSH key & add to ssh-agent**: ([GitHub Docs][2])
* **Add the key to your GitHub account**: ([GitHub Docs][3])
* **Test your SSH connection**: ([GitHub Docs][4])
* **Manage remote URLs (HTTPS ↔ SSH)**: ([GitHub Docs][5])
* **Working with SSH key passphrases (auto-launch agent)**: ([GitHub Docs][10])

---

**Scope**: This page targets **Ubuntu/Debian** and standard OpenSSH. If
you're on another distro or using a desktop keyring/agent, steps are similar
but UI prompts may vary.

[1]: https://docs.github.com/articles/checking-for-existing-ssh-keys "Checking for existing SSH keys"
[2]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent "Generating a new SSH key and adding it to the ssh-agent"
[3]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account "Adding a new SSH key to your GitHub account"
[4]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection "Testing your SSH connection"
[5]: https://docs.github.com/en/get-started/git-basics/managing-remote-repositories "Managing remote repositories"
[6]: https://docs.github.com/en/authentication/troubleshooting-ssh "Troubleshooting SSH"
[7]: https://docs.github.com/en/authentication/troubleshooting-ssh/error-agent-admitted-failure-to-sign "Error: Agent admitted failure to sign"
[8]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh "Connecting to GitHub with SSH"
[9]: https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github "Creating an account on GitHub"
[10]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases "Working with SSH key passphrases"
