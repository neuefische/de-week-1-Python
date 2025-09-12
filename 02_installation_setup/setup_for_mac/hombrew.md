# Homebrew on macOS — Install & Verify

> Target audience: Students using **macOS** (Apple Silicon or Intel).
> Goal: Install **Homebrew** (the macOS package manager), add it to your shell so `brew` works in new terminals, and verify.

---

## 1) Open Terminal

* **Applications → Utilities → Terminal**, or press **Cmd+Space** and type “Terminal”.

---

## 2) Run the official install command

Paste this into Terminal and press **Enter**:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

* The installer puts Homebrew in the **default prefix**

  * Apple Silicon: `/opt/homebrew`
  * Intel: `/usr/local`
    so you can use prebuilt packages (“bottles”). It shows exactly what it will do and asks for confirmation. ([Homebrew Documentation][1])
* The installer may prompt to install **Command Line Tools for Xcode**—allow it. ([Homebrew Documentation][1])

---

## 3) Add Homebrew to your shell’s PATH (one-time)

After installation, the script prints **two commands** to add Homebrew to your PATH. **Copy/paste the exact lines it shows.**
Examples:

* **Apple Silicon (zsh default):**

  ```bash
  echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
  eval "$(/opt/homebrew/bin/brew shellenv)"
  ```
* **Intel (zsh default on newer macOS, or bash users use \~/.bash\_profile):**

  ```bash
  echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zprofile
  eval "$(/usr/local/bin/brew shellenv)"
  ```

Generic guidance from the docs: add
`eval "$(<Homebrew prefix>/bin/brew shellenv)"`
to your shell init file so `brew` is available next time you open Terminal. ([Homebrew Documentation][1])

---

## 4) Verify

```bash
brew --version
brew doctor
```

You should see a version like `Homebrew 4.x.x`; `brew doctor` offers suggestions if anything needs fixing. ([Homebrew Documentation][2])

---

## 5) (Optional) Alternative installer (.pkg)

For managed or automated setups, an official **.pkg** installer is available and installs to the same default prefix (`/opt/homebrew` on Apple Silicon, `/usr/local` on Intel). See the **latest Homebrew/brew release** page for the `.pkg`. ([Homebrew Documentation][1], [GitHub][3])

---

## Notes & Common gotchas

* If `brew` isn’t found right after install, you likely **didn’t add `brew shellenv`** lines yet (Step 3) or need to **open a new terminal**. ([Homebrew Documentation][1])
* No need to use `sudo` with `brew install` after the initial installation; the default prefix is designed to avoid that. ([Homebrew Documentation][1])

---

## References (Official)

* **Homebrew — Homepage** (install command): ([Homebrew][4])
* **Homebrew Docs — Installation** (prefixes, PATH instructions, requirements, .pkg): ([Homebrew Documentation][1])
* **Homebrew Docs — Manual / Help**: ([Homebrew Documentation][2])

---

### Scope

This page focuses on **macOS** and follows the same format as our Linux lessons: verify → install → add to PATH → verify.

[1]: https://docs.brew.sh/Installation "Installation — Homebrew Documentation"
[2]: https://docs.brew.sh/ "Documentation — Homebrew Documentation"
[3]: https://github.com/Homebrew/brew/releases/latest "Release 4.6.3 · Homebrew/brew · GitHub"
[4]: https://brew.sh/ "Homebrew — The Missing Package Manager for macOS (or ..."
