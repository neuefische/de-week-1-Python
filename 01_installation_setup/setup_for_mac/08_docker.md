# Docker Desktop on macOS — Install & Verify

> Target audience: Students using **macOS** (Apple Silicon or Intel).
> Goal: Install **Docker Desktop**, confirm it runs, and know when to use **Rosetta** for x86/amd64 images.

---

## 1) System requirements (quick)

* **macOS:** Docker Desktop supports the **current and previous two major macOS releases**.
* **RAM:** At least **4 GB**.
* **Chip:** Download the correct installer for **Apple silicon** or **Intel**. ([Docker Documentation][1])

> On Apple silicon, **Rosetta 2** is **recommended** (not strictly required). Some optional CLI tools and x86/amd64 images may need it. Install manually if prompted:
> `softwareupdate --install-rosetta` ([Docker Documentation][1])

---

## 2) Install Docker Desktop (interactive)

1. Download **Docker Desktop for Mac** (choose Apple silicon or Intel). ([Docker][2])
2. Open the downloaded **`Docker.dmg`** and **drag Docker** to **Applications**.
3. Open **Applications → Docker.app**. Accept the subscription terms and complete any prompts. ([Docker Documentation][1])

<p align="center">

<img src="asset/Docker_mac.png" alt="Docker Desktop for Mac" />

</p>


---

## 3) (Alternative) Install from the command line

If you’ve downloaded `Docker.dmg`, you can install via Terminal:

```bash
sudo hdiutil attach Docker.dmg
sudo /Volumes/Docker/Docker.app/Contents/MacOS/install
sudo hdiutil detach /Volumes/Docker
```

This places Docker at `/Applications/Docker.app`. First run security checks can take a few minutes. ([Docker Documentation][1])

---

## 4) Verify

Open a new Terminal and run:

```bash
docker --version
docker info
docker run --rm hello-world
```

You should see version info and “**Hello from Docker!**”. ([Docker Hub][3])

---

## 5) Running x86/amd64 images on Apple silicon (Rosetta)

Most popular images have **arm64** variants and run natively on Apple silicon. If you must run **amd64** images:

* Enable **Rosetta for Linux** in **Docker Desktop → Settings → General** (enabled by default on macOS 14.1+).
* Requires **macOS 13+** on Apple silicon. ([Docker][4])

If macOS asks to install **Rosetta 2**, confirm or run:

```bash
softwareupdate --install-rosetta
```

(Apple’s official Rosetta instructions.) ([Apple Support][5])

---

## Notes & common gotchas

* If Docker doesn’t start after a macOS update, **update Docker Desktop** to the latest release and relaunch. ([Docker][6])
* Larger enterprises (≥250 employees **or** ≥\$10M USD revenue) need a **paid** Docker Desktop subscription for commercial use. Education/personal use is free. Accept the terms on first run. ([Docker Documentation][1])

---

## References (Official)

* **Install Docker Desktop on Mac** — system requirements, DMG install, CLI install: ([Docker Documentation][1])
* **Docker Desktop product page** — downloads for Apple silicon/Intel: ([Docker][2])
* **hello-world image** — verification: ([Docker Hub][3])
* **Rosetta for Linux in Docker Desktop** — availability and defaults: ([Docker][4])
* **Apple Support: Install Rosetta** — command and behavior: ([Apple Support][5])

---

### Scope

This page is macOS-only to keep setup consistent. If you need Docker **Engine** on Linux or Docker Desktop on Windows/Linux, use the corresponding OS pages in this course.

[1]: https://docs.docker.com/desktop/setup/install/mac-install/ "Mac | Docker Docs
"
[2]: https://www.docker.com/products/docker-desktop/ "The #1 Containerization Tool for Developers"
[3]: https://hub.docker.com/_/hello-world "hello-world - Official Image"
[4]: https://www.docker.com/blog/docker-desktop-4-25/ "Enhanced productivity and speed with Rosetta for Linux GA"
[5]: https://support.apple.com/en-us/102527 "If you need to install Rosetta on Mac"
[6]: https://www.docker.com/blog/incident-update-docker-desktop-for-mac/ "Incident Update: Docker Desktop for Mac"
