# Python Advanced

This folder builds on Intermediate concepts and focuses on **object-oriented design** and **concurrency/parallelism** for real data-engineering tasks.

You’ll commit progress and submit via PR using the Day-3 Git workflow.

## What you’ll learn

* **OOP**: classes vs instances, data model methods (`__repr__`, `__eq__`, ordering, hashing), properties, class/staticmethods, inheritance vs composition, abstract base classes, protocols & typing, context-manager classes, basic patterns (strategy/registry).
* **Concurrency & parallelism**: threads vs processes vs `asyncio`, executors, queues, synchronization (locks/semaphores), cancellation & timeouts, when to use each (I/O-bound vs CPU-bound), mixing models safely.

## Prerequisites

* Completed **Python Intermediate** (exceptions, iterators/generators, functional patterns, basic perf).
* Python **3.11.x** in a project **venv** selected as the kernel (see `02_Installation_and_setup/`).

## Getting started

1. Open this folder in VS Code (or JupyterLab).
2. Ensure your venv is active and selected as the kernel.
3. Open a notebook and run cells with **Shift+Enter**.

> Tip: Commit per section. Ensure notebooks **Restart & Run All** cleanly before committing.

## Notebooks (recommended order)

1. [Introduction to OOPs](./Introduction_to_Oops.ipynb)
2. [Concurrency and Parallelism](./Concurrency_and_parallelism.ipynb)

## Exercises

Each topic has a matching set of practice tasks in `Exercises/`:

* `exercise/Introduction_to_Oops_exercises.md`
* `exercise/Concurrency_and_parallelism_exercises.md`

Complete exercises after each notebook section, then push your branch and open a PR.

---

### Submission notes

* Prefer **pure functions** where possible; isolate side effects.
* Add comments explaining which model you chose (threads/processes/async) and why (I/O- vs CPU-bound).
* For multiprocessing on Windows/macOS, remember the `if __name__ == "__main__":` guard when running as a script.
