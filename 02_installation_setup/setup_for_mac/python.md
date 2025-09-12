# Python 3.11.x via pyenv on macOS — Install & Verify

> Target: **macOS** (Apple Silicon or Intel).
> Goal: Use **pyenv** to install a stable Python **3.11.x** without touching the system Python.
> Prereq: pyenv installed & configured (see `install-pyenv-macos.md`).

---

## 1) Pick a 3.11 release

As of now, the latest 3.11 security release is **3.11.13** (June 3, 2025). For strict reproducibility with course materials, you may install **3.11.3** instead—both work the same way. ([Python.org][4])

> Tip: pyenv supports **prefix auto-resolution**; installing `3.11` resolves to the latest 3.11.x known to pyenv. ([GitHub][3])

---

## 2) Install Python with pyenv

Choose **one**:

```bash
# A) Install a specific patch release
pyenv install 3.11.13

# B) Install the latest 3.11.x via prefix
pyenv install 3.11
```

If you hit SSL/readline/tk errors, make sure you installed the macOS build deps from the pyenv wiki (OpenSSL, readline, sqlite, zlib, tcl-tk, etc.). ([GitHub][1])

---

## 3) Make it your default (for your user)

```bash
pyenv global 3.11.13   # or: pyenv global 3.11
```

You can also set per-project versions with `pyenv local 3.11.13` or for just this shell with `pyenv shell 3.11.13`. See pyenv usage. ([GitHub][3])

---

## 4) Verify

```bash
python --version
python -c "import sys,platform; print(sys.executable, platform.python_version())"
```

Expected: `Python 3.11.x` and an executable under `~/.pyenv/versions/...`.

---

## 5) Useful commands

```bash
pyenv install -l   # list all versions available to install
pyenv versions     # list installed versions
pyenv which python # see the resolved interpreter path
```

These behaviors and commands are described in the pyenv README (shims, version selection). ([GitHub][3])

---

## References (Official)

* **Python 3.11.13 release page** (current 3.11.x). ([Python.org][4])
* **pyenv README** (install/usage, prefix resolution & version switching). ([GitHub][3])
* **pyenv wiki — Suggested build environment (macOS)**. ([GitHub][1])

---

[1]: https://github.com/pyenv/pyenv/wiki "Home · pyenv/pyenv Wiki · GitHub"
[2]: https://formulae.brew.sh/formula/pyenv "pyenv — Homebrew Formulae"
[3]: https://github.com/pyenv/pyenv "GitHub - pyenv/pyenv: Simple Python version management"
[4]: https://www.python.org/downloads/release/python-31113/ "Python Release Python 3.11.13"
