# pyenv on Ubuntu — Install & Set Up

> Target: **Ubuntu** (incl. WSL).
> Goal: Install **pyenv**, add it to your shell so it works in new terminals, and verify.

---

## 1) Install build tools (required later for building Python)

```bash
sudo apt update
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
  libbz2-dev libreadline-dev libsqlite3-dev curl git \
  libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev \
  libffi-dev liblzma-dev
```

These are the official dependencies recommended for Ubuntu/Debian in the pyenv wiki. ([GitHub][1])

---

## 2) Install pyenv (official installer)

```bash
curl https://pyenv.run | bash
```

This runs the official **pyenv-installer** script. ([GitHub][2])

---

## 3) Add pyenv to your shell (Bash on Ubuntu)

Append the recommended lines to **both** `~/.bashrc` (interactive shells) **and** your **login** profile (`~/.profile` on Ubuntu). This mirrors pyenv’s current README guidance. ([GitHub][3])

```bash
# Add to ~/.bashrc
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init - bash)"' >> ~/.bashrc

# Add to ~/.profile (login shells)
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init - bash)"' >> ~/.profile
```

<p align="center">
  <img src="asset/Scroll.png" alt="Add lines to shell config" width="60%" />
</p>

Apply changes:

```bash
exec "$SHELL"    # or: source ~/.bashrc
```

> Note: Some systems behave differently; pyenv documents when to prefer putting the `eval` line in `~/.bash_profile` instead of `~/.bashrc`. The above layout matches typical Ubuntu behavior. ([GitHub][3])

---

## 4) Verify pyenv

```bash
which pyenv
pyenv --version
```

You should see a valid path (e.g., `~/.pyenv/bin/pyenv`) and a version number.

---

## References (Official)

* **pyenv README** (shell setup & usage): ([GitHub][3])
* **pyenv-installer** (installer script: `curl https://pyenv.run | bash`): ([GitHub][2])
* **pyenv wiki – Suggested build environment (Ubuntu/Debian)**: ([GitHub][1])

---

[1]: https://github.com/pyenv/pyenv/wiki "Home · pyenv/pyenv Wiki · GitHub"
[2]: https://github.com/pyenv/pyenv-installer "This tool is used to install `pyenv` and friends."
[3]: https://github.com/pyenv/pyenv "GitHub - pyenv/pyenv: Simple Python version management"
[4]: https://www.python.org/downloads/release/python-31113 "Python Release Python 3.11.13"
[5]: https://www.python.org/doc/versions "Python Documentation by Version"
