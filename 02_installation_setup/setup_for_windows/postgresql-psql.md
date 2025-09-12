# PostgreSQL + psql on Windows — Install & Verify

> Target audience: Students on **Windows 10/11** (64-bit).
> Goal: Install **PostgreSQL 16.9** (which includes the **psql** client) using the official EDB installer, then verify.

---

## 1) Download the official Windows installer

1. Go to the PostgreSQL Windows download page and follow the **Windows installers** link (EDB Interactive Installer). ([PostgreSQL][1])
2. On the EDB downloads page, choose **PostgreSQL 16.9 → Windows x86-64**. ([EDB][2])

<p align="center">
   <img src="asset/EDB_photo.png" alt="" width="60%" />
</p>

---

## 2) Run the installer (EDB Interactive Installer)

* Double-click the downloaded installer and click **Next** through the wizard.
* Accept the license, pick the default install directory, and select components (see below).
* You’ll be asked to set a password for the **`postgres` superuser** (there’s **no default password**—you must create one during install). Keep it safe. ([PostgreSQL][1], [Super User][3])

**Select components** — ensure these are checked:

* **PostgreSQL Server** (database server)
* **pgAdmin 4** (GUI) — optional if you’ll install it separately; covered in the pgAdmin file
* **Command Line Tools** (includes **psql**)
* **Stack Builder** — optional; not required for this course ([PostgreSQL][1])

<p align="center">
   <img src="asset/Checkbox_postgres.png" alt="" width="60%" />
</p>

Set the **superuser password** when prompted:

<p align="center">
   <img src="asset/Password.png" alt="" width="60%" />
</p>

Leave the default **port 5432** unless told otherwise:

<p align="center">
   <img src="asset/port.png" alt="" width="60%" />
</p>

Accept the default **locale** and continue to install:

<p align="center">
   <img src="asset/last.png" alt="" width="60%" />
</p>

> The EDB Windows installer is the official packaging path linked from postgresql.org and includes server, pgAdmin, and Stack Builder. ([PostgreSQL][1])

---

## 3) Verify the installation

### A) From **SQL Shell (psql)**

Open **Start → SQL Shell (psql)**. If you accepted defaults, you can press **Enter** through the prompts (host, database, port, user), then enter the password you set during install.

<p align="center">
   <img src="asset/Testing_1.png" alt="" width="60%" />
</p>

If you get the `postgres=#` prompt, you’re connected. Try:

```sql
SELECT version();
```

<p align="center">
   <img src="asset/Testing_2.png" alt="" width="60%" />
</p>

### B) From Command Prompt / PowerShell

If your PATH includes PostgreSQL’s `bin`, you can run:

```powershell
psql --version
```

(You should see `psql (PostgreSQL) 16.9`.) The Windows installer provides the psql client as part of the tools. ([PostgreSQL][1])

---

## References (Official)

* **PostgreSQL — Windows installers (EDB)** (lists bundled components, official path). ([PostgreSQL][1])
* **EDB — Installing PostgreSQL on Windows** (components include PostgreSQL Server, pgAdmin 4, Stack Builder). ([EDB][4])
* **PostgreSQL — Downloads hub** (links to Windows). ([PostgreSQL][5])

---

### Scope

This page focuses on the **server + psql** setup via the official installer. If you skipped pgAdmin during installation (or want the latest separately), see the **pgAdmin 4 on Windows** file.

[1]: https://www.postgresql.org/download/windows/ "PostgreSQL: Windows installers"
[2]: https://www.enterprisedb.com/downloads/postgres-postgresql-downloads "Download PostgreSQL"
[3]: https://superuser.com/questions/576623/default-password-for-postgresql "Default password for postgreSQL"
[4]: https://www.enterprisedb.com/docs/supported-open-source/postgresql/installing/windows/ "Installing PostgreSQL on Windows"
[5]: https://www.postgresql.org/download/ "Downloads"
[6]: https://www.pgadmin.org/download/pgadmin-4-windows/ "pgAdmin 4 (Windows) Download"
[7]: https://www.pgadmin.org/docs/pgadmin4/latest/master_password.html "Master Password — pgAdmin 4 9.6 documentation"
[8]: https://www.pgadmin.org/download/ "Download"
