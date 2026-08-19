# pgAdmin 4 on Ubuntu

> Target audience: Students using **Ubuntu** desktop (including WSL with WSLg).
> Goal: Install **pgAdmin 4** (desktop mode) from its official APT repository, launch it, and connect to your local PostgreSQL server.

---

## 1) Add the pgAdmin APT repository

Commands below are exactly as published on the official pgAdmin APT page:

```bash
# Install prerequisites
sudo apt update
sudo apt install -y curl ca-certificates gnupg lsb-release

# Create the keyring directory (harmless if it already exists)
sudo mkdir -p /etc/apt/keyrings

# Install the public key for the repository
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub \
  | sudo gpg --dearmor -o /etc/apt/keyrings/packages-pgadmin-org.gpg

# Create the repository configuration file (uses your Ubuntu codename automatically)
sudo sh -c 'echo "deb [signed-by=/etc/apt/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
```

> Note: the pgAdmin APT repo supports specific Ubuntu releases — check the supported-platforms table on the official page if you're on a very new release. ([pgadmin.org][1])

---

## 2) Install pgAdmin 4 (desktop mode — recommended for this course)

```bash
sudo apt install -y pgadmin4-desktop
```

Other options (not needed for the course):

* **Both desktop + web modes:** `sudo apt install -y pgadmin4`
* **Web mode only:** `sudo apt install -y pgadmin4-web && sudo /usr/pgadmin4/bin/setup-web.sh` (requires a configured web server; served at `http://localhost/pgadmin4`)

---

## 3) Launch

Open your applications menu and search for **pgAdmin 4**.

On first launch you may be asked to set a **Master Password** — it protects passwords you save in pgAdmin. Set it and keep it safe. ([pgadmin.org][3])

---

## 4) Connect pgAdmin to your local PostgreSQL

Ubuntu's PostgreSQL packages create the `postgres` superuser **without a password**, but pgAdmin connects over TCP and must authenticate — so set a password first:

```bash
sudo -u postgres psql -c "ALTER USER postgres PASSWORD 'choose-a-password';"
```

Then in pgAdmin:

1. Right-click **Servers → Register → Server…** (or **Add New Server**).
2. **General → Name:** `Local` (any name).
3. **Connection → Host:** `localhost` | **Port:** `5432` | **Maintenance DB:** `postgres`
4. **Username:** `postgres` — **Password:** the one you just set.
5. **Save** — your databases appear under the server node.

---

## Troubleshooting

* **`Error: Unable to locate package pgadmin4-desktop`** → the repo wasn't added correctly; re-run Step 1 and check `sudo apt update` output for errors on the pgAdmin line.
* **Connection fails with "password authentication failed"** → you skipped the `ALTER USER` command above, or typed a different password in pgAdmin.
* **Connection refused** → PostgreSQL isn't running: `sudo systemctl start postgresql` (WSL without systemd: `sudo service postgresql start`).

---

## References (Official)

* pgAdmin 4 — **APT (Debian/Ubuntu) install** (repo key, sources line, packages). ([pgadmin.org][1])
* pgAdmin 4 — Downloads overview. ([pgadmin.org][2])
* pgAdmin docs — **Master Password**. ([pgadmin.org][3])

[1]: https://www.pgadmin.org/download/pgadmin-4-apt/ "pgAdmin 4 (APT)"
[2]: https://www.pgadmin.org/download/ "pgAdmin Downloads"
[3]: https://www.pgadmin.org/docs/pgadmin4/latest/master_password.html "Master Password — pgAdmin 4 documentation"
