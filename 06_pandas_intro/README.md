[![Shipping files](https://github.com/neuefische/ds-pandas-numpy/actions/workflows/workflow-02.yml/badge.svg?branch=main&event=workflow_dispatch)](https://github.com/neuefische/ds-pandas-numpy/actions/workflows/workflow-02.yml)
# Introduction to Pandas 


![Pandas](./images/pandas_photo.jpg)
<span>Photo by <a href="https://unsplash.com/@pbernardon?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Pascal Bernardon</a> on <a href="https://unsplash.com/s/photos/panda?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>



In this Repository you can find Jupyter Notebooks that you should work on together as **Pair-Programmers**.

Please make sure you have **forked** the repo, clone it on your computer, and  then set up a new virtual environment.


## Set up your Environment

The added [requirements file](requirements.txt) contains all libraries and dependencies we need to execute Pandas and Numpy. 

### **`macOS`** type the following commands : 

- Install the virtual environment and the required packages by following commands:

    ```BASH
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/bin/activate
    pip install --upgrade pip
    pip install -r requirements.txt
    ```
### **`WindowsOS`** type the following commands :

- Install the virtual environment and the required packages by following commands.

   For `PowerShell` CLI :

    ```PowerShell
    pyenv local 3.11.3
    python -m venv .venv
    .venv\Scripts\Activate.ps1
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```
    Or...

    For `Git-Bash` CLI :
  
    ```Bash
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/Scripts/activate
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```

    **`Note:`**
    If you encounter an error when trying to run `pip install --upgrade pip`, try using the following command:

    ```Bash
    python.exe -m pip install --upgrade pip
    ```
    



At the end of this repo you should 
- understand why Pandas  is valuable tools for Data Engineers
- be familiar to handle data in Pandas DataFrames.
- be able to do some EDA on a new dataset
- know how to plot some basic plots for better data understanding

This repo covers:

- [Introduction to Pandas](01_pandas.ipynb)
- [Practice Pandas functionalities](02_pandas_practice_1.ipynb)
- [Introduction to Pandas visualization](03_pandas_visualization.ipynb)
- [Practice Pandas functionalities and visualizations](04_pandas_practice_2.ipynb)
- [More Pandas practice and EDA](05_pandas_practice_3.ipynb)



