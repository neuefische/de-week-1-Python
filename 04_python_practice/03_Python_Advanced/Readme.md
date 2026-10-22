# 🚀 Python Advanced

This folder builds on **Intermediate Python** and focuses on **Object-Oriented Design (OOP)** and **Concurrency/Parallelism**—key skills for real-world data engineering tasks.

> 💻 You’ll commit your progress and submit via **PR** using the Day-3 Git workflow.

---

## 🎯 What You’ll Learn

### 🏗 Object-Oriented Programming (OOP)

* Classes vs instances  
* Data model methods: `__repr__`, `__eq__`, ordering, hashing  
* Properties, `@classmethod`, `@staticmethod`  
* Inheritance vs composition  
* Abstract base classes, protocols & typing  
* Context-manager classes (`with`)  
* Common patterns: strategy, registry  

### ⚡ Concurrency & Parallelism

* Threads vs processes vs `asyncio`  
* Executors, queues, and synchronization (locks/semaphores)  
* Cancellation & timeouts  
* Choosing the right model: **I/O-bound vs CPU-bound**  
* Mixing concurrency models safely  

---

## 📝 Prerequisites

* Completion of **Python Intermediate** (exceptions, iterators/generators, functional patterns, basic performance techniques)  
* A project environment created with **uv**, selected as your Jupyter kernel (see `02_Installation_and_setup/`)  

---

## 🏁 Getting Started

1. Open this folder in **VS Code** or **JupyterLab**  
2. Activate your **virtual environment** and select it as the kernel  
3. Open a notebook and run cells with **Shift + Enter**  

> 💡 **Tip:** Commit per section. Always **Restart Kernel → Run All** to ensure clean notebooks before committing.

---

## 📚 Notebooks (Recommended Order)

1. [Introduction to OOP](./Introduction_to_Oops.ipynb)  
2. [Concurrency and Parallelism](./Concurrency_and_parallelism.ipynb)  

---

## 🛠 Exercises

Each notebook has matching practice tasks in the `Exercises/` folder:

* `Exercises/Introduction_to_Oops_exercises.md`  
* `Exercises/Concurrency_and_parallelism_exercises.md`  

> ✅ Complete exercises **after each notebook section**, then push your branch and open a PR.

---

## 📝 Submission Notes

* Prefer **pure functions** where possible; isolate side effects  
* Add comments explaining **which concurrency model** you chose (threads, processes, or async) and why (I/O- vs CPU-bound)  
* On **Windows/macOS**, remember the `if __name__ == "__main__":` guard for multiprocessing scripts  

---

✨ Ready to level up? These notebooks will equip you with **real-world Python skills** for building high-performance, scalable data pipelines! 🐍💻⚡

