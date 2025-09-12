# Jupyter on Ubuntu/Debian — Install & Verify

> Target audience: Students using **Ubuntu/Debian** (including WSL).
> Goal: Install **Jupyter Notebook** (and optionally **JupyterLab**) with `pip`, using a virtual environment for clean isolation. Steps mirror the official docs.

---

## 1) Prerequisites

* **Python 3** and **pip** available (system Python or via `pyenv`).
* Basic terminal access and `sudo` privileges (only if installing Python).
* Jupyter recommends installing with **pip**; use a **virtual environment** to avoid polluting system packages. ([jupyter.org][1], [Python documentation][2])

Check versions:

```bash
python --version
python -m pip --version
```

If Python/pip are missing, install Python first (e.g., with `pyenv`) and return here.

---

## 2) Create & activate a virtual environment (recommended)

```bash
# from your project folder
python -m venv .venv
source .venv/bin/activate
```

This uses the standard library `venv` module. ([Python documentation][3])

> Tip: To leave the venv later: `deactivate`.

---

## 3) Install Jupyter Notebook (or JupyterLab)

### Option A — Notebook (classic interface, Notebook 7)

```bash
python -m pip install --upgrade pip
python -m pip install notebook
```

Launching Notebook 7 after install is still `jupyter notebook`. ([PyPI][4], [jupyter-notebook.readthedocs.io][5])

### Option B — JupyterLab (next-gen UI)

```bash
python -m pip install jupyterlab
```

If you installed with `--user` instead of a venv, make sure `~/.local/bin` is on your `PATH` so `jupyter lab` is found:
`export PATH="$HOME/.local/bin:$PATH"`. ([JupyterLab Documentation][6], [PyPI][7])

---

## 4) Launch

```bash
# Notebook
jupyter notebook

# OR JupyterLab
jupyter lab
```

Jupyter will start a local server and open your browser (default: `http://localhost:8888`). ([jupyter.org][1])

---

## 5) Create a new notebook

In the browser, use **New → Python 3 (ipykernel)** and start coding.

> Note: Installing Notebook also installs the **IPython kernel** for Python. If a kernel is missing in a specific environment, install it with `python -m pip install ipykernel`. ([docs.jupyter.org][8], [ipython.readthedocs.io][9])

---

## 6) Verify

```bash
jupyter --version          # shows Jupyter components
jupyter notebook --version # Notebook version
jupyter lab --version      # if you installed JupyterLab
```

Notebook 7 and JupyterLab report their versions here. ([jupyter-notebook.readthedocs.io][5], [JupyterLab Documentation][6])

---

## 7) Stop Jupyter

Press **Ctrl+C** in the terminal where it’s running, then confirm with **Y**.

If port 8888 is in use, launch on a different port:

```bash
jupyter notebook --port 8889
# or
jupyter lab --port 8889
```

---

## 8) (Optional) Register the current venv as a named kernel

Useful when you manage multiple environments:

```bash
python -m pip install ipykernel
python -m ipykernel install --user --name myenv --display-name "Python (myenv)"
```

You’ll see **Python (myenv)** in the notebook Kernel list. ([ipython.readthedocs.io][9])

---

## References (Official)

* **Install Jupyter (pip recommended)** — Project Jupyter: ([jupyter.org][1])
* **Jupyter Notebook docs** (Notebook 7): ([jupyter-notebook.readthedocs.io][5])
* **JupyterLab — Installation**: ([JupyterLab Documentation][6])
* **Kernels overview / IPython kernel**: ([docs.jupyter.org][8])
* **`venv` (Python virtual environments)**: ([Python documentation][3])

---

### Scope

This page targets **Ubuntu/Debian** setups and keeps to the simplest, officially recommended path: `pip` + virtual environments. If your course uses `conda` instead, installation commands differ but the launch steps (`jupyter notebook` / `jupyter lab`) are the same.

[1]: https://jupyter.org/install "Project Jupyter | Installing Jupyter"
[2]: https://docs.python.org/3/tutorial/venv.html "12. Virtual Environments and Packages"
[3]: https://docs.python.org/3/library/venv.html "venv — Creation of virtual environments"
[4]: https://pypi.org/project/notebook/ "Jupyter Notebook"
[5]: https://jupyter-notebook.readthedocs.io/ "Jupyter Notebook Documentation — Jupyter Notebook 7.4.5 ..."
[6]: https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html "Installation — JupyterLab 4.4.5 documentation"
[7]: https://pypi.org/project/jupyterlab/ "jupyterlab"
[8]: https://docs.jupyter.org/en/latest/install/kernels.html "Installing Kernels - Jupyter Documentation"
[9]: https://ipython.readthedocs.io/en/stable/install/kernel_install.html "Installing the IPython kernel — IPython 9.4.0 documentation"
