# Python Basics

This folder contains Jupyter notebooks for the **Python Basics** track. You’ll commit progress and submit via PR using the Day-3 Git workflow.

## What you’ll learn

* Core Python (numbers, strings, `if/elif/else`, loops)
* Built-in data structures (lists, sets, dicts) and **comprehensions**
* Functions (definitions, calling, parameters/returns)
* Good notebook habits and coding best practices

## Prerequisites

* Set up Python, Jupyter, and VS Code (see `02_Installation_and_setup/` for your OS).
* Recommended: **Python 3.11.3** in a project **venv** selected as the Jupyter kernel.

## Getting started

1. Open the project folder in VS Code (or JupyterLab).
2. Create and select a virtual environment:

   * **Linux/macOS**

     ```bash
     python -m venv .venv
     source .venv/bin/activate
     ```
   * **Windows (PowerShell)**

     ```powershell
     python -m venv .venv
     .\.venv\Scripts\Activate.ps1
     ```
   * In VS Code: **Python: Select Interpreter** → choose `.venv`.
3. Open a notebook and run cells with **Shift+Enter**.

> Tip: Commit early and often (e.g., per notebook section).

---

## Orientation

* [Intro to Jupyter Lab](./Intro_to_Jupyter_Lab.ipynb)
* [Coding best practices](./Coding_best_practices.ipynb)

## Basics

1. [Numeric Variable Types](./Basics/1_Numeric_Variable_Types.ipynb)
2. [Strings](./Basics/2_Strings.ipynb)
3. [If-Statement (if, elif, else)](./Basics/3_If_Statement.ipynb)
4. [Loops (while, for)](./Basics/4_Loops.ipynb)

## Data Structures in Python

1. [Lists](./Data_Structures_in_Python/1_Lists.ipynb)
2. [Sets](./Data_Structures_in_Python/2_Sets.ipynb)
3. [Mutability](./Data_Structures_in_Python/3_Mutability.ipynb)
4. [Dictionaries](./Data_Structures_in_Python/4_Dictionaries.ipynb)
5. [Comprehension](./Data_Structures_in_Python/5_Comprehension.ipynb)

## Functions

1. [Introduction to functions](./Functions/1_Introduction_to_Functions.ipynb)
2. [Function definitions](./Functions/2_Function_Definitions.ipynb)
3. [Calling Functions](./Functions/3_Calling_Functions.ipynb)
4. [Function challenge](./Functions/4_Functions_Challenge.ipynb)

---

## Exercises

Each topic folder includes an **Exercises/** subfolder with practice tasks that align to the notebooks. Complete the exercises for each section before moving on.

* **Basics/exercise/**
* **Data\_Structures\_in\_Python/exercise/**
* **Functions/exercise/**

Submit your work via PR according to the Day-3 Git guide. Ensure notebooks **Restart & Run All** cleanly before committing.
