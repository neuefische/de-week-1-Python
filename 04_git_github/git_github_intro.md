# Git + GitHub

> Goal : learn the Git + GitHub workflow you’ll use in this course—clone → branch → commit → push → pull request (PR) → update from upstream → resolve conflicts.
> Install steps (Git, SSH keys) are already in **`02_Installation_and_setup/`**.

---

## 1) What are Git and GitHub?

* **Git** is a version control system. It tracks changes to files and lets teams work in parallel.
* **GitHub** hosts Git repositories in the cloud and adds features like pull requests, issues, and code reviews.

**Why we use them here**

* Keeps your work safe (you can roll back).
* Enables feedback via PRs.
* Matches real-world team workflows.

---

## 2) One-time setup (do this once per machine)

If you didn’t already in Day 1/2:

```bash
git config --global user.name  "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
```

Use **SSH** for pushes (set up in `02_Installation_and_setup/…/github_ssh_keys_*`):

```bash
ssh -T git@github.com   # should greet you by username
```

---

## 3) Course workflow (forks & branches)

We’ll use a standard “**fork & PR**” flow so you can keep your own copy while still pulling updates from the course repo.

### A) Fork the course repository

* On GitHub, open the **course repo** → click **Fork** → create fork under your account.

### B) Clone **your fork** (use SSH)

```bash
git clone git@github.com:<your-username>/<course-repo>.git
cd <course-repo>
```

### C) Add the upstream remote (the instructors’ repo)

```bash
git remote add upstream git@github.com:<instructor-org>/<course-repo>.git
git remote -v
```

Now:

* `origin` = **your fork** (you can push here).
* `upstream` = **course repo** (read-only for you).

### D) Create a feature branch per exercise

```bash
git checkout -b feat/<unit-or-day>-<short-topic>
# examples:
# feat/day3-git-basics
# feat/day3-colab-notebook
```

### E) Make changes → stage → commit

```bash
git status
git add path/to/file1 path/to/file2   # or: git add .
git commit -m "Add XYZ: short, imperative message"
```

**Commit style tip**

* Keep messages short, specific, and in the imperative (“Add”, “Fix”, “Update”).

### F) Push your branch to your fork

```bash
git push -u origin feat/day3-git-basics
```

### G) Open a Pull Request (PR)

* On GitHub, you’ll see **Compare & pull request**.
* **Base:** `main` on **your fork** (unless instructors told you to PR to the course repo).
* **Title:** `Day 3 – Git basics (Your Name)`
* **Description template (copy/paste):**

  * What changed?
  * How to test?
  * Screenshots/logs (if relevant)
  * Known issues / questions

> If your instructors want PRs **to the course repo** instead of your fork, change the PR target accordingly. We’ll announce which route we’re using.

---

## 4) Pull latest updates from instructors

Before starting new work each day:

```bash
git checkout main
git fetch upstream
git merge upstream/main        # or: git rebase upstream/main
git push origin main
```

Then branch from your fresh `main`:

```bash
git checkout -b feat/day3-new-task
```

---

## 5) Resolve merge conflicts (quick guide)

Conflicts happen when the same lines changed in two branches.

1. Run your update and see conflicts:

   ```bash
   git fetch upstream
   git merge upstream/main
   # or during rebase:
   # git rebase upstream/main
   ```
2. Open the conflicted files. Look for markers:

   ```
   <<<<<<< HEAD
   your version
   =======
   incoming version
   >>>>>>> upstream/main
   ```
3. Edit to the final content you want. Remove the markers.
4. Stage and continue:

   ```bash
   git add <file>
   git commit        # if merging
   # or, if rebasing:
   git rebase --continue
   ```
5. Push the updated branch:

   ```bash
   git push
   # If rebase rewrote history, you may need:
   git push --force-with-lease
   ```

**Tip:** If you’re unsure, prefer **merge** over rebase (simpler to reason about).

---

## 6) Working with Jupyter notebooks in Git

* Notebooks are JSON; small diffs can look noisy.
* **Keep outputs small** or **Clear All Outputs** before committing (especially big plots/large dataframes).
* Don’t commit large datasets (`data/` belongs in `.gitignore` or in cloud storage).
* For repeatability, also track `requirements.txt`:

  ```bash
  python -m pip freeze > requirements.txt
  ```

---

## 7) .gitignore & repo hygiene

* Use the project’s **`.gitignore`** to avoid committing junk:

  * Python: `.venv/`, `__pycache__/`, `*.pyc`
  * Jupyter: `.ipynb_checkpoints/`
  * Data: `data/`, `*.csv` (if large/private)
* Don’t commit **secrets** (API keys, passwords). If needed, put examples in `.env.example`.

---

## 8) Minimal Git command map (you’ll use these daily)

| Goal                            | Command                                                                |
| ------------------------------- | ---------------------------------------------------------------------- |
| Clone your fork                 | `git clone git@github.com:<you>/<repo>.git`                            |
| Add upstream                    | `git remote add upstream git@github.com:<org>/<repo>.git`              |
| New branch                      | `git checkout -b feat/xyz`                                             |
| Stage & commit                  | `git add .` → `git commit -m "Message"`                                |
| Push first time                 | `git push -u origin feat/xyz`                                          |
| Open PR                         | Use GitHub UI (Compare & pull request)                                 |
| Update local main               | `git checkout main` → `git fetch upstream` → `git merge upstream/main` |
| Bring updates into branch       | `git checkout feat/xyz` → `git merge main`                             |
| See history                     | `git log --oneline --graph --decorate --all`                           |
| Undo last commit (keep changes) | `git reset --soft HEAD~1`                                              |
| Discard local file changes      | `git checkout -- path/to/file` (or `git restore`)                      |

---

## 9) Small team habits (we’ll model these)

* **Small PRs**: easier to review and merge.
* **One branch per task**: keeps work isolated.
* **Pull before you push**: reduce conflicts.
* **PR titles & descriptions**: make reviewers’ lives easy.
* **CI later**: we’ll add checks (linters/tests) in later days.

---

## 10) 60–90 min activity (hands-on)

1. **Fork & clone** the course repo (SSH).
2. **Add upstream** remote.
3. **Create branch** `feat/day3-warmup-<yourname>`.
4. Add a short note to `notes/day3.md` (or a sandbox file):

   * 3 bullets you learned about Git.
   * 1 question you have.
5. **Stage, commit, push**, then **open a PR** to your fork’s `main` (or to the course repo if instructed).
6. **Review a peer’s PR**: leave one comment and one suggestion.
7. **Update from upstream** and **resolve a small, instructor-seeded conflict** (we’ll provide a file to collide on).
8. **Merge** your PR after review is addressed.

Deliverable: PR link posted in the class chat or LMS.

---

## 11) Troubleshooting quick fixes

* **“Permission denied (publickey)”** → your SSH key isn’t set or GitHub doesn’t have the public key. Revisit `02_Installation_and_setup/.../github_ssh_keys_*`.
* **“fatal: not a git repository”** → you’re not inside the repo folder (`cd <repo>`).
* **“Updates were rejected”** → pull first: `git pull --rebase` (or `git fetch` + `git merge`) then push.
* **Detached HEAD** → create a branch: `git switch -c rescue/<topic>` and continue.
* **Wrong remote** → check `git remote -v`; set SSH URL:

  ```bash
  git remote set-url origin git@github.com:<you>/<repo>.git
  ```

