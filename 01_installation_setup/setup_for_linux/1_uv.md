# Installing uv (Linux / Ubuntu)

## Goal

Install **uv**, the tool we use in this course to manage Python versions and
Python packages. uv replaces pyenv, pip, virtualenv and pipx with a single,
very fast tool — so this is the only thing you need to install before getting
Python itself.

## Prerequisites

- Ubuntu (or another Debian-based Linux) with a terminal
- `curl` — check with:

```bash
curl --version
```

If `curl` is missing, install it first:

```bash
sudo apt update && sudo apt install curl -y
```

## Step 1: Install uv

Run the official installer:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

> No `curl`? Use `wget` instead:
>
> ```bash
> wget -qO- https://astral.sh/uv/install.sh | sh
> ```

The installer places `uv` and `uvx` in `~/.local/bin` and adds that folder to
your `PATH`. No `sudo` required.

## Step 2: Reload your shell

Close and reopen your terminal — or load the new `PATH` directly:

```bash
source $HOME/.local/bin/env
```

## Step 3: Verify the installation

```bash
uv --version
```

You should see something like `uv 0.x.y`. If you get `command not found`,
repeat Step 2 and make sure `~/.local/bin` is on your `PATH`.

## Keeping uv up to date

```bash
uv self update
```

## Troubleshooting

- **`uv: command not found`** → your shell has not picked up the new `PATH`.
  Run `source $HOME/.local/bin/env` or restart the terminal.
- **Installer fails with network errors** → check proxy/VPN settings, or try
  the `wget` variant above.
- **Previously installed pyenv?** → you no longer need it. uv manages Python
  versions on its own, and it does not need the pyenv build dependencies
  (`build-essential`, `libssl-dev`, ...). Removing pyenv is optional — uv and
  pyenv can coexist.

## Next step

➡️ Continue with [2_python.md](2_python.md) to install Python using uv.
