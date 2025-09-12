# pyenv-win on Windows — Install & Set Up

> Target: **Windows 10/11 (64-bit)**
> Goal: Install **pyenv-win**, add it to your environment so it works in new terminals, and verify.

---

## 1) Install pyenv-win (PowerShell — official method)

Open **PowerShell** (you can run as Admin if your execution policy blocks scripts) and run:

```powershell
Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"
```

If you hit a policy error, start PowerShell **as Administrator** and run:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine
```

…then rerun the install command. (This is the **PowerShell** method recommended by pyenv-win.) ([pyenv-win.github.io][1])

---

## 2) Add environment variables (one-time)

Use the official commands to add the variables and PATH entries **for your user**:

```powershell
[System.Environment]::SetEnvironmentVariable('PYENV',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
[System.Environment]::SetEnvironmentVariable('PYENV_ROOT',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
[System.Environment]::SetEnvironmentVariable('PYENV_HOME',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")

[System.Environment]::SetEnvironmentVariable('path', $env:USERPROFILE + "\.pyenv\pyenv-win\bin;" + $env:USERPROFILE + "\.pyenv\pyenv-win\shims;" + [System.Environment]::GetEnvironmentVariable('path', "User"),"User")
```

If you can’t run PowerShell commands on a managed device, set the same values via **Settings → System → About → Advanced system settings → Environment Variables** (User variables). ([pyenv-win.github.io][1])

---

## 3) Restart your terminal & handle Windows Python aliases

Close and reopen **PowerShell / Command Prompt**.
If `python` still launches the Microsoft Store app, disable the **App Installer aliases**:

* **Start → “Manage App Execution Aliases”** → turn **off** the Python aliases. ([pyenv-win.github.io][1])

---

## 4) Verify pyenv-win

```powershell
pyenv --version
pyenv install -l | Select-Object -First 10
```

(If `pyenv` isn’t found, recheck Step 2.) ([pyenv-win.github.io][1])

---

## References (Official)

* **pyenv-win — Installation & System Settings** (PowerShell, env vars, aliases). ([pyenv-win.github.io][1])
* **pyenv (upstream) note on Windows** (use pyenv-win on Windows). ([GitHub][2])

---


[1]: https://pyenv-win.github.io/pyenv-win/docs/installation.html "Installation | pyenv-win"
[2]: https://github.com/pyenv/pyenv "pyenv/pyenv: Simple Python version management"
[3]: https://www.python.org/downloads/release/python-31113/ "Python Release Python 3.11.13"
[4]: https://stackoverflow.com/questions/63941443/local-python-version-not-changing-after-installing-pyenv-win "Local python version not changing after installing pyenv-win"
[5]: https://www.python.org/downloads/ "Download Python"
[6]: https://docs.python.org/3/using/windows.html "4. Using Python on Windows"
