# pgAdmin 4 on Ubuntu

> Target audience: Students using **Ubuntu** desktop or server (for web mode).
> Goal: Install **pgAdmin 4** from its official APT repository and launch (Desktop or Web).

---

## 1) Add the pgAdmin APT repository

```bash
# Install prerequisites
sudo apt update
sudo apt install -y curl ca-certificates gnupg lsb-release

# Add the pgAdmin repository key
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub \
  | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg

# Add the repository (uses your Ubuntu codename automatically)
echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] \
https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" \
| sudo tee /etc/apt/sources.list.d/pgadmin4.list > /dev/null

sudo apt update
```

> Commands come directly from the official pgAdmin APT page.

---

## 2) Install pgAdmin 4

Choose one:

* **Desktop mode (GUI app):**

  ```bash
  sudo apt install -y pgadmin4-desktop
  ```

* **Web mode (served in browser):**

  ```bash
  sudo apt install -y pgadmin4-web
  sudo /usr/pgadmin4/bin/setup-web.sh
  ```

* **Both desktop + web modes:**

  ```bash
  sudo apt install -y pgadmin4
  ```

---

## 3) Launch

* **Desktop:** Open your applications menu and search for **pgAdmin 4**.
* **Web:** Navigate to:

  ```
  http://localhost/pgadmin4
  ```

---

## References (Official)

* pgAdmin 4 — **APT (Debian/Ubuntu) install**: [https://www.pgadmin.org/download/pgadmin-4-apt/](https://www.pgadmin.org/download/pgadmin-4-apt/)
* pgAdmin 4 — Downloads overview: [https://www.pgadmin.org/download/](https://www.pgadmin.org/download/)