# Jupyter Quick Start

> Goal: Use **Jupyter Notebooks** for quick experiments, visuals, and notes.
> Install guides for each OS live in **`02_Installation_and_setup/`**.

---

## 1) Ways to open Jupyter

Choose one:

* **In VS Code (recommended):**

  * Open your project folder → **Command Palette → “Jupyter: Create New Jupyter Notebook”** (or open an existing `.ipynb`).
  * Pick the **kernel** (top-right) that matches your project’s environment (your `.venv` or pyenv version).

* **Standalone from a terminal:**

  * Activate your project’s environment.

    * Linux/macOS: `source .venv/bin/activate`
    * Windows (PowerShell): `.venv\Scripts\Activate.ps1`
  * Start Jupyter:

    ```bash
    jupyter lab      # modern UI
    # or
    jupyter notebook # classic UI
    ```

Default URL is `http://localhost:8888`.

---

## 2) Kernels = which Python you’re using

The kernel is **the interpreter that runs your code**.

* In VS Code / JupyterLab, click **Select Kernel** and choose the interpreter for your project.
* If your venv isn’t listed, install the kernel **inside that env**:

  ```bash
  python -m pip install ipykernel
  python -m ipykernel install --user --name myenv --display-name "Python (myenv)"
  ```

  Then pick **Python (myenv)** as the kernel.

---

## 3) Cells & shortcuts (the 90% you’ll use)

* **Run cell:** **Shift+Enter**
* **Add cell below:** **B** (in command mode)
* **Add cell above:** **A**
* **Change to Markdown:** **M**
* **Change to Code:** **Y**
* **Delete cell:** **DD** (press *D* twice)
* **Restart Kernel:** from the top bar (useful if things get stuck)

Two cell types:

* **Code** — runs Python.
* **Markdown** — titles, notes, equations (e.g., `**bold**`, `# Heading`).

---

## 4) First notebook

Create a new notebook and try:

```python
# basics
import sys, math
sys.version, math.sqrt(16)
```

```python
# small DataFrame
import pandas as pd
data = {"city": ["NY", "SF", "LA"], "temp_c": [24, 20, 26]}
df = pd.DataFrame(data)
df
```

```python
# quick plot
import matplotlib.pyplot as plt
df.plot(x="city", y="temp_c", kind="bar")
plt.title("Temperatures (°C)")
plt.show()
```

If you get “module not found”, install into **this** environment:

```python
# In a notebook cell (works with the active kernel)
%pip install pandas matplotlib
```

*(You can also use the terminal: `python -m pip install <pkg>` while your venv is active.)*

---

## 5) Files & paths (avoid “file not found”)

* The notebook’s **working directory** is usually the folder you opened. Check with:

  ```python
  import os; os.getcwd()
  ```
* Use **relative paths** from the project root (e.g., `data/sales.csv`).
* Keep data and notebooks in predictable folders:

  ```
  project/
    ├─ data/
    ├─ notebooks/
    ├─ src/
    └─ .venv/
  ```

Load a CSV:

```python
import pandas as pd
sales = pd.read_csv("data/sales.csv")
sales.head()
```

---

## 6) Save, restart, and export

* **Save** often (Ctrl/Cmd+S).
* Use **Restart Kernel** then **Run All** to confirm notebooks run top-to-bottom.
* Export options: **HTML** (shareable) or **.py** (script).

  * In VS Code: “Export” on the top toolbar.
  * In terminal (optional): `jupyter nbconvert --to html notebook.ipynb`.

---

## 7) Mini-activity (15–20 minutes)

1. Open your project folder in VS Code.
2. Create a venv (if missing) and select its **kernel**.
3. New notebook `intro.ipynb`:

   * Make a **Markdown** title and a short goal.
   * Create a small **DataFrame**, compute summary stats (`df.describe()`), and plot a simple chart.
   * Add a cell that saves a filtered result to `data/output.csv`.
4. **Restart & Run All**. Confirm it runs cleanly end-to-end.

---

### Remember

* All install steps for Jupyter and Python are in **`02_Installation_and_setup/`** per OS.
* If something breaks, verify you’re using the **right kernel** and that packages are installed **into that environment**.
