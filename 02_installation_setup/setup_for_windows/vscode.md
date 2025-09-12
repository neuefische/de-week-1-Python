# VS Code on Windows — Install & Verify

> Target audience: Students on **Windows 10/11**.
> Goal: Install **Visual Studio Code**, ensure the **`code`** command is on your PATH, enable Explorer context-menu items, and verify.

---

## Option A — Download installer (GUI)

1. Go to the official site and click **Download for Windows**:
   [https://code.visualstudio.com/](https://code.visualstudio.com/) ([Visual Studio Code][1])

2. Run the downloaded **`.exe`**.

<p align="center">
  <img src="asset/7--Wait.png" alt="" width="60%" />
</p>

3. **During installation**, make sure these are selected (they usually are by default):

   * **Add to PATH** (lets you run `code` from the terminal)
   * **Add ‘Open with Code’ to context menu** (files & folders)

<p align="center">
  <img src="asset/5--Click-Next.png" alt="" width="60%" />
</p>

> The Windows setup **adds VS Code to your `%PATH%`** so you can run `code .` from a folder. Open a **new** terminal after install so the PATH refreshes. ([Visual Studio Code][1])

4. Click **Install**, then finish the wizard.

<p align="center">
  <img src="asset/8--Finish.png" alt="" width="60%" />
</p>

5. Launch **Visual Studio Code** from the Start menu (or tick “Launch Visual Studio Code” at the end of the wizard).

---

## Option B — Install with WinGet (one-liner)

Open **PowerShell** or **Windows Terminal** and run:

```powershell
winget install -e --id Microsoft.VisualStudioCode
```

This installs the official VS Code package via Windows Package Manager. ([Microsoft Learn][2], [Winget.run][3])

---

## Verify

Open a **new** terminal and run:

```powershell
code --version
```

You should see something like `1.xx.x`. (For CLI usage tips, see VS Code’s command-line docs.) ([Visual Studio Code][4])

To open the current folder in VS Code:

```powershell
code .
```

---

## Notes & tips

* If `code` isn’t found, open a **new** terminal so the PATH updates, or re-run the installer ensuring **Add to PATH** is selected. ([Visual Studio Code][1])
* You can also get VS Code via the **Microsoft Store** if preferred. ([Microsoft GitHub][5])
* The context menu entries (“Open with Code”) are controlled by installer options; if they’re missing, reinstall and ensure those boxes are selected.

---

## References (Official)

* **Set up VS Code on Windows** — installer, PATH note: ([Visual Studio Code][1])
* **VS Code CLI** — `code` and `code .` usage: ([Visual Studio Code][4])
* **WinGet** — install and manage apps from the command line: ([Microsoft Learn][2])

---

### Scope

This page mirrors our Linux/macOS guides: **download/winget → install → PATH/context menu → verify**.

[1]: https://code.visualstudio.com/docs/setup/windows "Visual Studio Code on Windows"
[2]: https://learn.microsoft.com/en-us/windows/package-manager/winget/ "Use WinGet to install and manage applications"
[3]: https://winget.run/pkg/Microsoft/VisualStudioCode "Download and install Microsoft Visual Studio Code ..."
[4]: https://code.visualstudio.com/docs/configure/command-line "Command Line Interface (CLI)"
[5]: https://microsoft.github.io/vscode-essentials/en/01-getting-started.html "Getting started with VS Code · Visual Studio Code"
