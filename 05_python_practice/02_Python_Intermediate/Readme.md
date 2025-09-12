# Python Intermediate

This folder contains Jupyter notebooks that build on Python Basics and prepare you for real-world data engineering tasks: clean control flow with exceptions, efficient iteration with iterators/generators, functional patterns (lambda/map/filter/reduce), and performance profiling/optimization.

You’ll commit progress and submit via PR using the Day-3 Git workflow.

## What you’ll learn

* Robust code via **error handling** (try/except/else/finally), custom exceptions, and context managers
* **Iterators & generators** for memory-efficient pipelines
* **Functional patterns**: lambda, map, filter, reduce, and when to prefer comprehensions
* **Performance**: measure first (time/space), profile, and apply targeted optimizations

## Prerequisites

* Completed “Python Basics” (or equivalent comfort with numbers, strings, `if/else`, loops, lists/sets/dicts, functions)
* Working environment: Python 3.11.x in a project **venv** selected as the Jupyter kernel (see `02_Installation_and_setup/`)

## Getting started

1. Open this folder in VS Code (or JupyterLab).
2. Ensure your venv is active and selected as the kernel.
3. Open a notebook and run cells with **Shift+Enter**.

> Tip: Commit early and often (e.g., per section). Ensure notebooks **Restart & Run All** cleanly before committing.

## Notebooks (recommended order)

1. [Error Handling in Python](./Error_Handling_in_python.ipynb)
2. [Iterators and Generators](./Iterators_and_generators.ipynb)
3. [Lambda, Map, Filter, Reduce](./Lambda_Map_Filter_Reduce.ipynb)
4. [Performance Optimization in Python](./Performance_Optimization_in_python.ipynb)

## Exercises

Each topic has a matching set of practice tasks in the `Exercises/` subfolder:

* `exercise/Error_Handling_in_python_exercises.md`
* `exercise/Iterators_and_generators_exercises.md`
* `exercise/Lambda_Map_Filter_Reduce_exercises.md`
* `exercise/Performance_Optimization_in_python_exercises.md`

Complete the exercises after each notebook section, then push your branch and open a PR.

### Submission notes

* Keep each solution **pure** where possible.
* Add micro-benchmarks (`%timeit`) and short comments explaining *why* an optimization helps.
* Ensure the notebook **Restart & Run All** passes before committing/PR.

