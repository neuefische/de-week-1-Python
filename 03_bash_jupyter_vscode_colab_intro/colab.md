# Google Colab Quick Start

> Goal: Use **Google Colab** to run Python notebooks in the cloud—no local setup needed. Great for quick experiments, demos, and when your laptop is underpowered.

---

## 1) What is Colab?

* A free, hosted Jupyter environment from Google.
* Runs your code on Google servers; you work in the browser.
* Comes with many scientific packages preinstalled (NumPy, Pandas, etc.).
* You can use **CPU**, **GPU**, or **TPU** (subject to availability and limits).

**When to use it**

* You don’t have Python set up yet.
* You need a quick GPU for a short task.
* You want to share a notebook that “just runs” in a browser.

---

## 2) Start a new notebook

1. Go to **[https://colab.research.google.com](https://colab.research.google.com)** and sign in.
2. **New Notebook** (bottom-right) → a blank notebook opens.
3. Rename it (top-left) and it will save to **My Drive/Colab Notebooks** by default.

> You can also open a notebook from **Google Drive**, **GitHub**, or by **uploading** a `.ipynb`.

---

## 3) Choose hardware (CPU / GPU / TPU)

1. **Runtime → Change runtime type**
2. **Hardware accelerator:** choose **GPU** or **TPU**, or leave as **None (CPU)**.
3. **Save**. A session restarts with the chosen hardware.

> GPUs/TPUs are shared resources. Availability and session length can vary.

---

## 4) Install extra packages

Colab has many packages already. For extras, use `pip` **in a cell**:

```python
!pip install scikit-learn plotly
```

* The **!** means “run this as a shell command”.
* Packages install into the current session only; you may need to reinstall when a session is recycled.

---

## 5) Access files and data

### Option A — Upload from your computer

```python
from google.colab import files
uploaded = files.upload()    # choose local files to upload
```

Uploaded files live in the ephemeral `/content/` directory.

### Option B — Download to your computer

```python
from google.colab import files
files.download("result.csv")
```

### Option C — Mount Google Drive (recommended for datasets & outputs)

```python
from google.colab import drive
drive.mount('/content/drive')        # follow the prompt
```

Your Drive appears under `/content/drive/MyDrive/…`. Read/write like normal files:

```python
import pandas as pd
df = pd.read_csv('/content/drive/MyDrive/data/sales.csv')
df.to_csv('/content/drive/MyDrive/outputs/result.csv', index=False)
```

### Option D — Pull from GitHub (read-only clone)

```python
!git clone https://github.com/OWNER/REPO.git
%cd REPO
```

---

## 6) Work with data & plots (quick example)

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.DataFrame({"city": ["NY","SF","LA"], "temp_c": [24,20,26]})
df.describe()

df.plot(x="city", y="temp_c", kind="bar")
plt.title("Temperatures (°C)")
plt.show()
```

If you get “ModuleNotFoundError”, install in the current session:

```python
!pip install pandas matplotlib
```

---

## 7) Keyboard shortcuts you’ll use

* **Shift+Enter**: run cell
* **Ctrl/Cmd+M, B**: insert cell below
* **Ctrl/Cmd+M, A**: insert cell above
* **Ctrl/Cmd+M, M**: change cell to Markdown
* **Ctrl/Cmd+M, Y**: change cell to Code
* **Ctrl/Cmd+M, .**: interrupt execution

---

## 8) Save, share, and version

* **Autosave** to Google Drive is on.
* **File → Save a copy in Drive** to duplicate.
* **Share** (top-right): add emails or make a link (respect classroom privacy).
* To keep a record of packages used:

  ```python
  !pip freeze > requirements.txt
  ```

  Then **files.download('requirements.txt')** or save to Drive.


## 9) Limits & gotchas

* **Session timeouts**: idle sessions disconnect; long jobs may stop. Break work into smaller steps and persist results to Drive.
* **Hardware availability**: GPU/TPU access can be limited. If not available, fall back to CPU or try later.
* **Environment resets**: when the kernel restarts, packages and `/content` files are gone—reinstall or read from Drive.
* **Large files**: prefer streaming/Chunked reads or store in Drive. Consider compressing outputs.

---

## 10) Mini-activity (15–20 minutes)

1. Open Colab → **New Notebook** → switch to **GPU** (if available).
2. **Mount Drive** and create a folder: `/content/drive/MyDrive/day2/`.
3. Make a small **DataFrame**, do `df.describe()`, and **plot** a chart.
4. Save a CSV to your `day2` folder in Drive.
5. Use `!pip install` to add one package you don’t have (e.g., `seaborn`) and make a second plot.
6. **Restart runtime** and **Run all** to confirm it fully reproduces.

### Remember

Colab is great for quick wins. For larger projects or team work, prefer a local repo in VS Code with a reproducible environment (venv/pyenv) and keep notebooks clean and re-runnable.
