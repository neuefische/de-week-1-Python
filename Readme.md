# 🚀 Week 1 — Python for Data Engineering
Welcome! This repo contains everything you need for **Week 1** of the Data Engineering program: environment setup, Bash/VS Code/Jupyter intros, Git + GitHub workflows, Python practice (basics → intermediate → advanced), and a Pandas primer.
> 💡 Tip: Keep commits small (e.g., one per exercise). When a notebook's tests pass, Restart Kernel → Run All to ensure a clean run.
---
## ⚡ Quick Start
1. **Install uv** (if you haven't already)
* **Linux / macOS**
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```
* **Windows (PowerShell)**
  ```powershell
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```
> 📖 Full installation options: <https://docs.astral.sh/uv/getting-started/installation/>
 
2. **Clone the repo**
```bash
git clone <your-fork-or-classroom-url>.git
cd WEEK1-PYTHON-FOR-DATA-ENGINEERING
```
3. **Create a project virtual environment** (recommended: **Python 3.11.3**)
```bash
uv venv --python 3.11.3
```
> uv will automatically download Python 3.11.3 if it isn't installed on your machine.
 
* **Linux / macOS**
  ```bash
  source .venv/bin/activate
  ```
* **Windows (PowerShell)**
  ```powershell
  .\.venv\Scripts\Activate.ps1
  ```
4. **(Optional) Jupyter & data stack for local runs**
```bash
uv add notebook jupyterlab pandas numpy matplotlib seaborn
```
5. **Launch notebooks**
```bash
jupyter lab
# or
jupyter notebook
```
> 💻 In VS Code:
Open the folder → Command Palette → "Python: Select Interpreter" → pick .venv.
---
## 🎯 What You Will Learn This Week
+ 🛠 Tooling: Bash, VS Code, Jupyter, Google Colab
+ 🌱 Version control: Git + GitHub (clone, branch, commit, PR)
+ 🐍 Python: Core syntax & flow, data structures, functions, error handling, iterators/generators, performance tips
+ 📊 Pandas: Series/DataFrame basics, transforms, visualization
---
## 📂 Folder Map
* **`01_welcome/`**
  * `welcome.md` — course kickoff and expectations. 🎉
* **`02_installation_setup/` [Time Allocation - 2nd half of Day 1]**
  * `setup_for_linux/` — Linux install guides (Bash, Docker, Git, Python/pyenv, VS Code, PostgreSQL/pgAdmin, Jupyter). 🐧
  * `setup_for_mac/` — macOS install guides (Homebrew, Bash, Docker, Git, Python/pyenv, VS Code, PostgreSQL/pgAdmin, Jupyter). 🍎
  * `setup_for_windows/` — Windows  install guides (Git Bash/WSL notes, Docker Desktop, Git, Python/pyenv-win, VS Code, PostgreSQL/pgAdmin, Jupyter). 🪟
  * `vscode_venv/` — how to use **virtual environments** with VS Code (Windows/macOS). 🖥️
    *Use these if your machine isn't set up yet.*
* **`03_bash_jupyter_vscode_colab_intro/`**
  * `bash.md` — Bash intro + practice game (Bandit). 🔹
  * `vscode.md` — VS Code essentials for this course. ✨
  * `jupyter.md` — Jupyter Notebook/Lab walkthrough. 📓
  * `colab.md` — Using Google Colab. ☁️
* **`04_git_github/`**
  * `git_github_intro.md` — class workflow: fork/clone, feature branches, commits, PRs, resolving simple conflicts. 🧩
* **`05_python_practice/`**
  * `python_basics/` — notebooks + **exercise** folder. 
     - Topics:
    * Numeric variable types, Strings, If/Elif/Else, Loops  🐍
    * Lists, Sets, Mutability, Dictionaries, Comprehensions
    * Functions (intro/definitions/calling/challenge)
    * ✅ Each student notebook has **TODOs** and **`assert` tests**.
  * `python_intermediate/` — notebooks + **exercise** folder: ⚡
    * Error handling, Iterators & Generators, Lambda/Map/Filter/Reduce, Performance.
  * `python_advanced/` — notebooks + **exercise** folder:   🚀
    * OOP introduction, Concurrency & Parallelism.
* **`06_pandas_intro/`**
  * `01_pandas.ipynb` → foundations (Series/DataFrame, indexing, I/O).   📊
  * `02_pandas_practice_1.ipynb`, `04_pandas_practice_2.ipynb`, `05_pandas_practice_3.ipynb` → progressively harder practice.
  * `03_pandas_visualization.ipynb` → quick plotting. 📈
  * `data/` — sample CSVs/parquet used by the notebooks. **Don't move/rename**. 🗂️
---
### ✨ Ready to dive in? Your Python + Pandas journey starts here! 🐍💻📊
---
