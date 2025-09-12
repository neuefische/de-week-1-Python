# Python Virtual Environments in VS Code (macOS)

> Goal: Create/activate a project-scoped Python environment, then point **VS Code** to it.

---

## 1) Method A — `pyenv` + `pyenv-virtualenv`

Install the plugin if needed (Homebrew users can also `brew install pyenv-virtualenv`):

```bash
git clone https://github.com/pyenv/pyenv-virtualenv.git \
  "$(pyenv root)/plugins/pyenv-virtualenv"
exec "$SHELL"
```

Create & activate:

```bash
pyenv install 3.11.3
pyenv virtualenv 3.11.3 myenv
pyenv activate myenv
```

Deactivate & link to a project:

```bash
pyenv deactivate
cd /path/to/project
pyenv local myenv       # writes .python-version so this folder auto-uses myenv
```

> `pyenv virtualenv` and `pyenv activate` are provided by **pyenv-virtualenv**. ([GitHub][1])

---

## 2) Method B — Python’s built-in `venv`

From your project folder:

```bash
python -m venv .venv
source .venv/bin/activate
# ... work ...
deactivate
```

> `venv` is the standard library tool for virtual environments. ([Python documentation][2])

---

## 3) Wire it up in **VS Code**

1. Open the project in VS Code.
2. **Select interpreter**: **Command Palette → “Python: Select Interpreter”** → choose your `.venv` or `myenv`. ([Visual Studio Code][3])
3. (Optional) **Python: Create Environment** to let VS Code create `.venv` for you. ([Visual Studio Code][4])
4. **Auto-activation** in new terminals is handled by the Python extension (`terminal.activateEnvironment`). ([Visual Studio Code][5])

List packages:

```bash
pip list
```

---

## References

* VS Code — **Environments / Select Interpreter / Create Environment**. ([Visual Studio Code][3])
* **pyenv-virtualenv** plugin. ([GitHub][1])
* Python docs — **`venv`**. ([Python documentation][2])

---

### Notes

* Using the folder name **`.venv`** makes VS Code detect it automatically and prefer it for that workspace. ([Visual Studio Code][4])
* Keep per-project envs small and reproducible (e.g., `pip freeze > requirements.txt`).

[1]: https://github.com/pyenv/pyenv-virtualenv "a pyenv plugin to manage virtualenv"
[2]: https://docs.python.org/3/library/venv.html "venv — Creation of virtual environments"
[3]: https://code.visualstudio.com/docs/python/environments "Python environments in VS Code"
[4]: https://code.visualstudio.com/docs/python/python-tutorial "Getting Started with Python in VS Code"
[5]: https://code.visualstudio.com/docs/python/settings-reference "Python settings reference"
