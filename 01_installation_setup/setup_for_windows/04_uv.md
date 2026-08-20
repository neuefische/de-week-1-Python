# Installing uv (Windows)

## Goal

Install **uv**, the tool we use in this course to manage Python versions and
Python packages. uv replaces pyenv, pip, virtualenv and pipx with a single,
very fast tool — so this is the only thing you need to install before getting
Python itself.

## Prerequisites

- Windows 10/11 with **PowerShell**

## Step 1: Install uv

Open PowerShell and run the official installer:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

The installer places `uv.exe` and `uvx.exe` in
`C:\Users\<you>\.local\bin` and adds that folder to your user `PATH`.
No administrator rights required.

> Alternative — if you use WinGet:
>
> ```powershell
> winget install --id=astral-sh.uv -e
> ```
>
> Note: with WinGet, `uv self update` is disabled — you update with
> `winget upgrade astral-sh.uv` instead.

## Step 2: Restart the terminal

Close **all** terminal windows (and VS Code, if open) so the new `PATH` is
picked up, then open PowerShell again.

## Step 3: Verify the installation

```powershell
uv --version
```

You should see something like `uv 0.x.y`. If you get an error that `uv` is
not recognized, repeat Step 2.

## Keeping uv up to date

```powershell
uv self update
```

## Troubleshooting

- **`uv is not recognized...`** → the terminal was open during installation.
  Close and reopen it (or log out/in once) so the updated `PATH` loads.
- **Script execution is blocked** → make sure you copied the full command
  including `-ExecutionPolicy ByPass`.
- **Previously installed pyenv-win?** → you no longer need it. uv manages
  Python versions on its own. Removing pyenv-win is optional — uv and
  pyenv-win can coexist.

## Next step

➡️ Continue with [4_python.md](4_python.md) to install Python using uv.
