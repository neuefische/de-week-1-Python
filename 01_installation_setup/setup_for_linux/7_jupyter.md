# Jupyter on Linux — Install & Verify (uv)

> Target audience: Students using **Linux** (Ubuntu or other distributions).
> Goal: Install **JupyterLab** and **Jupyter Notebook** once, globally, with
> `uv tool` — then launch them from any folder or from VS Code, no project
> or virtual environment activation needed.

---

## 1) Prerequisites

* **uv** installed → see `1_uv.md`
* **Python** installed via uv → see `2_python.md`

Check:

```bash
uv --version
```

No `pip`, `apt install python3`, or pyenv needed — uv replaces them.
([Astral][1])

---

## 2) Install Jupyter (once)

```bash
uv tool install jupyterlab --with-executables-from notebook --with pip
```

What this does:

* Installs JupyterLab **and** classic Notebook into one isolated, persistent
  environment — your project environments stay untouched.
* Puts the commands `jupyter-lab` and `jupyter-notebook` into
  `~/.local/bin` (already on your `PATH` from the uv setup).
  `--with-executables-from notebook` is needed because `uv tool install`
  only exposes the named package's own command by default.
* `--with pip` adds `pip` to that environment, so `%pip install` works
  inside notebooks (uv environments come without pip by default).
  ([Astral][1], [Astral][2])

If you see `command not found` afterwards, run `uv tool update-shell` and
reopen the terminal.

---

## 3) Launch — from any folder

```bash
jupyter-lab          # JupyterLab
# OR
jupyter-notebook     # classic Notebook
```

Jupyter starts a local server and opens your browser (default:
`http://localhost:8888`). ([docs.jupyter.org][5])

---

## 4) Install packages inside a notebook

Because `pip` was baked in during installation, use the `%pip` magic in a
cell:

```python
%pip install pandas
```

* Always use `%pip`, not `!pip` — the magic installs into the exact
  environment the running kernel uses; `!pip` may hit a different Python.
* If `import` fails right after installing, restart the kernel
  (**Kernel → Restart**) and run the cell again.
* Packages installed this way live in the Jupyter tool environment. If you
  ever re-run the `uv tool install ...` command from step 2, the environment
  is rebuilt and `%pip`-installed packages are removed — install them again
  afterwards.

---

## 5) Using notebooks in VS Code

VS Code runs notebooks through its **Jupyter extension** — it does *not* use
the `jupyter-lab` server from step 2. What it needs is a registered kernel.
([VS Code Docs][8])

**Step 1 — Install the Jupyter extension**

Open the Extensions view (**Ctrl+Shift+X**), search for
`ms-toolsai.jupyter` and click **Install** ([Open VSX][9]). Four small
companion extensions (Keymap, Renderers, Cell Tags, Slide Show) are
installed automatically — that is expected.

**Step 2 — Make a kernel visible to VS Code**

Register the global Jupyter tool environment once:

```bash
"$(uv tool dir)/jupyterlab/bin/python" -m ipykernel install --user --name=uv-jupyter --display-name "Python (uv tool)"
```

**Step 3 — Select the kernel in VS Code**

Open the `.ipynb` file → click **Select Kernel** (top right) →
**Jupyter Kernel…** → choose `my-project` or `Python (uv tool)`.

* If VS Code asks whether you trust the folder, click **Trust** —
  Restricted Mode blocks cell execution. ([VS Code Docs][8])
* Kernel not listed? Reload the window: **Ctrl+Shift+P** →
  *Developer: Reload Window*.

**Installing packages from VS Code cells**

* `my-project` kernel: use `!uv add pandas` (recorded in `pyproject.toml`)
  or `!uv pip install pandas` (environment only). `%pip` does **not** work
  here — uv project environments contain no pip. ([Astral][2])
* `Python (uv tool)` kernel: `%pip install pandas` works, exactly as in
  step 4.

> With Microsoft's optional **Python** extension installed, a project's
> `.venv` also appears directly under **Python Environments…** in the
> kernel picker — registration (step 2) is then unnecessary.

---

## 6) Verify

```bash
jupyter-lab --version
jupyter-notebook --version
uv tool list                 # shows the Jupyter tool environment
```

---

## 7) Stop & keep up to date

To stop, press **Ctrl+C** in the terminal where Jupyter is running, then confirm with
**Y**. 

If port 8888 is in use, launch on another port:

```bash
jupyter-lab --port 8889
```

Upgrade Jupyter (or all uv tools) with:

```bash
uv tool upgrade jupyterlab
uv tool upgrade --all
```

([Astral][1], [docs.jupyter.org][5])

---

## References (Official)

* **Using tools (uv tool install / upgrade)** — Astral. ([Astral][1])
* **Using uv with Jupyter** — Astral. ([Astral][2])
* **Install Jupyter** — Project Jupyter. ([Jupyter][3])
* **Running the Notebook** — Project Jupyter docs. ([docs.jupyter.org][5])
* **Kernels & IPython kernel**. ([ipython][7])
* **Jupyter Notebooks in VS Code**. ([VS Code Docs][8])
* **Jupyter extension `ms-toolsai.jupyter`** — Open VSX. ([Open VSX][9])

---

### Scope

This page targets **Linux** and mirrors the macOS/Windows lessons, using the
**uv tool-based flow**: install once globally → launch from anywhere →
`%pip install` inside notebooks → optional VS Code integration via the
Jupyter extension. The older `pip` + `python -m venv` flow is replaced —
uv handles isolation and PATH.

[1]: https://docs.astral.sh/uv/guides/tools/ "Using tools — Astral Docs"
[2]: https://docs.astral.sh/uv/guides/integration/jupyter/ "Using uv with Jupyter — Astral Docs"
[3]: https://jupyter.org/install "Project Jupyter | Installing Jupyter"
[5]: https://docs.jupyter.org/en/latest/running.html "Running the Notebook — Jupyter Documentation"
[7]: https://ipython.readthedocs.io/en/stable/install/kernel_install.html "Installing the IPython kernel"
[8]: https://code.visualstudio.com/docs/datascience/jupyter-notebooks "Jupyter Notebooks in VS Code"
[9]: https://open-vsx.org/extension/ms-toolsai/jupyter "Jupyter extension — Open VSX"
