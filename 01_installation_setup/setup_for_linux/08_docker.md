# Docker on Ubuntu/Debian — Install & Verify (Engine) + Optional Desktop

> Target audience: Students using **Ubuntu** or **Debian** on a real machine or VM.
> Goal: Install **Docker Engine** from Docker’s official repo, verify it, and (optionally) set up non-root use. A brief optional section covers **Docker Desktop for Linux**.

---

## 1) Prerequisites (quick)

* Use a **supported** Ubuntu/Debian release (e.g., Ubuntu 24.04/22.04 LTS; Debian 12/11). See the official OS lists if unsure. ([Docker Documentation][1])
* You need **sudo** privileges.
* If you previously installed community packages (like `docker.io`), **remove conflicts** first:

```bash
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do
  sudo apt-get remove -y $pkg || true
done
```

This matches Docker’s guidance to remove conflicting packages before installing the official ones. ([Docker Documentation][2])

---

## 2) Install Docker Engine from Docker’s official apt repo

The following works for **both Ubuntu and Debian** by reading `/etc/os-release`.

```bash
# 2.1 Required packages
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg

# 2.2 Add Docker’s official GPG key (into keyrings path)
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL "https://download.docker.com/linux/$(. /etc/os-release && echo "$ID")/gpg" \
  | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# 2.3 Add the Docker apt repository
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/$(. /etc/os-release && echo "$ID") \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 2.4 Install Docker Engine, CLI, containerd, Buildx & Compose v2
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# 2.5 Ensure the service starts now and on boot (systemd distros)
sudo systemctl enable --now docker
```

These steps follow Docker’s current Ubuntu/Debian install guides, including the keyring path and Compose v2 plugin. ([Docker Documentation][1])

---

## 3) Verify your installation

```bash
docker --version
docker compose version
sudo docker run --rm hello-world   # first run works with sudo for everyone
```

You should see version info and a “Hello from Docker!” message. ([Docker Documentation][1])

---

## 4) (Recommended) Use Docker without `sudo`

Add your user to the `docker` group, then **re-login** (or run `newgrp docker`) so your session picks up the change:

```bash
# Create group if it doesn't exist (harmless if it already exists)
sudo groupadd docker 2>/dev/null || true

# Add your user to the group
sudo usermod -aG docker $USER

# Start a new shell with the new group (or log out/in)
newgrp docker

# Test without sudo
docker run --rm hello-world
```

Note: membership in `docker` grants root-equivalent access; review the security note in Docker’s post-install docs. ([Docker Documentation][3])

---

## 5) Optional: Docker Desktop for Linux (GUI)

Most course work only needs **Docker Engine**. If you want the Desktop app (GUI, integrated Kubernetes, etc.):

* **Check system requirements** (KVM virtualization, QEMU ≥ 5.2, systemd, supported desktop environment). ([Docker Documentation][4])
* Follow the **Ubuntu** or **Debian** Desktop guides:

  * Ubuntu: download the `.deb` and install with `sudo apt-get install ./docker-desktop-<version>-<arch>.deb`. ([Docker Documentation][5])
  * Debian: similar flow for Debian. ([Docker Documentation][6])

Docker Desktop includes Docker Engine; licensing terms may apply for larger enterprises. ([Docker Documentation][4])

---

## References (Official)

* **Install Docker Engine on Ubuntu** — Docker Docs. ([Docker Documentation][1])
* **Install Docker Engine on Debian** — Docker Docs. ([Docker Documentation][2])
* **Linux post-installation (non-root use, security note)** — Docker Docs. ([Docker Documentation][3])
* **Docker Desktop on Linux (requirements)** — Docker Docs. ([Docker Documentation][4])
* **Docker Desktop on Ubuntu / Debian** — Docker Docs. ([Docker Documentation][5])

---

### Scope

This page focuses on **Ubuntu/Debian** to keep the setup consistent for students. Other distros can be added later in a separate appendix if needed.

[1]: https://docs.docker.com/engine/install/ubuntu "Install Docker Engine on Ubuntu"
[2]: https://docs.docker.com/engine/install/debian "Install Docker Engine on Debian"
[3]: https://docs.docker.com/engine/install/linux-postinstall "Linux post-installation steps for Docker Engine"
[4]: https://docs.docker.com/desktop/setup/install/linux "Install Docker Desktop on Linux"
[5]: https://docs.docker.com/desktop/setup/install/linux/ubuntu "Install Docker Desktop on Ubuntu"
[6]: https://docs.docker.com/desktop/setup/install/linux/debian "Install Docker Desktop on Debian"
