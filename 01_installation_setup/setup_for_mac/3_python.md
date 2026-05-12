# Python 3.11.x via uv on macOS — Install & Verify
> Target: **macOS** (Apple Silicon or Intel).
> Goal: Use **uv** to install a stable Python **3.11.x** without touching the system Python.
> Prereq: uv installed (see installation instructions at https://docs.astral.sh/uv/getting-started/installation/).
---
## 1) Pick a 3.11 release
As of now, the latest 3.11 security release is **3.11.13** (June 3, 2025). For strict reproducibility with course materials, you may install **3.11.3** instead—both work the same way.

> Tip: uv supports **prefix auto-resolution**; specifying `3.11` resolves to the latest 3.11.x known to uv.
---
## 2) Install Python with uv
Choose **one**:
```bash
# A) Install a specific patch release
uv python install 3.11.13

# B) Install the latest 3.11.x via prefix
uv python install 3.11
```
> uv downloads and manages Python versions automatically — no need to install build dependencies manually.
---
## 3) Create a virtual environment with that version
```bash
uv venv --python 3.11.13
```
You can also pin a version per project by adding a `.python-version` file:
```bash
echo "3.11.13" > .python-version
```
uv will automatically pick this up when creating environments in that directory.

---
## 4) Activate the environment
* **macOS**
  ```bash
  source .venv/bin/activate
  ```
---
## 5) Verify
```bash
python --version
python -c "import sys,platform; print(sys.executable, platform.python_version())"
```
Expected: `Python 3.11.x` and an executable under `.venv/bin/python`.

---
## 6) Useful commands
```bash
uv python list                  # list all available Python versions
uv python list --only-installed # list installed versions
uv python find                  # show the resolved interpreter path
```
---
## References (Official)
* **Python 3.11.13 release page** (current 3.11.x). https://www.python.org/downloads/release/python-31113/
* **uv documentation** (Python version management). https://docs.astral.sh/uv/concepts/python-versions/
* **uv installation guide**. https://docs.astral.sh/uv/getting-started/installation/

