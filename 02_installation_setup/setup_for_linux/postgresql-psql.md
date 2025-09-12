# PostgreSQL + psql on Ubuntu 

> Target audience: Students using **Ubuntu** (including WSL).
> Goal: Install **PostgreSQL 16** and the **psql** client from the official PostgreSQL (PGDG) repository, then verify.

---

## 1) Add the official PostgreSQL Apt repository (PGDG)

Use the official helper script (simplest):

```bash
sudo apt update
sudo apt install -y postgresql-common
sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh
```

> This configures the PGDG repo for your Ubuntu release. Commands are taken from the official PostgreSQL “Linux downloads (Ubuntu)” page.

---

## 2) Install PostgreSQL 16 and the client

```bash
sudo apt update
sudo apt install -y postgresql-16 postgresql-client-16
sudo systemctl enable --now postgresql
```

What you get:

* **PostgreSQL 16** server
* **psql 16** client
* Service started and enabled at boot

<p align="center">
   <img src="Assets_Linux/postgrescommands.png" alt="" width="60%" />
</p>

---

## 3) Verify

```bash
psql --version
sudo systemctl status postgresql --no-pager
sudo -u postgres psql -c "SELECT version();"
```

Expected: `psql (PostgreSQL) 16.x` and a running service.

<p align="center">
   <img src="Assets_Linux/Pg16Installed.png" alt="" width="60%" />
</p>

---

## Notes

* If you only need the client tools on your workstation, install just:

  ```bash
  sudo apt install -y postgresql-client-16
  ```
* If a different major version is required later, replace `16` with that version (e.g., `postgresql-17`, `postgresql-client-17`).

---

## References (Official)

* PostgreSQL — **Linux downloads (Ubuntu)**: [https://www.postgresql.org/download/linux/ubuntu/](https://www.postgresql.org/download/linux/ubuntu/)
* PGDG Apt repository wiki: [https://wiki.postgresql.org/wiki/Apt](https://wiki.postgresql.org/wiki/Apt)
* Ubuntu Server docs — Install PostgreSQL: [https://documentation.ubuntu.com/server/how-to/databases/install-postgresql/](https://documentation.ubuntu.com/server/how-to/databases/install-postgresql/)

