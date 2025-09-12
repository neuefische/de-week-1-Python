# pgAdmin 4 on Windows — Install & Launch

> Target audience: Students on **Windows 10/11** (64-bit).
> Goal: Install **pgAdmin 4** and connect to a local PostgreSQL instance.

---

## Option A — Installed with PostgreSQL (EDB)

If you **checked pgAdmin 4** during the PostgreSQL installer, it’s already installed. Launch **pgAdmin 4** from the Start menu. (The Windows installer from postgresql.org includes pgAdmin as an optional component.) ([PostgreSQL][1])

---

## Option B — Stand-alone pgAdmin installer

1. Download **pgAdmin 4 for Windows** (choose the current version). ([pgadmin.org][6])
2. Run the installer and follow the prompts.
3. Launch **pgAdmin 4** from the Start menu.

> The official pgAdmin downloads page lists supported Windows versions and provides the desktop installer. ([pgadmin.org][6])

---

## First-run behavior (Master Password)

* On recent pgAdmin releases, **Windows’ password store** is used by default in desktop mode. If it isn’t available, pgAdmin will **prompt for a Master Password** to encrypt saved server passwords. You may be asked to set or enter it on first launch. ([pgadmin.org][7])

---

## Connect pgAdmin to your local PostgreSQL

With PostgreSQL running (from the EDB install):

1. In pgAdmin, **Add New Server**.
2. **General → Name:** `Local` (any name).
3. **Connection → Host:** `localhost` | **Port:** `5432` | **Maintenance DB:** `postgres`
4. **Username:** the PostgreSQL role you’ll use (often `postgres` or your Windows username).
5. **Password:** the one you set during the PostgreSQL install.
6. Save. You should now see your databases under the server node.

---

## References (Official)

* **pgAdmin 4 for Windows — Download** (installer & support notes). ([pgadmin.org][6])
* **pgAdmin — Downloads overview**. ([pgadmin.org][8])
* **PostgreSQL — Windows installers** (pgAdmin included with EDB installer). ([PostgreSQL][1])
* **pgAdmin docs — Master Password** (Windows password store & prompts). ([pgadmin.org][7])

---

### Scope

We keep the **PostgreSQL/psql** setup separate from **pgAdmin** (GUI) to reduce confusion, just like on Linux and macOS. If you used the EDB installer and already have pgAdmin, this page serves as a connection checklist.

[1]: https://www.postgresql.org/download/windows/ "PostgreSQL: Windows installers"
[2]: https://www.enterprisedb.com/downloads/postgres-postgresql-downloads "Download PostgreSQL"
[3]: https://superuser.com/questions/576623/default-password-for-postgresql "Default password for postgreSQL"
[4]: https://www.enterprisedb.com/docs/supported-open-source/postgresql/installing/windows/ "Installing PostgreSQL on Windows"
[5]: https://www.postgresql.org/download/ "Downloads"
[6]: https://www.pgadmin.org/download/pgadmin-4-windows/ "pgAdmin 4 (Windows) Download"
[7]: https://www.pgadmin.org/docs/pgadmin4/latest/master_password.html "Master Password — pgAdmin 4 9.6 documentation"
[8]: https://www.pgadmin.org/download/ "Download"