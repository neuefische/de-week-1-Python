# Bash on macOS — Verify, Install, and Set as Default

> Target audience: Students using **macOS** (Apple Silicon or Intel).
> Goal: Keep macOS stable while installing **Bash 5** via Homebrew, then (optionally) make it your default login shell.

---

## 1) Check what you already have

macOS ships an older Bash (3.2). Confirm your current version and path:

```bash
bash --version
echo "$BASH_VERSION"
which bash
echo "$SHELL"      # current login shell
```

Expected (before installing): version `3.2.x` and `/bin/bash`.

---

## 2) Install Homebrew (if not already installed)

If `brew` is not found:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

After installation, follow the on-screen message to add Homebrew to your `PATH` (it differs for Apple Silicon vs Intel).

* Apple Silicon default prefix: `/opt/homebrew`
* Intel default prefix: `/usr/local`

Verify:

```bash
brew --version
```

---

## 3) Install Bash 5 with Homebrew

```bash
brew install bash
```

This installs a modern Bash at `$(brew --prefix)/bin/bash`.

---

## 4) (Optional) Make Homebrew Bash your default login shell

1. Add the new Bash binary to `/etc/shells` **once**:

```bash
BREW_BASH="$(brew --prefix)/bin/bash"
echo "$BREW_BASH"     # sanity check (should be /opt/homebrew/bin/bash or /usr/local/bin/bash)

# Append only if not already listed
sudo grep -qxF "$BREW_BASH" /etc/shells || echo "$BREW_BASH" | sudo tee -a /etc/shells >/dev/null
```

2. Change your login shell to the new path:

```bash
chsh -s "$BREW_BASH"
```

3. **Close and reopen** Terminal (or log out/in), then verify:

```bash
echo "$SHELL"          # should now be the Homebrew path
bash --version         # should report 5.x
```

---

## 5) Start a Bash 5 session now (without changing your default)

```bash
"$(brew --prefix)/bin/bash"
# type 'exit' to return to your previous shell
```

---

## Notes & Common Gotchas

* Since macOS Catalina, the **default shell is zsh**. That’s fine—installing Bash 5 doesn’t break zsh.
* **Do not change `/bin/sh`**; it’s managed by the system.
* If `chsh` fails with a permissions error, ensure you used `sudo` when updating `/etc/shells`, and that the path you added matches `$(brew --prefix)/bin/bash`.
* On managed/locked-down Macs, changing the login shell may require admin approval.

---

## References (Official)

* Homebrew (install & usage): [https://brew.sh/](https://brew.sh/)
* GNU Bash Manual (language & builtins): [https://www.gnu.org/software/bash/manual/](https://www.gnu.org/software/bash/manual/)
* `chsh(1)` (change login shell) — macOS man page: run `man chsh` in Terminal

---

### Scope

This page focuses on **macOS** with **Homebrew**. It mirrors the Linux lesson’s layout: verify → install → (optional) set as default → verify.
