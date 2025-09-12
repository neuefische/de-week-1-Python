# VS Code on Ubuntu/Debian — Install & Verify

> Target audience: Students using **Ubuntu/Debian** (including WSL).
> Goal: Install **Visual Studio Code**, verify it, and open a folder from the terminal.

---

## Option A — Install via `.deb` (simple)

1. **Download** the Debian/Ubuntu package from the official site:
   [https://code.visualstudio.com/download](https://code.visualstudio.com/download) ([Visual Studio Code][1])

2. **Install** it from your `Downloads` folder:

```bash
sudo apt update
sudo apt install -y wget gpg   # prerequisites if missing
cd ~/Downloads
ls                             # find the downloaded .deb (e.g., code_*_amd64.deb)
sudo apt install ./code_*_amd64.deb
```

<p align="center">
  <img src="asset/vscode03.png" alt="Install VS Code .deb" width="60%" />
</p>

* The `.deb` installer also **offers to add Microsoft’s apt repo and signing key** so you get automatic updates. On a non-interactive terminal, you can pre-accept that prompt:

  ```bash
  echo "code code/add-microsoft-repo boolean true" | sudo debconf-set-selections
  ```

  Then install the `.deb` as above. ([Visual Studio Code][2])

---

## Option B — Install via Microsoft apt repository (for auto-updates)

If you prefer to set up the repo **first** and then install:

```bash
# 1) Prereqs
sudo apt update
sudo apt install -y wget gpg apt-transport-https

# 2) Add Microsoft GPG key
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo install -D -o root -g root -m 644 microsoft.gpg /usr/share/keyrings/microsoft.gpg
rm -f microsoft.gpg

# 3) Add VS Code repo
sudo tee /etc/apt/sources.list.d/vscode.sources >/dev/null <<'EOF'
Types: deb
URIs: https://packages.microsoft.com/repos/code
Suites: stable
Components: main
Architectures: amd64,arm64,armhf
Signed-By: /usr/share/keyrings/microsoft.gpg
EOF

# 4) Install
sudo apt update
sudo apt install -y code   # or: code-insiders
```

These commands are from the official “Visual Studio Code on Linux” docs. ([Visual Studio Code][2])

---

## Verify

```bash
code --version
```

You should see a version like `1.xx.x`. Official CLI usage is documented here. ([Visual Studio Code][3])

---

## Launch from the terminal

Open the current folder in VS Code:

```bash
code .
```

If `code` is not found, **close and reopen the terminal** (or log out/in) so your shell picks up the new command. CLI usage reference: ([Visual Studio Code][3])

---

## References (Official)

* **Visual Studio Code on Linux (Debian/Ubuntu)** — install via `.deb` or repository, auto-update notes: ([Visual Studio Code][2])
* **Download Visual Studio Code** — official `.deb` package: ([Visual Studio Code][1])
* **VS Code Command Line (CLI)** — `code` and `code .` usage: ([Visual Studio Code][3])

---

### Scope

This page focuses on **Ubuntu/Debian** to keep your course consistent and simple.

[1]: https://code.visualstudio.com/download "Download Visual Studio Code - Mac, Linux, Windows"
[2]: https://code.visualstudio.com/docs/setup/linux "Visual Studio Code on Linux"
[3]: https://code.visualstudio.com/docs/configure/command-line "Command Line Interface (CLI)"
