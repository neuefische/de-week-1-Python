# Installing Python with uv (macOS)

## Goal

Install Python using uv. You do **not** need the python.org installer,
`brew install python`, or pyenv — uv downloads and manages its own standalone
Python builds, and can even fetch Python automatically the first time a
project needs it.

## Prerequisites

- uv installed → see [2_uv.md](2_uv.md)

## Step 1: Install Python

Install the Python version used in this course (check with your coaches which
version that is — example with 3.13):

```bash
uv python install 3.13
```

To install the latest stable release instead:

```bash
uv python install
```

You can install several versions side by side:

```bash
uv python install 3.12 3.13
```

## Step 2: See what is installed

```bash
uv python list
```

This shows the Python versions uv manages (and the ones it can still
download).


## Step 3: Verify

```bash
uv run python --version
```

`uv run` automatically uses the pinned/managed Python — no virtual
environment activation needed.

Want a run plain `python <script_name>.py` command for running python script on your terminal instead of  `uv run <script_name>.py` as well? 

Install with:
>
> ```bash
> uv python install 3.13 --default
> ```

If `python --version` then says `command not found`, the bin folder is missing
from your `PATH`. Fix it once:

```bash
uv python update-shell
```

Then **close and reopen the terminal** and check again:

```bash
python --version
```

**Note**: this step is optional — `uv run python ...` works without any PATH changes. You only need it if you want to type bare `python`.

## Upgrading Python later

```bash
uv python upgrade 3.13   # newest patch release of 3.13
```

## Troubleshooting

- **Wrong Python is used** → uv prefers its own managed Pythons, but falls
  back to system Python (e.g. the macOS `/usr/bin/python3`). Force managed
  Python with `uv run --managed-python ...` or check `uv python list`.
- **Old pyenv shims interfere** → if `which python` still points into
  `~/.pyenv`, remove the pyenv lines from `~/.zshrc` and restart the
  terminal. uv does not need pyenv.

## Next step

➡️ Python is ready — head back to the main setup guide.
