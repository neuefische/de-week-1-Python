# PostgreSQL + psql on macOS — Install & Verify

> Target audience: Students using **macOS** (Apple Silicon or Intel).
> Goal: Install **PostgreSQL 16** and the **psql** client on macOS using a method that’s easy for students (Homebrew or EDB installer). Postgres.app is listed as a simple GUI alternative.

---

## Option A — Homebrew (recommended for most students)

1. Install PostgreSQL 16:

```bash
brew install postgresql@16
```

* The Homebrew formula for `postgresql@16` creates a **default database cluster** automatically (`initdb … $HOMEBREW_PREFIX/var/postgresql@16`). ([Homebrew Formulae][1])

2. Start PostgreSQL as a background service:

```bash
brew services start postgresql@16
```

* `brew services` is Homebrew’s standard way to start/stop background services on macOS. ([GitHub][2], [Homebrew Documentation][3])

3. Verify:

```bash
psql --version
psql -d postgres -c "select version();"
```

If you see a FATAL error about your role not existing, create a superuser for your macOS user, then try again:

```bash
createuser -s "$USER"
psql -d postgres
```

**Reference:** PostgreSQL download page for macOS and the Homebrew formula page. ([PostgreSQL][4], [Homebrew Formulae][5])

---

## Option B — EDB interactive installer (GUI)

This is the classic point-and-click installer linked from the official PostgreSQL macOS downloads page. ([PostgreSQL][4], [EDB][6])

1. Go to the EDB downloads page and pick **PostgreSQL 16** for macOS.

<p align="center">
   <img src="asset/EDB_photo.png" alt="" width="60%" />
</p>

2. Open the downloaded installer and follow the prompts. You may be asked for your macOS password.

<p align="center">
   <img src="asset/Save_changes_postgres.png" alt="" width="60%" />
</p>

3. Accept defaults unless your course specifies otherwise, then **Next** through the wizard.

<p align="center">
   <img src="asset/Postgres_clicknext.png" alt="" width="60%" />
</p>

4. After install, verify in Terminal:

```bash
psql --version
```

**References:** PostgreSQL macOS downloads; EDB’s step-by-step tutorial. ([PostgreSQL][4], [EDB][7])

---

## (Optional) Postgres.app (single-app bundle)

If you prefer a single macOS app that bundles PostgreSQL and tools:

* Download **Postgres.app** (choose the 16.x build if you want PG16).
* Launch the app to initialize and run the server.
* Add its `bin` directory to `PATH` if you want to use `psql` in Terminal.
  **Reference:** Postgres.app downloads page (lists versions incl. **16.9**). ([Postgres.app][8])

---

## Client-only (psql without the server)

If you only need the command-line tools (e.g., to connect to a remote DB):

```bash
brew install libpq
# Use with full path OR link it into PATH:
#   $(brew --prefix)/opt/libpq/bin/psql
brew link --force libpq    # optional: symlink psql into your PATH
```

`libpq` is **keg-only**, so it isn’t symlinked by default. ([Homebrew Formulae][9])

---

## Quick sanity checks

```bash
psql --version
psql -d postgres -c "select current_database(), current_user;"
```

---

## References (Official)

* **PostgreSQL — macOS downloads** (links to EDB installer, Postgres.app, Homebrew). ([PostgreSQL][4])
* **EDB — PostgreSQL downloads (macOS)**; **EDB tutorial** for macOS installer. ([EDB][6])
* **Homebrew formula: `postgresql@16`** (caveats & version). ([Homebrew Formulae][5])
* **Homebrew docs / services** (background services on macOS). ([GitHub][2], [Homebrew Documentation][3])
* **Postgres.app — Downloads**. ([Postgres.app][8])
* **Homebrew formula: `libpq`** (psql client). ([Homebrew Formulae][9])

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
