# Bash on Ubuntu/Debian — Verify, Install, and Set as Default

> Target audience: Students using **Ubuntu** or **Debian** (including WSL).
> Goal: Confirm Bash is available, install/update if needed, and optionally set it as your default login shell.

---

## 1) Check if Bash is already installed

```bash
bash --version
command -v bash
echo "$BASH_VERSION"   # prints a value if you're already running bash
```

Expected: output like `GNU bash, version 5.x` and a path for `bash` (typically `/bin/bash`).

---

## 2) Install or update Bash (only if missing or broken)

```bash
sudo apt update
sudo apt install --yes bash
# If bash is installed but corrupted:
sudo apt --reinstall install bash
```

> Tip: If you’re running as `root` (e.g., in a minimal container), omit `sudo`.

---

## 3) Make Bash your default login shell (optional but recommended)

Set your login shell to `/bin/bash`:

```bash
chsh -s /bin/bash
```

Then **log out and back in** (or close/reopen your terminal). Verify:

```bash
echo "$SHELL"          # should show /bin/bash after re-login
getent passwd "$USER"  # last field shows your login shell
```

If `chsh` says `/bin/bash` is not listed in `/etc/shells`, add it:

```bash
grep -qxF '/bin/bash' /etc/shells || echo '/bin/bash' | sudo tee -a /etc/shells
chsh -s /bin/bash
```

---

## 4) Start a Bash session now (without changing your default)

```bash
bash
# Type 'exit' to return to your previous shell.
```

---

## Notes & Common Gotchas

* Ubuntu links `/bin/sh` to `dash` for speed. **Do not change `/bin/sh`**. Use `bash` explicitly when you need Bash features.
* Minimal Docker images or stripped-down environments may not include Bash—just install it with `apt`.
* If you see “permission denied” or “not found,” confirm the binary exists:

  ```bash
  ls -l /bin/bash
  ```

---

## References (Official)

* **GNU Bash Manual** (language, builtins, behavior):
  [https://www.gnu.org/software/bash/manual/](https://www.gnu.org/software/bash/manual/)
* **Ubuntu Manpage: `bash(1)`**:
  [https://manpages.ubuntu.com/manpages/latest/en/man1/bash.1.html](https://manpages.ubuntu.com/manpages/latest/en/man1/bash.1.html)
* **Debian Package: `bash`** (stable package info):
  [https://packages.debian.org/search?keywords=bash](https://packages.debian.org/search?keywords=bash)
* **`chsh(1)` Manpage** (change login shell):
  [https://man7.org/linux/man-pages/man1/chsh.1.html](https://man7.org/linux/man-pages/man1/chsh.1.html)
