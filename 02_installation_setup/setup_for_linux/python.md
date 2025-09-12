# Python 3.11.x via pyenv on Ubuntu — Install & Verify

> Target: **Ubuntu** (incl. WSL).
> Goal: Use **pyenv** to install a stable Python **3.11.x** without touching the system Python.
> Prereq: pyenv installed and configured (see `install-pyenv-ubuntu.md`).

---

## 1) Pick a 3.11 release

As of today, the latest security release in the 3.11 line is **3.11.13** (June 3, 2025). You may install **that** or any specific 3.11.x required by your course (e.g., **3.11.3** for matching screenshots). ([Python.org][4])

* To always get the **latest 3.11.x**, you can also let pyenv auto-resolve by installing **`3.11`** (prefix resolution). ([GitHub][3])

---

## 2) Install Python

Choose **one** of the following:

```bash
# Option A: Install a specific patch release
pyenv install 3.11.13

# Option B: Install the latest 3.11.x known to pyenv (prefix auto-resolution)
pyenv install 3.11
```

This downloads and compiles Python (first time takes a few minutes). If compilation errors mention SSL/zlib/etc., re-check you installed the build deps from the pyenv wiki. ([GitHub][1])

<p align="center">
  <img src="asset/Python_Done.png" alt="Python installation finished" width="60%" />
</p>

---

## 3) Make it your default (for your user)

```bash
pyenv global 3.11.13    # or: pyenv global 3.11
```

---

## 4) Verify

```bash
python --version
python -c "import sys; print(sys.executable)"
```

Expected: `Python 3.11.x` and an executable path under `~/.pyenv/versions/...`.

<p align="center">
  <img src="asset/Install.png" alt="Verify Python version" width="60%" />
</p>

---

## 5) Useful variations

```bash
pyenv versions     # list installed versions
pyenv install -l   # list all available versions
pyenv shell 3.11.13   # use for this shell only
pyenv local 3.11.13   # write .python-version in current project
```

Pyenv supports prefix auto-resolution (e.g., `3.11`) to track the latest in a minor line. ([GitHub][3])

---

## Notes

* If your screenshots mention **3.11.3**, that’s fine for class. Replace `3.11.13` with `3.11.3` in commands to match the images.
* After changing versions, you can run `pyenv rehash` if a tool complains (pyenv normally handles this automatically).

---

## References (Official)

* **Python 3.11.13 release page** (latest 3.11.x at time of writing): ([Python.org][4])
* **Python docs by version** (see 3.11.x entries): ([Python.org][5])
* **pyenv README** (install/usage, prefix auto-resolution): ([GitHub][3])
* **pyenv wiki – Suggested build environment (Ubuntu/Debian)**: ([GitHub][1])


[1]: https://github.com/pyenv/pyenv/wiki "Home · pyenv/pyenv Wiki · GitHub"
[2]: https://github.com/pyenv/pyenv-installer "This tool is used to install `pyenv` and friends."
[3]: https://github.com/pyenv/pyenv "GitHub - pyenv/pyenv: Simple Python version management"
[4]: https://www.python.org/downloads/release/python-31113 "Python Release Python 3.11.13"
[5]: https://www.python.org/doc/versions "Python Documentation by Version"
