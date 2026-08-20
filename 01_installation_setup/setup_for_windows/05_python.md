# Installing Python with uv (Windows)

## Goal

Install Python using uv. You do **not** need the python.org installer, the
Microsoft Store Python, or pyenv-win — uv downloads and manages its own
standalone Python builds, and can even fetch Python automatically the first
time a project needs it.

## Prerequisites

- uv installed → see [3_uv.md](3_uv.md)

## Step 1: Install Python

Install the Python version used in this course (check with your coaches which
version that is — example with 3.13):

```powershell
uv python install 3.13
```

To install the latest available release instead:

```powershell
uv python install
```

You can install several versions side by side:

```powershell
uv python install 3.12 3.13
```

## Step 2: See what is installed

```powershell
uv python list
```

This shows the Python versions uv manages (and the ones it can still
download).


## Step 3: Verify

```powershell
uv run python --version
```

`uv run` automatically uses the pinned/managed Python — no virtual
environment activation needed.

Want a run plain `python <script_name>.py` command for running python script on your terminal instead of  `uv run <script_name>.py` as well? 

Install with:
>
> ```powershell
> uv python install 3.13 --default
> ```

## Upgrading Python later

```powershell
uv python upgrade 3.13   # newest patch release of 3.13
```

## Troubleshooting

- **`python` opens the Microsoft Store** → Windows ships "App execution
  aliases" that hijack the `python` command. Go to
  *Settings → Apps → Advanced app settings → App execution aliases* and
  switch **off** the entries for `python.exe` and `python3.exe`. Using
  `uv run python` avoids this problem entirely.
- **Wrong Python is used** → uv prefers its own managed Pythons, but falls
  back to a system Python if one exists. Force managed Python with
  `uv run --managed-python ...` or check `uv python list`.
- **Old pyenv-win shims interfere** → if `where python` still points into
  `%USERPROFILE%\.pyenv`, remove the pyenv-win entries from your `PATH`
  environment variable and restart the terminal. uv does not need pyenv-win.

## Next step

➡️ Python is ready — head back to the main setup guide.
