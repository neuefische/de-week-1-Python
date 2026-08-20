# Git on macOS — Install & Verify

> Target audience: Students using **macOS** (Apple Silicon or Intel).
> Goal: Install Git the right way on macOS and verify it. Quick first-time config is included.

---

## 1) Check if Git is already installed

```bash
git --version
which git
```

macOS often has **Apple’s Git** via the Xcode Command Line Tools. The Git project also notes that *Apple ships Git with Xcode*. ([Git][1])

---

## 2) Install Git

### Option A — Fastest: Xcode Command Line Tools (Apple Git)

This gives you Apple’s Git quickly and is sufficient for most students.

```bash
xcode-select --install
```

Follow the prompts, then re-run `git --version`. Homebrew’s docs also call out that the **Command Line Tools (CLT)** are required for development on macOS. ([Homebrew Documentation][2])

### Option B — Latest Git via Homebrew

If you prefer the newest Git (and automatic updates):

```bash
brew install git
```

Verify the formula and supported macOS versions on Homebrew’s page. After install, `which git` should point to `$(brew --prefix)/bin/git` (e.g., `/opt/homebrew/bin/git` on Apple Silicon, `/usr/local/bin/git` on Intel). ([Homebrew Formulae][3])

---

## 3) Verify

```bash
git --version
which git
```

You should see a version like `git version 2.x.y` and the path you expect (Apple’s Git under `/usr/bin/git` after CLT, or Homebrew’s under its prefix).

---

## 4) One-time user configuration (recommended)

Set your identity and default initial branch:

```bash
git config --global user.name  "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global --list
```

The `init.defaultBranch` option is supported in Git ≥ 2.28; see the Git book and `git-config` docs. ([Git][4])

---

## Notes & tips

* If `git` prompts to install developer tools, that’s the **CLT** flow—accept it. (You can also trigger it manually with `xcode-select --install`.) ([Homebrew Documentation][2])
* Using Homebrew? Make sure `brew` is installed and on your `PATH` (see our Homebrew page).
* You can have both Apple Git and Homebrew Git installed; your shell will use whichever appears first in `PATH`.

---

## References (Official)

* **Git for macOS (downloads/notes; Apple ships Git with Xcode)** — Git SCM. ([Git][1])
* **Homebrew: Install & requirements (CLT mentioned)** — Homebrew Docs. ([Homebrew Documentation][2])
* **Homebrew formula: `git`** — current version & support matrix. ([Homebrew Formulae][3])
* **Git Book: First-time setup (default branch, identity)** — git-scm.com. ([Git][4])
* **git-config manual** — options and files. ([Git][5])

---

### Scope

This guide is macOS-only and mirrors our Linux lessons: check → install (CLT or Homebrew) → verify → first-time config.

[1]: https://git-scm.com/downloads/mac "Download for macOS"
[2]: https://docs.brew.sh/Installation "Installation — Homebrew Documentation"
[3]: https://formulae.brew.sh/formula/git "git — Homebrew Formulae"
[4]: https://git-scm.com/book/ms/v2/Getting-Started-First-Time-Git-Setup "1.6 Getting Started - First-Time Git Setup"
[5]: https://git-scm.com/docs/git-config "Git - git-config Documentation"
