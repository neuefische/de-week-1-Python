# Docker Desktop on Windows — Install & Verify

> Target audience: Students on **Windows 10/11**.
> Goal: Install **Docker Desktop**, make sure **WSL 2** is set up (recommended backend), and verify with `hello-world`.

---

## 1) System requirements (quick)

* **Windows 11 64-bit:** Home/Pro/Enterprise/Education **22H2 or later**
* **Windows 10 64-bit:** Home/Pro/Enterprise/Education **22H2 (build 19045) or later**
* **Backends:** **WSL 2** (recommended) or **Hyper-V** (needed for Windows containers)
* **Hardware:** 64-bit CPU with SLAT, **4 GB RAM**, virtualization enabled in BIOS/UEFI. ([Docker Documentation][1])

> Note: Docker Desktop is supported only on Windows client versions within Microsoft’s servicing timeline; Windows Server isn’t supported by Desktop. ([Docker Documentation][1])

---

## 2) Optional — Verify or install WSL 2 (recommended backend)

Open **PowerShell (Admin)** and run:

```powershell
wsl --version
wsl --install
wsl --update
```

If you’re on a managed device without Store access, you can install WSL via the **MSI** from the WSL GitHub releases page (see Docker’s WSL section). ([Docker Documentation][1])

---

## 3) Install Docker Desktop (interactive)

1. Download **Docker Desktop for Windows** (x86\_64) and run the installer:

   * From Docker’s Windows install page (Download button at top), or use the Microsoft Store listing. ([Docker Documentation][1])

2. Double-click `Docker Desktop Installer.exe` and follow the wizard.

   * On the **Configuration** step, choose **Use WSL 2 based engine** (or Hyper-V if you specifically need Windows containers).
   * Finish the install and **Start Docker Desktop**. ([Docker Documentation][1])

<p align="center">
  <img src="asset/docker-home-page.png" alt="Docker Desktop home page" />
</p>


> Admin installs for non-admin users: see installer flags like `--always-run-service` and `--accept-license` in Docker’s docs. ([Docker Documentation][1])

---

## 4) (Alternative) Install from the command line

After downloading `Docker Desktop Installer.exe`, you can install via PowerShell:

```powershell
Start-Process 'Docker Desktop Installer.exe' -Wait install
```

By default Docker Desktop installs to `C:\Program Files\Docker\Docker`. See docs for additional installer flags and automation details. ([Docker Documentation][1])

---

## 5) Start Docker Desktop

Launch **Docker Desktop** from Start, accept the **Subscription Service Agreement**, and wait for the whale icon to indicate it’s running. (Education/personal use is free; larger enterprises need a paid subscription.) ([Docker Documentation][1])

---

## 6) Verify

Open **PowerShell**, **Command Prompt**, or **Windows Terminal**, then run:

```powershell
docker --version
docker info
docker run --rm hello-world
```

You should see version info and “**Hello from Docker!**” from the `hello-world` container. ([Docker Hub][2])

---

## Notes & tips

* **WSL 2 vs Hyper-V:** Functionality is comparable; choose WSL 2 unless you specifically need **Windows containers** (which require Pro/Enterprise). You can switch between Linux/Windows containers from the Docker Desktop menu. ([Docker Documentation][1])
* **Virtualization errors:** Ensure virtualization is enabled in BIOS/UEFI and required Windows features are on; re-run WSL steps if needed. ([Docker Documentation][1])
* **Windows Terminal (nice to have):**

  ```powershell
  winget install -e --id Microsoft.WindowsTerminal
  ```

  Use it to open Ubuntu (WSL), PowerShell, etc., in tabs. (Microsoft Learn guide for using WSL with Docker.) ([Microsoft Learn][3])

---

## References (Official)

* **Install Docker Desktop on Windows** — system requirements, WSL/Hyper-V choices, installer flags, start-up. ([Docker Documentation][1])
* **Docker + WSL 2** — verification and setup guidance. ([Docker Documentation][4])
* **`hello-world` image** — verification output. ([Docker Hub][2])

---

### Scope

This page is Windows-only and mirrors our Linux/macOS guides: **requirements → (WSL 2) → install → start → verify**.

[1]: https://docs.docker.com/desktop/setup/install/windows-install/ "Windows | Docker Docs
"
[2]: https://hub.docker.com/_/hello-world "hello-world - Official Image"
[3]: https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-containers "Get started with Docker remote containers on WSL 2"
[4]: https://docs.docker.com/desktop/features/wsl/ "Docker Desktop WSL 2 backend on Windows"
