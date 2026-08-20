# PostgreSQL + psql on macOS — Install & Verify

> Target audience: Students using **macOS** (Apple Silicon or Intel).
> Goal: Install **PostgreSQL 18** (current major release) and the **psql** client on macOS using a method that's easy for students (Homebrew or EDB installer). Postgres.app is listed as a simple GUI alternative.

---

## Option A — Homebrew (recommended for most students)

1. Install PostgreSQL 18:

```bash
brew install postgresql@18
```

* The formula creates a **default database cluster** automatically (`initdb … $HOMEBREW_PREFIX/var/postgresql@18`). ([Homebrew Formulae][1])

2. Add it to your `PATH` — **required**, because `postgresql@18` is *keg-only* (not symlinked by default):

```bash
echo 'export PATH="'"$(brew --prefix)"'/opt/postgresql@18/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

3. Start PostgreSQL as a background service:

```bash
brew services start postgresql@18
```

* `brew services` is built into Homebrew — no separate plugin needed. ([Homebrew Formulae][1])

4. Verify:

```bash
psql --version
psql -d postgres -c "select version();"
```

Expected: `psql (PostgreSQL) 18.x`. The installer creates a superuser role named after your macOS user, so this normally connects directly. If you see `FATAL: role "<user>" does not exist`, create the role and retry:

```bash
createuser -s "$USER"
psql -d postgres
```

**Reference:** PostgreSQL download page for macOS and the Homebrew formula page. ([PostgreSQL][4], [Homebrew Formulae][1])

---

## Option B — EDB interactive installer (GUI)

This is the classic point-and-click installer linked from the official PostgreSQL macOS downloads page. ([PostgreSQL][4], [EDB][6])

1. Go to the EDB downloads page and pick the latest **PostgreSQL 18.x** for macOS.

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

4. The EDB installer does not add `psql` to your `PATH`. Add it once:

```bash
echo 'export PATH="/Library/PostgreSQL/18/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

5. Verify in Terminal:

```bash
psql --version
```

**References:** PostgreSQL macOS downloads; EDB's step-by-step tutorial. ([PostgreSQL][4], [EDB][7])

---

## (Optional) Postgres.app (single-app bundle)

If you prefer a single macOS app that bundles PostgreSQL and tools:

* Download **Postgres.app** (the current release ships PostgreSQL 18).
* Launch the app to initialize and run the server.
* Add its `bin` directory to `PATH` to use `psql` in Terminal:

```bash
echo 'export PATH="/Applications/Postgres.app/Contents/Versions/latest/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

**Reference:** Postgres.app downloads page. ([Postgres.app][8])

---

## Client-only (psql without the server)

If you only need the command-line tools (e.g., to connect to a remote DB):

```bash
brew install libpq
echo 'export PATH="'"$(brew --prefix)"'/opt/libpq/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

`libpq` is **keg-only**, so the PATH step is required. ([Homebrew Formulae][9])

---

## Quick sanity checks

```bash
psql --version
psql -d postgres -c "select current_database(), current_user;"
```

---

## References (Official)

* **PostgreSQL — macOS downloads** (links to EDB installer, Postgres.app, Homebrew). ([PostgreSQL][4])
* **EDB — PostgreSQL downloads (macOS)**; **EDB tutorial** for macOS installer. ([EDB][6], [EDB][7])
* **Homebrew formula: `postgresql@18`** (caveats: keg-only, PATH, `brew services`). ([Homebrew Formulae][1])
* **Postgres.app — Downloads**. ([Postgres.app][8])
* **Homebrew formula: `libpq`** (psql client). ([Homebrew Formulae][9])

---

[1]: https://formulae.brew.sh/formula/postgresql%4018 "postgresql@18 — Homebrew Formulae"
[4]: https://www.postgresql.org/download/macosx/ "macOS packages"
[6]: https://www.enterprisedb.com/downloads/postgres-postgresql-downloads "Download PostgreSQL"
[7]: https://www.enterprisedb.com/postgres-tutorials/installation-postgresql-mac-os "Installation of PostgreSQL on Mac OS"
[8]: https://postgresapp.com/downloads.html "Postgres.app Downloads"
[9]: https://formulae.brew.sh/formula/libpq "libpq — Homebrew Formulae"
