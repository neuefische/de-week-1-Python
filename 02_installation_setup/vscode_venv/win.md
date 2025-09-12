# Python Virtual Environments in VS Code (Windows)

> Goal: Create/activate a project-scoped Python environment on Windows, then point **VS Code** to it.

---

## 1) Method A — **pyenv-win** + a venv

> `pyenv-win` manages **Python versions** on Windows. For **virtual environments**, prefer the built-in `venv`. (There’s a community `pyenv-win-venv` CLI, but it’s optional.) ([pyenv-win][6], [GitHub][7])

Create a venv for a specific pyenv-win Python:

```powershell
# Ensure the desired version is active
pyenv global 3.11.3

# From your project folder:
python -m venv .venv
.\.venv\Scripts\Activate.ps1   # PowerShell
# ... work here ...
deactivate
```

---

## 2) Method B — Python’s built-in `venv` (recommended on Windows)

From your project folder:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1   # PowerShell
# or (cmd.exe)
# .\.venv\Scripts\activate.bat
```

To deactivate:

```powershell
deactivate
```

> `venv` is the standard library tool for virtual environments. ([Python documentation][2])

*If PowerShell blocks the activation script, either activate from **cmd.exe** (`activate.bat`) or adjust your execution policy per your org’s security rules.*

---

## 3) Wire it up in **VS Code**

1. Open the project in VS Code.
2. **Select interpreter**: **Command Palette → “Python: Select Interpreter”** → pick `.venv` (or another venv). ([Visual Studio Code][3])
3. (Optional) **Python: Create Environment** to have VS Code create `.venv` for you. ([Visual Studio Code][4])
4. **Auto-activate in new terminals**: enabled via `terminal.activateEnvironment`. On Windows the Python extension runs `.\.venv\Scripts\activate` automatically when a new terminal opens. ([Visual Studio Code][5])

List packages:

```powershell
pip list
```

---

## Quick checks

```powershell
python --version
Get-Command python      # PowerShell
# or (cmd.exe)
# where python
```

You should see the interpreter under your project’s `.venv`.

---

## References

* VS Code — **Environments / Select Interpreter / Create Environment / Auto-activation**. ([Visual Studio Code][3])
* **pyenv-win** (Windows Python version manager). ([pyenv-win][6])
* **pyenv-win-venv** (optional CLI for virtualenvs on Windows). ([GitHub][7])
* Python docs — **`venv`**. ([Python documentation][2])

---

### Notes

* Using the folder name **`.venv`** makes VS Code detect it automatically and prefer it for that workspace. ([Visual Studio Code][4])
* Keep per-project envs small and reproducible (e.g., `pip freeze > requirements.txt`).

[2]: https://docs.python.org/3/library/venv.html "venv — Creation of virtual environments"
[3]: https://code.visualstudio.com/docs/python/environments "Python environments in VS Code"
[4]: https://code.visualstudio.com/docs/python/python-tutorial "Getting Started with Python in VS Code"
[5]: https://code.visualstudio.com/docs/python/settings-reference "Python settings reference"
[6]: https://pyenv-win.github.io/pyenv-win/ "pyenv for Windows - GitHub Pages"
[7]: https://github.com/pyenv-win/pyenv-win-venv "A CLI to manage virtual envs with pyenv-win"
