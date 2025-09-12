# VS Code Quick Start

> Goal: Use **VS Code** for Python work—scripts, Jupyter notebooks, and Markdown—using clear, simple steps.
> Install guides are in this repo under **`02_Installation_and_setup/`** for Linux, macOS, and Windows.

---

## 1) Open a project in VS Code

1. **Open VS Code**.
2. **File → Open Folder…** (pick your course/project folder).
3. Open a terminal **inside VS Code**: **Terminal → New Terminal** (or ``Ctrl+` `` / ``Cmd+` `` on macOS).

> Tip: Keep each project in its **own folder** with a `.venv/` (or pyenv environment) for clean dependencies.

---

## 2) Add the right extensions

Install these from the **Extensions** view (square icon on the left):

* **Python** (by Microsoft) — language support, Run/Debug, testing.
* **Jupyter** (by Microsoft) — run **`.ipynb`** notebooks.
* *(Optional)* **Pylance** (type checking/completions), **Markdown All in One** (better Markdown editing).

---

## 3) Use your Python environment

1. Create/activate your venv for this project (see your OS guide in `02_Installation_and_setup/` if needed).
2. In VS Code, open the **Command Palette** (**Ctrl+Shift+P** / **Cmd+Shift+P**) → **Python: Select Interpreter** → pick your project’s interpreter (e.g., **.venv/bin/python** on Linux/macOS or **.venv\Scripts\python.exe** on Windows).
3. New terminals opened in VS Code will auto-activate the environment (if you selected the interpreter and the Python extension is enabled).

> If the wrong Python shows up, re-run **Python: Select Interpreter** and reopen the terminal.

---

## 4) Run a Python script

1. Create a file: **`hello.py`**
2. Paste:

   ```python
   name = "World"
   print(f"Hello, {name}!")
   ```
3. Run it:

   * In the editor, click **Run Python File** (triangle button), **or**
   * In the terminal: `python hello.py`

**Debug (optional):** Press **F5**, choose **Python: Current File**. Add breakpoints by clicking in the left gutter.

---

## 5) Work with Jupyter notebooks

### Create and run a notebook

1. **Command Palette → Jupyter: Create New Jupyter Notebook**, or create a file ending with **`.ipynb`**.
2. Pick the **kernel** (top-right): choose your project interpreter.
3. Add a code cell:

   ```python
   import sys
   sys.version
   ```

   Run the cell (play icon).

### Tips

* Add **Markdown cells** for notes and headings.
* Use **Save** to keep your notebook in the project folder.
* You can also **Run All** or **Restart Kernel** from the top bar if things get stuck.

---

## 6) Edit Markdown (READMEs, notes)

1. Create **`README.md`**.
2. Try this starter:

   ````markdown
   # Project Title
   Short description.

   ## Steps
   1. Create venv
   2. Install packages
   3. Run script

   ```bash
   python -m venv .venv
   source .venv/bin/activate   # Windows: .venv\Scripts\Activate.ps1
   pip install -r requirements.txt
   ````

   ```
   ```
3. **Preview**: **Ctrl+Shift+V** (or **Cmd+Shift+V**), or **Open Preview to the Side**.

> Keep docs small and near code so teammates can find them quickly.

---

## 7) Useful VS Code habits

* **Command Palette**: **Ctrl/Cmd+Shift+P** (search any command).
* **Toggle Sidebar**: **Ctrl/Cmd+B**.
* **Rename file**: Right-click in Explorer.
* **Multi-cursor**: **Alt+Click** (Option+Click on macOS).
* **Search in project**: **Ctrl/Cmd+Shift+F**.
* **Format on Save**: Settings → search “format on save” → enable.
* **Integrated Git** (optional today): Source Control view → **Initialize Repository**, stage, commit.
* **Terminal**: open per task (e.g., one for server, one for tests).

---

## 8) Common issues & quick fixes

* **Interpreter mismatch**

  * Re-run **Python: Select Interpreter** for this workspace.
  * Ensure your venv exists and is activated in the terminal.

* **Notebook kernel not found**

  * In the notebook, click **Select Kernel** and choose your project interpreter.
  * If needed: `pip install ipykernel` inside the venv, then select it again.

* **`pip` installs to the wrong Python**

  * Use `python -m pip install <package>` (always picks the active interpreter).

* **Terminal not activating venv**

  * Close that terminal and open a **new** VS Code terminal after selecting interpreter.
  * Windows PowerShell policy blocking `Activate.ps1`? Use **cmd.exe** activation (`.\.venv\Scripts\activate.bat`) or follow your org’s policy to allow scripts.

---

## 9) Mini-activity (15–20 minutes)

1. **Open a new folder** `day2_playground/` in VS Code.
2. **Create & select a venv** → run `python -m venv .venv`, activate it, then **Python: Select Interpreter**.
3. **Make `hello.py`** (above) and run it.
4. **Create `notes.ipynb`** and run a cell that prints `sys.version` and a small list comprehension.
5. **Write `README.md`** with a short checklist and preview it.

Done = you can create, run, and document work in one place.

---

## 10) Where to look next

* **Extensions**: explore linters (Flake8), formatters (Black), testing (pytest).
* **Debugging**: breakpoints, watch variables, launch configs in `.vscode/launch.json`.
* **Notebooks**: try exporting to HTML/PDF for sharing.
* **Settings Sync**: sign in to sync your VS Code settings across machines.

---

### Remember

All install steps (VS Code, Python, Jupyter) are already documented per OS in **`02_Installation_and_setup/`**. If something fails, re-check that page for your platform first.
