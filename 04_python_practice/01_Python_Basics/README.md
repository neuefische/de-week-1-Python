# 🐍 Python Basics

This folder contains Jupyter notebooks for the **Python Basics** track. You’ll practice Python fundamentals, complete exercises, and submit your work via **Git + PR** using the Day-3 workflow.

> 💡 **Pro Tip:** Commit early and often—one commit per notebook section works best. Always **Restart Kernel → Run All** before submitting.

---

## 🎯 What You’ll Learn

* **Core Python:** numbers, strings, `if/elif/else`, loops  
* **Built-in data structures:** lists, sets, dictionaries, and **comprehensions**  
* **Functions:** definitions, calling, parameters & return values  
* **Good notebook habits & coding best practices**  

---

## ⚡ Prerequisites

* Python, Jupyter, and VS Code installed (see `02_Installation_and_setup/` for your OS)  
* A project environment created with **uv**, selected as your Jupyter kernel  

---
## 🏁 Getting Started

1. Open the project folder in **VS Code** or **JupyterLab**.  
2. Create the project environment in the terminal:

   ```bash
   uv init
   uv venv
   ```
3. In VS Code, open a notebook, click **Select Kernel** and choose the `.venv` environment.
4. Install libraries with `uv add`, e.g. `uv add pandas numpy matplotlib ipykernel`. They are all recorded in the `pyproject.toml` file.
5. Open a notebook and run cells with **Shift+Enter**.

> Tip: Commit early and often (e.g., per notebook section).

---

## 🗺 Orientation
* [Intro to Jupyter Lab](./Intro_to_Jupyter_Lab.ipynb)
* [Coding best practices](./Coding_best_practices.ipynb)

## 📚 Basics

1. [Numeric Variable Types](./Basics/1_Numeric_Variable_Types.ipynb)
2. [Strings](./Basics/2_Strings.ipynb)
3. [If-Statement (if, elif, else)](./Basics/3_If_Statement.ipynb)
4. [Loops (while, for)](./Basics/4_Loops.ipynb)

## 🧰 Data Structures in Python

1. [Lists](./Data_Structures_in_Python/1_Lists.ipynb)
2. [Sets](./Data_Structures_in_Python/2_Sets.ipynb)
3. [Mutability](./Data_Structures_in_Python/3_Mutability.ipynb)
4. [Dictionaries](./Data_Structures_in_Python/4_Dictionaries.ipynb)
5. [Comprehension](./Data_Structures_in_Python/5_Comprehension.ipynb)

## 🔧 Functions

1. [Introduction to functions](./Functions/1_Introduction_to_Functions.ipynb)
2. [Function definitions](./Functions/2_Function_Definitions.ipynb)
3. [Calling Functions](./Functions/3_Calling_Functions.ipynb)
4. [Function challenge](./Functions/4_Functions_Challenge.ipynb)

---

## 📝 Exercises

Each topic folder includes an **Exercises/** subfolder with practice tasks that align to the notebooks. Complete the exercises for each section before moving on.

* **Basics/exercise/**
* **Data\_Structures\_in\_Python/exercise/**
* **Functions/exercise/**

 ✅ Submit your work via PR according to the Day-3 Git guide. Ensure notebooks **Restart & Run All** cleanly before committing.
