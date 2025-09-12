# pgAdmin 4 on macOS — Install & Launch

> Target audience: Students using **macOS** (Apple Silicon or Intel).
> Goal: Install **pgAdmin 4** using either the official DMG or Homebrew cask, then launch it.

---

## Option A — Official DMG (Desktop app bundle)

1. Go to the pgAdmin macOS download page and choose **Apple Silicon** or **Intel**. ([pgadmin.org][10])
2. Download the `.dmg`, open it, and drag **pgAdmin 4** to **Applications**.
3. Launch from **Applications** or Spotlight (Cmd+Space → “pgAdmin 4”).

**References:** pgAdmin macOS downloads; pgAdmin downloads overview. ([pgadmin.org][10])

---

## Option B — Homebrew (auto-updates via cask)

```bash
brew install --cask pgadmin4
```

* Launch from **Applications** or Spotlight, or via Terminal:

```bash
open /Applications/pgAdmin\ 4.app
```

**Reference:** Homebrew cask for pgAdmin 4. ([Homebrew Formulae][11])

---

## First-run tips

* On first launch, pgAdmin asks you to set a **master password** (local credential storage).
* To connect to your local PostgreSQL (installed via Homebrew), host is `localhost`, port `5432`. If you created a `postgres` superuser or use your macOS user as a role, supply that user and its password (if any).
* If you used the **EDB installer**, use the superuser **password you set during install**.

---

## Verify pgAdmin connects

1. Start PostgreSQL (if installed via Homebrew):

```bash
brew services start postgresql@16
```

2. In pgAdmin, **Add New Server** →

   * **Name:** `Local`
   * **Host:** `localhost`
   * **Port:** `5432`
   * **Username:** your PostgreSQL role (e.g., your macOS user or `postgres`)
   * **Password:** as configured

You should see your databases listed under the server node.

---

## References (Official)

* **pgAdmin 4 (macOS) — Download page** (lists supported macOS versions, Apple Silicon/Intel builds). ([pgadmin.org][10])
* **Homebrew cask: `pgadmin4`** (install command/version). ([Homebrew Formulae][11])

---

[1]: https://formulae.brew.sh/formula/postgresql%4016 "postgresql@16 — Homebrew Formulae"
[2]: https://github.com/Homebrew/homebrew-services "Homebrew Services (deprecated)"
[3]: https://docs.brew.sh/Formula-Cookbook "Formula Cookbook"
[4]: https://www.postgresql.org/download/macosx/ "macOS packages"
[5]: https://formulae.brew.sh/formula/postgresql%4016 "postgresql@16 — Homebrew Formulae"
[6]: https://www.enterprisedb.com/downloads/postgres-postgresql-downloads "Download PostgreSQL"
[7]: https://www.enterprisedb.com/postgres-tutorials/installation-postgresql-mac-os "Installation of PostgreSQL on Mac OS"
[8]: https://postgresapp.com/downloads.html "Postgres.app Downloads"
[9]: https://formulae.brew.sh/formula/libpq "libpq — Homebrew Formulae"
[10]: https://www.pgadmin.org/download/pgadmin-4-macos/ "pgAdmin 4 (macOS)"
[11]: https://formulae.brew.sh/cask/pgadmin4 "pgadmin4"