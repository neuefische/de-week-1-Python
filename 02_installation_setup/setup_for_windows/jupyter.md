# Jupyter on Windows — Install & Verify

> Target audience: Students on **Windows 10/11**.
> Goal: Install **Jupyter Notebook** (and/or **JupyterLab**) with `pip`, using a **virtual environment** for clean isolation. Steps follow the official docs.

---

## 1) Prerequisites

* **Python 3** and **pip** installed (e.g., from python.org or the Microsoft Store).
* We’ll use Python’s built-in **venv** to keep packages isolated. ([Python documentation][1])

Check versions (PowerShell or Command Prompt):

```powershell
python --version
python -m pip --version
```

If Python/pip are missing, install Python first, then return here. For installing packages inside isolated environments with `pip + venv`, see the Python Packaging guide. ([Python Packaging][2])

---

## 2) Create & activate a virtual environment (recommended)

From your project folder:

```powershell
python -m venv .venv
```

Activate it:

* **PowerShell**

  ```powershell
  .\.venv\Scripts\Activate.ps1
  ```
* **Command Prompt (cmd.exe)**

  ```bat
  .\.venv\Scripts\activate.bat
  ```

To deactivate later: `deactivate`. (Virtual environments are the officially recommended way to manage project dependencies.) ([Python documentation][1], [Python Packaging][2])

> If PowerShell blocks `Activate.ps1` due to execution policy, either use the **cmd.exe** activation above or adjust your policy per your org’s guidelines.

---

## 3) Install Jupyter

Upgrade `pip`, then choose **Notebook** or **Lab**:

### Option A — Notebook (classic interface, Notebook 7)

```powershell
python -m pip install --upgrade pip
python -m pip install notebook
```

Launch later with `jupyter notebook`. ([jupyter.org][3], [jupyter-notebook.readthedocs.io][4])

### Option B — JupyterLab (next-gen UI)

```powershell
python -m pip install jupyterlab
```

Launch later with `jupyter lab`. If you install with `--user` instead of a venv, make sure your **user-level Scripts** directory is on `PATH` so `jupyter` is found. On Windows, find it via:
`py -m site --user-site` → replace `site-packages` with **`Scripts`**, then add that directory to your PATH. ([jupyterlab.readthedocs.io][5])

(Jupyter’s official pages document both `notebook` and `jupyterlab` installs via `pip`.) ([jupyter.org][3], [jupyterlab.readthedocs.io][5])

---

## 4) Launch

```powershell
# Notebook
jupyter notebook

# OR JupyterLab
jupyter lab
```

Jupyter starts a local server and opens your browser (default: `http://localhost:8888`). ([jupyter.org][3])

---

## 5) Create a new notebook

In the browser, choose **New → Python 3 (ipykernel)** and start coding.
Notebook/Lab install the **IPython kernel** for Python automatically; if you need to register a specific venv as a named kernel, see Step 8. ([docs.jupyter.org][6])

---

## 6) Verify

```powershell
jupyter --version          # Jupyter components
jupyter notebook --version # if installed
jupyter lab --version      # if installed
```

Notebook 7 / JupyterLab report versions here. ([jupyter-notebook.readthedocs.io][4])

---

## 7) Stop Jupyter

Press **Ctrl+C** in the terminal where it’s running, then confirm with **Y**.

If port 8888 is in use, start on another port:

```powershell
jupyter notebook --port 8889
# or
jupyter lab --port 8889
```

---

## 8) (Optional) Register the current venv as a named kernel

Useful when you juggle multiple environments:

```powershell
python -m pip install ipykernel
python -m ipykernel install --user --name myenv --display-name "Python (myenv)"
```

You’ll now see **Python (myenv)** in the kernel chooser. ([ipython.readthedocs.io][7], [docs.jupyter.org][6])

---

## Troubleshooting

* **`'jupyter' is not recognized`**
  Ensure your **venv is activated** (Step 2). If you installed with `--user`, add your **user Scripts** directory to `PATH` as described above. ([jupyterlab.readthedocs.io][5])
* **Browser doesn’t open**
  Copy the `http://localhost:8888/?token=...` URL from the terminal into your browser.
* **Wrong Python shows up**
  Use Step 8 to register the exact venv you want as a kernel.

---

## References (Official)

* **Install Jupyter (pip recommended)** — Project Jupyter. ([jupyter.org][3])
* **JupyterLab — Installation** (pip, PATH notes). ([jupyterlab.readthedocs.io][5])
* **Jupyter Notebook docs (Notebook 7)** — install & start. ([jupyter-notebook.readthedocs.io][4])
* **Python `venv`** — create & use virtual environments. ([Python documentation][1])
* **Packaging guide** — `pip` + virtual environments; Windows `--user` PATH note. ([Python Packaging][2])
* **IPython kernel** — installing kernels for Jupyter. ([ipython.readthedocs.io][7])

---

### Scope

This page is Windows-only and mirrors our Linux/macOS guides: create a venv → install (Notebook or Lab) → launch → verify/stop → optional kernel registration.

[1]: https://docs.python.org/3/library/venv.html "venv — Creation of virtual environments"
[2]: https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/ "Install packages in a virtual environment using pip and venv"
[3]: https://jupyter.org/install "Project Jupyter | Installing Jupyter"
[4]: https://jupyter-notebook.readthedocs.io/en/latest/index.html "Jupyter Notebook 7.5.0a1 documentation"
[5]: https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html "Installation — JupyterLab 4.4.5 documentation"
[6]: https://docs.jupyter.org/en/latest/install/kernels.html "Installing Kernels - Jupyter Documentation"
[7]: https://ipython.readthedocs.io/en/stable/install/kernel_install.html "Installing the IPython kernel — IPython 9.4.0 documentation"
