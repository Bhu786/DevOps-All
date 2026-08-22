# Git Interview Questions — Start to End

**Simple to Learn • Easy to Remember • Interview Ready**

> This Markdown version preserves the topics from the uploaded PATHNEX Git Interview Questions PDF and reorganizes them into simple interview explanations, memory tricks, commands, scenarios, and quick revision. The source starts with Merge vs Rebase, Hotfix, and Cherry-pick. fileciteturn2file0L5-L28

---

# 1. Rebase vs Merge

## Merge

Merge combines branches with a **merge commit**.

### Key points

- Combines branches with a merge commit.
- Preserves full history, including branch structure.
- Safe for shared branches.

### Interview answer

> **Merge combines branches and preserves the complete branch history by creating a merge commit. It is generally safe for shared branches.**

### Memory trick

**MERGE = COLLABORATION**

---

## Rebase

Rebase places your commits on top of another branch.

### Key points

- Rewrites history.
- Places your commits on top of another branch.
- Creates a cleaner, linear history.
- Dangerous on shared branches because it can affect others' work.

### Interview answer

> **Rebase rewrites history by placing my commits on top of another branch. It gives a cleaner linear history, but I avoid rebasing shared branches because it can affect other developers' work.**

### Memory trick

**REBASE = LOCAL CLEANUP**

### Rule of thumb

> **Use merge for collaboration, rebase for local cleanup.**

### Quick table

| Feature | Merge | Rebase |
|---|---|---|
| Merge commit | Yes | Normally no |
| Preserves branch structure | Yes | No |
| Rewrites history | No | Yes |
| Safe for shared branches | Yes | No |
| History | Complete | Linear/clean |

---

# 2. Hotfix

A **hotfix** is a quick fix for a critical issue in production.

### Key points

- Used for a critical production issue.
- Typically branched from `main` or `master`.
- After fixing, it is merged back into:
  - `main`
  - `develop` if using Git Flow.

### Simple flow

```text
main
  |
  +---- hotfix
          |
       fix issue
          |
          +---- main
          |
          +---- develop
```

### Interview answer

> **A hotfix is a short-lived branch created to quickly fix a critical production issue. It is typically created from main/master and then merged back into main and, when using Git Flow, develop.**

### Memory trick

**HOTFIX = PRODUCTION FIRE → QUICK FIX**

---

# 3. Cherry-pick

Cherry-pick applies a **specific commit** from one branch to another.

```bash
git cherry-pick <commit-hash>
```

### Useful when

- You need one specific fix.
- You do not need the whole branch.

### Interview answer

> **Cherry-pick allows me to apply a specific commit from one branch onto another branch. I use it when I need one particular fix without merging the entire branch.**

### Memory trick

**CHERRY-PICK = PICK ONE COMMIT**

---

# 4. Branching Strategies

The source covers:

1. Git Flow
2. GitHub Flow
3. Trunk-Based Development

---

## 4.1 Git Flow

```text
main      → production
develop   → ongoing work
feature   → feature work
release   → release preparation
hotfix    → urgent production fix
```

### Interview answer

> **Git Flow uses main for production, develop for ongoing work, and feature, release, and hotfix branches depending on the development and release process.**

### Memory trick

**Git Flow = MAIN + DEVELOP + FEATURE + RELEASE + HOTFIX**

---

## 4.2 GitHub Flow

Simple model:

```text
main
  |
feature branch
  |
Pull Request
  |
main
```

Uses:

- `main`
- Feature branches
- Pull Requests

### Interview answer

> **GitHub Flow is a simpler branching strategy based around main, short-lived feature branches, and pull requests.**

### Memory trick

**GitHub Flow = MAIN + FEATURE + PR**

---

## 4.3 Trunk-Based Development

- Developers commit to `main` frequently.
- Branches are short-lived.

### Interview answer

> **In trunk-based development, developers integrate changes into main frequently and use short-lived branches.**

### Memory trick

**TRUNK-BASED = FREQUENT MAIN + SHORT BRANCHES**

---

## Choosing a strategy

The source says to choose based on:

- Team size
- Release complexity

### Interview line

> **I choose the branching strategy based on team size and release complexity.**

---

# 5. `.gitignore`

`.gitignore` tells Git which files to ignore.

### Example

```gitignore
node_modules/
.env
*.log
```

It helps prevent committing:

- Secrets
- Dependencies
- Build files

### Interview answer

> **`.gitignore` tells Git which files or directories should not be tracked or committed. I commonly use it to avoid committing secrets, dependencies, logs, and build files.**

### Memory trick

**`.gitignore` = DON'T COMMIT THESE**

---

# 6. How to Resolve a Git Conflict

A conflict can occur during:

- Merge
- Rebase

## Step 1 — Conflict occurs

Git identifies conflicting changes.

## Step 2 — Open the conflicting file

You may see:

```text
<<<<<<< HEAD
your code
=======
incoming code
>>>>>>> branch
```

## Step 3 — Edit manually

Keep the correct version or combine the correct changes.

Remove the conflict markers.

## Step 4 — Stage the resolution

```bash
git add .
```

## Step 5 — Complete the merge

```bash
git commit
```

### For rebase

```bash
git rebase --continue
```

### Interview answer

> **When a Git conflict occurs, I open the conflicting file, review both versions using the conflict markers, manually resolve the correct code, remove the markers, stage the resolution with `git add`, and complete the operation. For a rebase, I use `git rebase --continue`.**

### Memory trick

**CONFLICT → EDIT → ADD → COMPLETE**

---

# 7. Hard vs Soft Reset

## Soft Reset

```bash
git reset --soft HEAD~1
```

### What it does

- Undoes the commit.
- Keeps changes staged.

### Interview answer

> **A soft reset undoes the commit but keeps the changes staged, so I can modify or recommit them.**

### Memory trick

**SOFT = COMMIT GONE, WORK STAYS**

---

## Hard Reset

```bash
git reset --hard HEAD~1
```

### What it does

- Deletes the commit.
- Deletes the changes permanently according to the source.

### Warning

The source explicitly says:

> **Use hard reset carefully because it is destructive.**

### Interview answer

> **A hard reset removes the commit and its changes. Because it is destructive, I use it carefully.**

### Memory trick

**HARD = COMMIT GONE + CHANGES GONE**

---

## Soft vs Hard

| Feature | Soft | Hard |
|---|---|---|
| Undo commit | Yes | Yes |
| Keep changes | Yes | No |
| Changes staged | Yes | No |
| Destructive | No | Yes |

---

# 8. Git Stash

Git stash temporarily saves **uncommitted changes**.

### Commands

```bash
git stash
git stash pop
```

### Useful when

You need to switch branches in the middle of your work.

### Example

```text
Working on feature-A
       ↓
Uncommitted work
       ↓
git stash
       ↓
Switch branch
       ↓
Do urgent work
       ↓
git stash pop
       ↓
Continue feature-A
```

### Interview answer

> **Git stash temporarily saves uncommitted changes so I can switch branches or work on another task without making an unfinished commit. I restore them using `git stash pop`.**

### Memory trick

**STASH = PARK WORK TEMPORARILY**

---

# 9. Git Clone vs Fork

## Clone

```bash
git clone <repo-url>
```

Clone copies the repository to your **local machine**.

### Interview answer

> **Clone copies a repository from a remote repository to my local machine so I can work on it locally.**

### Memory trick

**CLONE = GITHUB → MY COMPUTER**

---

## Fork

Fork copies a repository to **your GitHub account**.

The source describes it as useful for contributing to other people's projects.

### Interview answer

> **Fork creates a copy of a repository under my GitHub account and is commonly used when contributing to another project's repository.**

### Memory trick

**FORK = OTHER GITHUB → MY GITHUB**

---

## Clone vs Fork

| Feature | Clone | Fork |
|---|---|---|
| Destination | Local machine | Your GitHub account |
| Purpose | Local development | Collaboration/contribution |
| Memory | GitHub → Computer | GitHub → Your GitHub |

### Rule

> **Fork → Collaboration**
>
> **Clone → Local development**

---

# 10. Pull vs Fetch

## Fetch

```bash
git fetch
```

### What it does

- Downloads changes.
- Does not modify your working branch.

### Interview answer

> **`git fetch` downloads the latest remote changes but does not modify my current working branch.**

### Memory trick

**FETCH = DOWNLOAD, DON'T APPLY**

---

## Pull

```bash
git pull
```

The source describes:

```text
git pull = git fetch + merge
```

### Interview answer

> **`git pull` fetches changes and then merges them into the current branch.**

### Memory trick

**PULL = FETCH + MERGE**

---

## Safer workflow from the source

```bash
git fetch
git merge
```

This gives you more control over the merge.

---

# 11. Reset vs Revert

## Reset

Reset moves the branch pointer and rewrites history.

The source recommends it for:

- Local changes

### Memory trick

**RESET = MOVE HISTORY POINTER**

---

## Revert

```bash
git revert <commit>
```

Revert creates a **new commit** that undoes the changes of an earlier commit.

The source says it is:

- Safe for shared branches.
- Suitable for shared history.

### Example

```text
A---B---C
        |
        bad change

git revert C

A---B---C---D
            |
          D undoes C
```

### Interview answer

> **`git revert` creates a new commit that undoes the changes from an earlier commit, so it is safer for shared branches because it does not rewrite existing history.**

### Memory trick

**REVERT = UNDO WITH A NEW COMMIT**

---

## Reset vs Revert

| Feature | Reset | Revert |
|---|---|---|
| Moves branch pointer | Yes | No |
| Rewrites history | Yes | No |
| Creates new commit | No | Yes |
| Safe for shared branch | No | Yes |
| Best use | Local changes | Shared history |

### Easy rule

**RESET → LOCAL**

**REVERT → SHARED**

---

# 12. Quick Summary — Team Safety and History

The final page of the source gives this summary:

| Concept | Safe for Team? | Rewrites History? |
|---|---:|---:|
| Merge | Yes | No |
| Rebase | No (shared) | Yes |
| Reset | No | Yes |
| Revert | Yes | No |

### Master memory

```text
MERGE
→ Safe + No history rewrite

REBASE
→ Not safe for shared + History rewrite

RESET
→ Not safe for shared + History rewrite

REVERT
→ Safe for shared + No history rewrite
```

---

# 13. Master Git Interview Cheat Sheet

## Branch History

```text
Merge  → Preserve history
Rebase → Rewrite history / linear history
```

## Production Fix

```text
Hotfix → Quick production fix
```

## One Commit

```text
Cherry-pick → Pick one commit
```

## Branching

```text
Git Flow
→ main + develop + feature/release/hotfix

GitHub Flow
→ main + feature + PR

Trunk-Based
→ frequent main + short branches
```

## Ignore Files

```text
.gitignore
→ secrets + dependencies + build/log files
```

## Conflict

```text
Conflict
  ↓
Edit
  ↓
git add .
  ↓
git commit

Rebase:
git rebase --continue
```

## Undo Commit

```text
Soft Reset
→ Undo commit + keep staged changes

Hard Reset
→ Undo commit + delete changes
```

## Temporary Work

```text
git stash
git stash pop
```

## Repository

```text
Clone → Local machine
Fork  → Your GitHub account
```

## Remote Changes

```text
Fetch → Download only
Pull  → Fetch + Merge
```

## Undo Existing Commit

```text
Reset  → Rewrite history / local
Revert → New undo commit / shared
```

---

# 14. Scenario-Based Interview Memory

## Scenario 1 — Production is Broken

Use:

```text
HOTFIX
```

**Think:** Production problem → quick fix.

---

## Scenario 2 — I Need Only One Commit

Use:

```text
CHERRY-PICK
```

**Think:** Pick one commit, not the whole branch.

---

## Scenario 3 — My Local Branch History Is Messy

Use:

```text
REBASE
```

**Think:** Clean local history.

---

## Scenario 4 — Shared Branch

Prefer:

```text
MERGE
```

**Think:** Don't rewrite shared history.

---

## Scenario 5 — Unfinished Work, Need to Switch Branch

Use:

```bash
git stash
```

**Think:** Park work temporarily.

---

## Scenario 6 — Need Remote Changes Without Applying Them

Use:

```bash
git fetch
```

**Think:** Download, don't merge.

---

## Scenario 7 — Need Remote Changes Applied

Use:

```bash
git pull
```

**Think:** Fetch + merge.

---

## Scenario 8 — Undo a Commit on Shared Branch

Use:

```bash
git revert <commit>
```

**Think:** New commit that undoes old commit.

---

## Scenario 9 — Undo Local Commit and Keep Work

Use:

```bash
git reset --soft HEAD~1
```

**Think:** Commit gone, work stays staged.

---

## Scenario 10 — Throw Away Local Changes

Use:

```bash
git reset --hard HEAD~1
```

**Think:** Destructive — use carefully.

---

# 15. Complete Git Decision Tree

```text
What do I need?

        |
        +---- Combine branches?
        |         |
        |         +---- Shared branch → MERGE
        |         |
        |         +---- Local cleanup → REBASE
        |
        +---- Critical production issue?
        |         |
        |         +---- HOTFIX
        |
        +---- Need only one commit?
        |         |
        |         +---- CHERRY-PICK
        |
        +---- Unfinished work?
        |         |
        |         +---- Temporarily save → STASH
        |
        +---- Remote changes?
        |         |
        |         +---- Download only → FETCH
        |         |
        |         +---- Download + apply → PULL
        |
        +---- Undo commit?
        |         |
        |         +---- Local → RESET
        |         |
        |         +---- Shared → REVERT
        |
        +---- Repository copy?
        |         |
        |         +---- Local machine → CLONE
        |         |
        |         +---- GitHub account → FORK
        |
        +---- Conflict?
                  |
                  +---- EDIT → ADD → COMMIT
                              |
                              +---- Rebase → REBASE --CONTINUE
```

---

# 16. Ready-to-Speak Interview Answers

## Q1. Merge vs Rebase?

> **Merge combines branches and preserves the full history with a merge commit, so it is safe for shared branches. Rebase rewrites history by placing my commits on top of another branch, giving a cleaner linear history. I prefer merge for shared collaboration and rebase for local cleanup.**

---

## Q2. What is a Hotfix?

> **A hotfix is a quick fix for a critical production issue. It is typically created from main or master, and after fixing the issue it is merged back into main and, when using Git Flow, develop.**

---

## Q3. What is Cherry-pick?

> **Cherry-pick allows me to apply one specific commit from another branch without bringing the entire branch.**

```bash
git cherry-pick <commit-hash>
```

---

## Q4. How do you resolve a Git conflict?

> **I identify the conflicting file, review the current and incoming changes using the conflict markers, manually resolve the correct code, remove the markers, run `git add`, and complete the merge with `git commit`. If it is a rebase, I use `git rebase --continue`.**

---

## Q5. Soft Reset vs Hard Reset?

> **Soft reset undoes the commit but keeps the changes staged. Hard reset removes the commit and changes, so it is destructive and must be used carefully.**

---

## Q6. What is Git Stash?

> **Git stash temporarily saves uncommitted changes. I use it when I need to switch branches or handle another task without committing incomplete work.**

---

## Q7. Clone vs Fork?

> **Clone copies a repository to my local machine, while fork creates a copy of the repository under my GitHub account, commonly for contributing to another project's repository.**

---

## Q8. Fetch vs Pull?

> **Fetch downloads remote changes without modifying my working branch. Pull performs fetch followed by merge.**

---

## Q9. Reset vs Revert?

> **Reset moves the branch pointer and rewrites history, so it is generally used for local work. Revert creates a new commit that undoes an earlier commit, making it safer for shared branches.**

---

# 17. Final 30-Second Revision

```text
MERGE
= Combine + preserve history + shared safe

REBASE
= Rewrite history + linear + local cleanup

HOTFIX
= Critical production fix

CHERRY-PICK
= One specific commit

GIT FLOW
= main + develop + feature/release/hotfix

GITHUB FLOW
= main + feature + PR

TRUNK-BASED
= frequent main + short branches

.gitignore
= Ignore secrets/dependencies/build files

CONFLICT
= Edit → add → commit
= Rebase → git rebase --continue

SOFT RESET
= Undo commit + keep staged changes

HARD RESET
= Undo commit + delete changes

STASH
= Temporarily save uncommitted work

CLONE
= Repository → local machine

FORK
= Repository → your GitHub

FETCH
= Download changes only

PULL
= Fetch + merge

RESET
= Rewrite history / local

REVERT
= New undo commit / shared
```

---

# 18. Final Master Trick

> **MERGE keeps history. REBASE cleans local history. HOTFIX fixes production. CHERRY-PICK picks one commit. STASH parks unfinished work. FETCH downloads without applying. PULL fetches and merges. RESET rewrites local history. REVERT safely undoes shared history. CLONE brings the repository to your computer. FORK brings a copy to your GitHub account.**

---

# 19. Source Coverage Check

This document preserves the topics present in the uploaded 5-page PATHNEX Git Interview Questions PDF:

- Rebase vs Merge
- Merge
- Merge commit
- Full history
- Shared branch safety
- Rebase
- History rewriting
- Linear history
- Shared branch warning
- Merge vs rebase rule of thumb
- Hotfix
- Production issue
- Main/master
- Develop
- Cherry-pick
- Cherry-pick command
- Branching strategies
- Git Flow
- Main
- Develop
- Feature
- Release
- Hotfix branches
- GitHub Flow
- Main
- Feature branches
- Pull Requests
- Trunk-Based Development
- Frequent main commits
- Short-lived branches
- Team size and release complexity
- `.gitignore`
- Ignored file examples
- Secrets
- Dependencies
- Build files
- Git conflict
- Merge/rebase conflict
- Conflict markers
- Manual resolution
- `git add .`
- `git commit`
- `git rebase --continue`
- Soft reset
- `git reset --soft HEAD~1`
- Hard reset
- `git reset --hard HEAD~1`
- Destructive reset warning
- Git stash
- `git stash`
- `git stash pop`
- Switching branches with uncommitted work
- Git clone
- `git clone <repo-url>`
- Local repository
- Git fork
- GitHub account
- Collaboration
- Pull vs fetch
- `git fetch`
- `git pull`
- Fetch + merge
- Safer fetch + merge workflow
- Reset vs revert
- `git revert <commit>`
- Branch pointer
- History rewriting
- New undo commit
- Shared branch safety
- Final quick-summary table

The final quick-summary from page 5 is preserved as well:

| Concept | Safe for Team? | Rewrites History? |
|---|---:|---:|
| Merge | Yes | No |
| Rebase | No (shared) | Yes |
| Reset | No | Yes |
| Revert | Yes | No |

---

# FINAL MASTER MEMORY

```text
             GIT INTERVIEW
                   |
     +-------------+-------------+
     |             |             |
   BRANCH        UNDO          REMOTE
     |             |             |
 Merge/Rebase   Reset/Revert   Fetch/Pull
     |             |             |
   Hotfix        Stash          Clone/Fork
     |
 Cherry-pick
     |
 Branching Strategies
     |
 Git Flow / GitHub Flow / Trunk-Based
```

> **One-line interview memory:**
>
> **For shared collaboration use merge, for local history cleanup use rebase, for a production emergency use hotfix, for one specific commit use cherry-pick, for temporary unfinished work use stash, and for shared-history undo use revert instead of reset.**

