# Python 3.11.x via pyenv-win — Install & Verify (Windows)

> Target: **Windows 10/11 (64-bit)**
> Goal: Use **pyenv-win** to install a stable Python **3.11.x** without touching any system Python.
> Prereq: pyenv-win installed & configured (see `install-pyenv-windows.md`).

---

## 1) Pick a 3.11 release

As of now, the latest 3.11 security release is **3.11.13** (June 3, 2025). If your course screenshots use **3.11.3**, that version is fine too. ([Python.org][3])

List versions pyenv-win can install:

```powershell
pyenv install -l
```

---

## 2) Install Python

Choose **one**:

```powershell
# A) Install a specific patch release
pyenv install 3.11.13

# B) Match screenshots exactly
pyenv install 3.11.3
```

If you see SSL/readline/Tk issues, revisit pyenv-win’s installation page; ensure PATH and env vars are correct. ([pyenv-win.github.io][1])

---

## 3) Make it your default (for your user)

```powershell
pyenv global 3.11.13   # or 3.11.3
pyenv rehash
```

`pyenv rehash` refreshes shims after switching versions. ([Stack Overflow][4])

---

## 4) Verify

```powershell
python --version
python -c "import sys,platform; print(sys.executable, platform.python_version())"
```

Expected: `Python 3.11.x` and an executable path under `%USERPROFILE%\.pyenv\pyenv-win\...`.

If `python` opens the Microsoft Store instead, **turn off** the Python App Installer aliases (see Step 3 in the pyenv file). ([pyenv-win.github.io][1])

---

## 5) Useful commands

```powershell
pyenv versions      # list installed versions
pyenv which python  # see which interpreter is being used
pyenv local 3.11.13 # per-project version (creates .python-version)
pyenv shell 3.11.13 # this terminal session only
```

(Behavior and commands per pyenv-win usage.) ([pyenv-win.github.io][1])

---

## Alternative: Official python.org installer (GUI)

If you prefer the GUI installer instead of pyenv-win:

1. Go to the **Python 3.11.3** release page and download the **Windows 64-bit installer**. ([Python.org][5])
2. Run the installer and **check “Add Python to PATH”** (recommended). The official docs describe this PATH option. ([Python documentation][6])

<p align="center">
  <img src="asset/Check_Box.png" alt="Add Python to PATH" width="60%" />
</p>

3. Proceed with installation.

<p align="center">
  <img src="asset/Installing_python.png" alt="Installing Python on Windows" width="60%" />
</p>

4. Open a **new** Command Prompt and verify:

```cmd
python --version
```

Expected: `Python 3.11.3`. (Use this method only if your course requires the exact patch; otherwise prefer pyenv-win so you can manage multiple versions cleanly.) ([Python documentation][6])

---

## References (Official)

* **Python 3.11.13 release** (latest 3.11.x at time of writing). ([Python.org][3])
* **python.org downloads (3.11.3 listed)**. ([Python.org][5])
* **Using Python on Windows** — “Add Python to PATH” option. ([Python documentation][6])
* **pyenv-win — Installation / env vars / alias note**. ([pyenv-win.github.io][1])

---

### Scope

Two separate files keep **pyenv-win setup** independent from **Python version install**, just like your Linux and macOS guides. This makes patch-version bumps simple without touching the pyenv instructions.

[1]: https://pyenv-win.github.io/pyenv-win/docs/installation.html "Installation | pyenv-win"
[2]: https://github.com/pyenv/pyenv "pyenv/pyenv: Simple Python version management"
[3]: https://www.python.org/downloads/release/python-31113/ "Python Release Python 3.11.13"
[4]: https://stackoverflow.com/questions/63941443/local-python-version-not-changing-after-installing-pyenv-win "Local python version not changing after installing pyenv-win"
[5]: https://www.python.org/downloads/ "Download Python"
[6]: https://docs.python.org/3/using/windows.html "4. Using Python on Windows"
