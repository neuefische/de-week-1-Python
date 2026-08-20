# PostgreSQL + psql on Windows — Install & Verify

> Target audience: Students on **Windows 10/11** (64-bit).
> Goal: Install **PostgreSQL 18** (current major release; includes the **psql** client) using the official EDB installer, then verify.

---

## 1) Download the official Windows installer

1. Go to the PostgreSQL Windows download page and follow the **Windows installers** link (EDB Interactive Installer). ([PostgreSQL][1])
2. On the EDB downloads page, choose the latest **PostgreSQL 18.x → Windows x86-64**. ([EDB][2])

<p align="center">
   <img src="asset/EDB_photo.png" alt="" width="60%" />
</p>

---

## 2) Run the installer (EDB Interactive Installer)

* Double-click the downloaded installer and click **Next** through the wizard.
* Accept the license, pick the default install directory, and select components (see below).
* You'll be asked to set a password for the **`postgres` superuser** (there's **no default password** — you must create one during install). Keep it safe. ([PostgreSQL][1])

**Select components** — ensure these are checked:

* **PostgreSQL Server** (database server)
* **Command Line Tools** (includes **psql**)
* **pgAdmin 4** (GUI) — optional; also covered in the pgAdmin file
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

## 3) Make `psql` available in PowerShell / CMD (PATH)

The installer does **not** add PostgreSQL's `bin` folder to your `PATH` — `psql` works in the "SQL Shell" shortcut but not yet in a plain terminal. Add it (adjust `18` if you installed a different version):

1. Start Menu → search **"Edit the system environment variables"** → **Environment Variables…**
2. Under *User variables*, select **Path** → **Edit** → **New** and add:

   ```
   C:\Program Files\PostgreSQL\18\bin
   ```

3. **Close and reopen** PowerShell, then check:

```powershell
psql --version
```

Expected: `psql (PostgreSQL) 18.x`.

---

## 4) Verify the installation

### A) From **SQL Shell (psql)**

Open **Start → SQL Shell (psql)**. If you accepted defaults, press **Enter** through the prompts (host, database, port, user), then enter the password you set during install.

<p align="center">
   <img src="asset/Testing_1.png" alt="" width="60%" />
</p>

If you get the `postgres=#` prompt, you're connected. Try:

```sql
SELECT version();
```

<p align="center">
   <img src="asset/Testing_2.png" alt="" width="60%" />
</p>

### B) From Command Prompt / PowerShell

With the PATH step (Step 3) done:

```powershell
psql -U postgres -d postgres -c "SELECT version();"
```

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
[4]: https://www.enterprisedb.com/docs/supported-open-source/postgresql/installing/windows/ "Installing PostgreSQL on Windows"
[5]: https://www.postgresql.org/download/ "Downloads"
