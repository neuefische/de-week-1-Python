# pyenv on macOS — Install & Set Up

> Target: **macOS** (Apple Silicon or Intel).
> Goal: Install **pyenv**, add it to your shell so it works in new terminals, and verify.

---

## 1) Install Homebrew (if you don’t have it)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

After install, follow the on-screen `brew shellenv` instructions so `brew` is on your `PATH`, then check:

```bash
brew --version
```

(We use Homebrew to install pyenv and build dependencies.)

---

## 2) Install build tools & libraries (recommended by pyenv)

```bash
xcode-select --install || true
brew update
brew install openssl readline sqlite3 xz zlib tcl-tk@8 libb2 zstd
```

These are the **Suggested build environment** packages for macOS in the pyenv wiki. They prevent common compile errors (SSL, readline, Tk). ([GitHub][1])

---

## 3) Install pyenv (via Homebrew)

```bash
brew install pyenv
```

You can confirm the formula here: Homebrew `pyenv`. ([Homebrew Formulae][2])

---

## 4) Add pyenv to your shell (zsh on modern macOS)

Append these to **`~/.zshrc`** (works for Apple Silicon & Intel):

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init - zsh)"' >> ~/.zshrc
```

If you also want it in login shells, add the same lines to `~/.zprofile` or `~/.zlogin`. These lines are from pyenv’s README (Zsh section). ([GitHub][3])

Apply changes:

```bash
exec "$SHELL"   # or: source ~/.zshrc
```

---

## 5) Verify pyenv

```bash
which pyenv
pyenv --version
```

(If `pyenv` isn’t found, re-check Step 4.) See pyenv README for install & shell-setup details. ([GitHub][3])

---

## References (Official)

* **pyenv README** — Homebrew install & Zsh setup. ([GitHub][3])
* **pyenv wiki — Suggested build environment (macOS)**. ([GitHub][1])
* **Homebrew formula: `pyenv`**. ([Homebrew Formulae][2])

---


[1]: https://github.com/pyenv/pyenv/wiki "Home · pyenv/pyenv Wiki · GitHub"
[2]: https://formulae.brew.sh/formula/pyenv "pyenv — Homebrew Formulae"
[3]: https://github.com/pyenv/pyenv "GitHub - pyenv/pyenv: Simple Python version management"
[4]: https://www.python.org/downloads/release/python-31113/ "Python Release Python 3.11.13"
