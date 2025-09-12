# Jupyter on macOS — Install & Verify

> Target audience: Students using **macOS** (Apple Silicon or Intel).
> Goal: Install **Jupyter Notebook** (and optionally **JupyterLab**) with `pip`, using a virtual environment for clean isolation. Steps follow the official docs.

---

## 1) Prerequisites

* **Python 3** and **pip** available (via Homebrew or pyenv).
* Use a **virtual environment** to avoid polluting system/site packages. ([Python Packaging][1])

Check versions:

```bash
python --version
python -m pip --version
```

If Python/pip are missing, install Python first (e.g., Homebrew `brew install python` or pyenv), then return here. ([Homebrew Documentation][2])

---

## 2) Create & activate a virtual environment (recommended)

```bash
# from your project folder
python -m venv .venv
source .venv/bin/activate
```

This uses Python’s built-in `venv` module. To leave later: `deactivate`. ([Python Packaging][1])

---

## 3) Install Jupyter

### Option A — Notebook (classic interface, Notebook 7)

```bash
python -m pip install --upgrade pip
python -m pip install notebook
```

Notebook 7 is launched with `jupyter notebook`. ([Jupyter][3])

### Option B — JupyterLab (next-gen UI)

```bash
python -m pip install jupyterlab
```

If you installed with `--user` (not inside a venv), ensure your **user base bin** directory is on `PATH`. Find it with:
`python -m site --user-base` → append `/bin` to that path and add it to your shell profile. ([Python Packaging][4])

---

## 4) Launch

```bash
# Notebook
jupyter notebook

# OR JupyterLab
jupyter lab
```

Jupyter starts a local server and opens your browser (default: `http://localhost:8888`). ([docs.jupyter.org][5], [jupyter-notebook.readthedocs.io][6])

---

## 5) Create a new notebook

In the browser, use **New → Python 3 (ipykernel)** and start coding.
If a kernel is missing for your environment, install the IPython kernel:

```bash
python -m pip install ipykernel
```

(Needed only for special cases; Notebook/Lab normally set this up.) ([ipython.readthedocs.io][7], [PyPI][8])

---

## 6) Verify

```bash
jupyter --version          # Jupyter components
jupyter notebook --version # if installed
jupyter lab --version      # if installed
```

Notebook and JupyterLab report their versions here. ([docs.jupyter.org][9])

---

## 7) Stop Jupyter

Press **Ctrl+C** in the terminal where it’s running, then confirm with **Y**.
If port 8888 is in use, launch on another port:

```bash
jupyter notebook --port 8889
# or
jupyter lab --port 8889
```

(Starting the Notebook/Lab and default address are documented in Jupyter’s guides.) ([docs.jupyter.org][5], [jupyter-notebook.readthedocs.io][6])

---

## References (Official)

* **Install Jupyter (pip recommended)** — Project Jupyter. ([Jupyter][3])
* **Running the Notebook** — Project Jupyter docs. ([docs.jupyter.org][5])
* **Jupyter Notebook docs (start server)**. ([jupyter-notebook.readthedocs.io][6])
* **JupyterLab — Installation**. ([JupyterLab Documentation][10])
* **Kernels & IPython kernel**. ([ipython.readthedocs.io][7])
* **Python packaging: virtual environments with `venv`**. ([Python Packaging][1])

---

### Scope

This page targets **macOS** and mirrors our Linux lesson: create a venv → install (Notebook or Lab) → launch → verify/stop. If your class standardizes on conda/mamba, use their installers instead; launch remains `jupyter notebook` / `jupyter lab`.

[1]: https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/ "Install packages in a virtual environment using pip and venv"
[2]: https://docs.brew.sh/Homebrew-and-Python "Python — Homebrew Documentation"
[3]: https://jupyter.org/install "Project Jupyter | Installing Jupyter"
[4]: https://packaging.python.org/tutorials/installing-packages/ "Installing Packages - Python Packaging User Guide"
[5]: https://docs.jupyter.org/en/latest/running.html "Running the Notebook — Jupyter Documentation 4.1.1 alpha ..."
[6]: https://jupyter-notebook.readthedocs.io/en/stable/notebook.html "Introduction - Jupyter Notebook Documentation - Read the Docs"
[7]: https://ipython.readthedocs.io/en/stable/install/kernel_install.html "Installing the IPython kernel — IPython 9.4.0 documentation"
[8]: https://pypi.org/project/ipykernel/ "ipykernel"
[9]: https://docs.jupyter.org/en/stable/use/jupyter-command.html "The jupyter Command"
[10]: https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html "Installation — JupyterLab 4.4.5 documentation"
