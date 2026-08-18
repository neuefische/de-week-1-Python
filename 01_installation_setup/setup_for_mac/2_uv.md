# Installing uv (macOS)

## Goal

Install **uv**, the tool we use in this course to manage Python versions and
Python packages. uv replaces pyenv, pip, virtualenv and pipx with a single,
very fast tool — so this is the only thing you need to install before getting
Python itself.

## Prerequisites

- macOS with a terminal (Terminal.app, iTerm2, or the VS Code terminal)
- `curl` (preinstalled on macOS) **or** Homebrew

## Step 1: Install uv

**Option A — official installer (recommended):**

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

The installer places `uv` and `uvx` in `~/.local/bin` and adds that folder to
your `PATH`.

**Option B — Homebrew (if you already use brew):**

```bash
brew install uv
```

> Note: with the Homebrew installation, `uv self update` is disabled — you
> update with `brew upgrade uv` instead.

## Step 2: Reload your shell

Close and reopen your terminal — or load the new `PATH` directly:

```bash
source $HOME/.local/bin/env
```

(Not needed for the Homebrew option — brew's bin folder is already on your
`PATH`.)

## Step 3: Verify the installation

```bash
uv --version
```

You should see something like `uv 0.x.y`. If you get `command not found`,
repeat Step 2 and make sure `~/.local/bin` is on your `PATH`.

## Keeping uv up to date

```bash
uv self update        # official installer
brew upgrade uv       # Homebrew installation
```

## Troubleshooting

- **`uv: command not found`** → your shell has not picked up the new `PATH`.
  Run `source $HOME/.local/bin/env` or restart the terminal.
- **Previously installed pyenv?** → you no longer need it. uv manages Python
  versions on its own and needs neither pyenv nor its build dependencies.
  Removing pyenv is optional — uv and pyenv can coexist.

## Next step

➡️ Continue with [3_python.md](3_python.md) to install Python using uv.
