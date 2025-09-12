# VS Code on macOS — Install & Verify

> Target audience: Students using **macOS** (Apple Silicon or Intel).
> Goal: Install **Visual Studio Code**, add the `code` command to your PATH, and verify.

---

## Option A — Download & drag to Applications (official method)

1. **Download VS Code for macOS**.
   From the official page, download the **Universal** build (works on Apple silicon and Intel). ([Visual Studio Code][2])

2. **Install**:

   * Open the downloaded archive (ZIP).
   * **Drag** `Visual Studio Code.app` to **Applications**.
   * Launch **Visual Studio Code** from **Applications** or Spotlight. ([Visual Studio Code][2])

---

## Option B — Homebrew (auto-updates via cask)

```bash
brew install --cask visual-studio-code
```

This installs `Visual Studio Code.app` into Applications. ([Homebrew Formulae][3])

---

## Add `code` to your PATH (so `code .` works)

### Quick way (recommended)

1. Open VS Code.
2. Press **⌘⇧P** (Command–Shift–P) → type “**shell command**” → run
   **Shell Command: Install ‘code’ command in PATH**.
3. Restart your terminal. You can now run `code .` in any folder. ([Visual Studio Code][2])

### Manual alternative (if needed)

Add VS Code’s bin dir to your shell profile:

* **zsh** (`~/.zprofile`):

  ```bash
  echo 'export PATH="$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"' >> ~/.zprofile
  ```
* **bash** (`~/.bash_profile`):

  ```bash
  echo 'export PATH="$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"' >> ~/.bash_profile
  ```

Open a new terminal and try `code .`. ([Visual Studio Code][2])

---

## Verify

```bash
code --version
```

You should see a version like `1.xx.x`. (CLI details are in the official docs.) ([Visual Studio Code][4])

---

## Notes & Common Gotchas

* **Universal build / Apple silicon**: VS Code provides a Universal build (Intel + Arm64). Downloading the standard macOS build is fine for both chip types. ([Visual Studio Code][2])
* If `code` isn’t found after installation, you likely skipped the **Shell Command: Install ‘code’ command in PATH** step or need to **open a new terminal**. ([Visual Studio Code][2])
* **Don’t use Visual Studio for Mac** for this course; it’s a different product and was **retired** on Aug 31, 2024. Use **VS Code** instead. ([Microsoft Learn][1])

---

## References (Official)

* **Visual Studio Code on macOS — Install & CLI PATH**. ([Visual Studio Code][2])
* **Homebrew cask: `visual-studio-code`** (install command). ([Homebrew Formulae][3])
* **VS Code CLI docs** (`code`, `code .`). ([Visual Studio Code][4])

---

### Scope

This page is macOS-only and mirrors our Linux guide: install (download or Homebrew) → add PATH → verify.

[1]: https://learn.microsoft.com/en-us/visualstudio/releases/2022/what-happened-to-vs-for-mac "What happened to Visual Studio for Mac"
[2]: https://code.visualstudio.com/docs/setup/mac "Visual Studio Code on macOS"
[3]: https://formulae.brew.sh/cask/visual-studio-code "visual-studio-code"
[4]: https://code.visualstudio.com/docs/configure/command-line "Command Line Interface (CLI)"
