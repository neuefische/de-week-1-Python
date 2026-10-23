[![Shipping files](https://github.com/neuefische/ds-pandas-numpy/actions/workflows/workflow-02.yml/badge.svg?branch=main&event=workflow_dispatch)](https://github.com/neuefische/ds-pandas-numpy/actions/workflows/workflow-02.yml)
# Introduction to Pandas 


![Pandas](./images/pandas_photo.jpg)
<span>Photo by <a href="https://unsplash.com/@pbernardon?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Pascal Bernardon</a> on <a href="https://unsplash.com/s/photos/panda?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>



In this Repository you can find Jupyter Notebooks that you should work on together as **Pair-Programmers**.

Please make sure you have **forked** the repo, clone it on your computer, and  then set up a new virtual environment.


## Set up your Environment

We use [uv](https://docs.astral.sh/uv/) to manage the Python version, the virtual environment and the libraries (see `01_installation_setup/` for installing uv). The commands are the same on macOS, Windows and Linux.

1. In the terminal, inside the project folder, run:

    ```bash
    uv init
    uv venv
    ```

2. Open the folder in **VS Code**, open a notebook and select the kernel (top-right → **Select Kernel** → **Python Environments…** → `.venv`).

3. Install the libraries we need for Pandas and Numpy:

    ```bash
    uv add pandas numpy matplotlib ipykernel
    ```

    Add any further library the same way (`uv add <package>`).

> **Note:** Every library you add with `uv add` is automatically written to the `pyproject.toml` file (and pinned in `uv.lock`). If you clone a project that already has a `pyproject.toml`, just run `uv sync` to install everything.

At the end of this repo you should 
- understand why Pandas  is valuable tools for Data Engineers
- be familiar to handle data in Pandas DataFrames.
- be able to do some EDA on a new dataset
- know how to plot some basic plots for better data understanding



Let start with [Introduction to Pandas](01_pandas.ipynb)




