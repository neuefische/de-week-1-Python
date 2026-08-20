# pgAdmin 4 on macOS — Install & Launch

> Target audience: Students using **macOS** (Apple Silicon or Intel).
> Goal: Install **pgAdmin 4** using either the official DMG or Homebrew cask, launch it, and connect to your local PostgreSQL server.

---

## Option A — Homebrew cask (recommended if you use Homebrew)

```bash
brew install --cask pgadmin4
```

Launch from **Applications** or Spotlight (Cmd+Space → "pgAdmin 4"), or via Terminal:

```bash
open "/Applications/pgAdmin 4.app"
```

The cask automatically picks the right build for your Mac and updates with `brew upgrade --cask pgadmin4`. ([Homebrew Formulae][11])

---

## Option B — Official DMG (Desktop app bundle)

1. Go to the pgAdmin macOS download page and choose the build for your Mac: **Apple Silicon (arm64)** or **Intel (x86_64)**. ([pgadmin.org][10])
2. Download the `.dmg`, open it, and drag **pgAdmin 4** to **Applications**.
3. Launch from **Applications** or Spotlight.

> Not sure which chip you have? **Apple menu → About This Mac** — "Chip Apple M…" = Apple Silicon, "Processor Intel" = Intel.

---

## First-run behavior (Master Password)

On first launch, pgAdmin may ask you to set a **Master Password** — it encrypts server passwords you choose to save. Set it and keep it safe. ([pgadmin.org][12])

---

## Connect pgAdmin to your local PostgreSQL

1. Make sure PostgreSQL is running (Homebrew install from the PostgreSQL guide):

```bash
brew services start postgresql@18
```

2. In pgAdmin: right-click **Servers → Register → Server…** (or **Add New Server**).
3. Fill in:

   * **General → Name:** `Local` (any name)
   * **Connection → Host:** `localhost` | **Port:** `5432` | **Maintenance DB:** `postgres`
   * **Username / Password:** depends on how you installed PostgreSQL:
     * **Homebrew (`postgresql@18`)** → Username: your **macOS username**; leave **Password empty** (Homebrew uses *trust* authentication on localhost).
     * **EDB installer** → Username: `postgres`; **Password:** the one you set during install.

4. **Save** — your databases appear under the server node.

---

## Troubleshooting

* **Connection fails on a Homebrew install** → make sure you used your macOS username (run `whoami` to check), not `postgres`.
* **Connection refused** → PostgreSQL isn't running; re-run the `brew services start` command above.
* **"pgAdmin 4 is damaged / can't be opened"** → re-download from the official page and make sure you picked the right architecture (Apple Silicon vs Intel).

---

## References (Official)

* **pgAdmin 4 (macOS) — Download page** (supported macOS versions, Apple Silicon/Intel builds). ([pgadmin.org][10])
* **Homebrew cask: `pgadmin4`** (install command/version). ([Homebrew Formulae][11])
* **pgAdmin docs — Master Password**. ([pgadmin.org][12])
* **Homebrew formula: `postgresql@18`** (service management). ([Homebrew Formulae][1])

---

[1]: https://formulae.brew.sh/formula/postgresql%4018 "postgresql@18 — Homebrew Formulae"
[10]: https://www.pgadmin.org/download/pgadmin-4-macos/ "pgAdmin 4 (macOS)"
[11]: https://formulae.brew.sh/cask/pgadmin4 "pgadmin4 — Homebrew Formulae"
[12]: https://www.pgadmin.org/docs/pgadmin4/latest/master_password.html "Master Password — pgAdmin 4 documentation"
