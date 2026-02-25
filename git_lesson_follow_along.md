# Git Lesson Handout (Carpentries-aligned, 90-minute flow)

This handout is a truncated classroom path based on Software Carpentry Git Novice. Use it in class, then continue the full Carpentries lesson on your own.

References:
- <https://swcarpentry.github.io/git-novice/index.html>
- <https://swcarpentry.github.io/git-novice/instructor/index.html>

## Carpentries lesson map

| Lesson block | Carpentries lessons used |
| --- | --- |
| Motivation | [01 Automated Version Control](https://swcarpentry.github.io/git-novice/01-basics.html) |
| Block 1 | [02 Setting Up Git](https://swcarpentry.github.io/git-novice/02-setup.html), [03 Creating a Repository](https://swcarpentry.github.io/git-novice/03-create.html), [04 Tracking Changes](https://swcarpentry.github.io/git-novice/04-changes.html) |
| Block 2 | [05 Exploring History](https://swcarpentry.github.io/git-novice/05-history.html), [06 Ignoring Things](https://swcarpentry.github.io/git-novice/06-ignore.html), [07 Remotes in GitHub](https://swcarpentry.github.io/git-novice/07-github.html), [08 Collaborating](https://swcarpentry.github.io/git-novice/08-collab.html) |
| Block 3 | [09 Conflicts](https://swcarpentry.github.io/git-novice/09-conflict.html) |

## 0) Why use Git?

Carpentries lesson used: [01 Automated Version Control](https://swcarpentry.github.io/git-novice/01-basics.html)

When people work without version control, they often end up with many copies of the same file and no reliable way to know which one is correct.

![Manual file version chaos (PhD comics)](carpentries_figures/phd101212s.png)

Git solves this by recording changes over time. Instead of saving many independent copies, you save a sequence of meaningful snapshots called commits.

![Changes played forward in time](carpentries_figures/play-changes.svg)

Because changes are tracked, you can inspect history, recover older versions, and understand how your current file came to be.

![Two versions from one base](carpentries_figures/versions.svg)

This also makes collaboration practical. Multiple people can work from the same starting point, and Git can combine non-overlapping changes.

![Merging independent changes](carpentries_figures/merge.svg)

When changes overlap, Git marks a conflict and asks humans to decide the final content. That is a normal part of collaborative work, not a failure.

## How to use this handout

Work through each block in order. Each block starts with a short concept explanation and then command steps. Use one terminal window throughout. Run this lesson once in a fresh folder.

## 1) Block 1: Local workflow fundamentals

Carpentries lessons used: [02 Setting Up Git](https://swcarpentry.github.io/git-novice/02-setup.html), [03 Creating a Repository](https://swcarpentry.github.io/git-novice/03-create.html), [04 Tracking Changes](https://swcarpentry.github.io/git-novice/04-changes.html)

At the core of Git is a simple model: you edit files in your working tree, choose what belongs in the next snapshot with `git add`, and save that snapshot with `git commit`.

![Staging area model](carpentries_figures/git-staging-area.svg)

You can stage files independently and then commit related changes together as one logical unit.

![Committing multiple files](carpentries_figures/git-committing.svg)

A practical beginner loop is: edit -> `git status` -> `git add` -> `git commit`.

![Full local workflow cartoon](carpentries_figures/git_staging.svg)

### Step 1. Configure identity (once per machine)

```bash
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### Step 2. Create a repository

```bash
mkdir -p git-lesson
cd git-lesson
mkdir -p recipes
cd recipes
git init -b main
git status
```

### Step 3. Create `guacamole.md` and make first commit

Create/edit the file with `nano`:

```bash
nano guacamole.md
```

Paste this content:

```text
# Guacamole
## Ingredients
## Instructions
```

Then run:

```bash
cat guacamole.md
git status
git add guacamole.md
git commit -m "Create initial structure for a Guacamole recipe"
git log --oneline
```

### Step 4. Edit file, inspect diff, make second commit

Edit the file again:

```bash
nano guacamole.md
```

Replace content with:

```text
# Guacamole
## Ingredients
* avocado
* lime
* salt
## Instructions
```

Then run:

```bash
git diff
git add guacamole.md
git commit -m "Add ingredients for basic guacamole"
git log --oneline
```

Checkpoint: you should now have at least 2 commits.

## 2) Block 2: History, ignore rules, remotes, collaboration

Carpentries lessons used: [05 Exploring History](https://swcarpentry.github.io/git-novice/05-history.html), [06 Ignoring Things](https://swcarpentry.github.io/git-novice/06-ignore.html), [07 Remotes in GitHub](https://swcarpentry.github.io/git-novice/07-github.html), [08 Collaborating](https://swcarpentry.github.io/git-novice/08-collab.html)

Before collaborating, it helps to understand how to inspect and recover file states.

![Restore concept](carpentries_figures/git-restore.svg)

`git diff` compares versions, while `git restore` can discard local edits or recover file content from another commit.

### Step 5. Explore recent history

```bash
git diff HEAD~1 guacamole.md
git log --oneline
git log guacamole.md
```

### Step 6. Ignore generated/unimportant files

```bash
mkdir -p pictures
touch a.png b.png c.png pictures/cake1.jpg pictures/cake2.jpg
nano .gitignore
```

Put this in `.gitignore`:

```text
*.png
pictures/
```

Then run:

```bash
cat .gitignore
git status
git add .gitignore
git commit -m "Ignore png files and the pictures folder."
git status
```

Next comes remotes. A local repository and a hosted/shared repository are separate copies connected by a URL.

![Create repo screen 1](carpentries_figures/github-create-repo-01.png)
![Create repo screen 2](carpentries_figures/github-create-repo-02.png)
![Create repo screen 3](carpentries_figures/github-create-repo-03.png)

![Fresh local vs empty remote](carpentries_figures/git-freshly-made-github-repo.svg)

The remote URL is what `git remote add origin <URL>` stores.

![Find repository URL](carpentries_figures/github-find-repo-string.png)
![Repository URL detail](carpentries_figures/github-change-repo-string.png)

After that, `git push` sends commits to the remote and `git pull` integrates remote commits locally.

![After first push model](carpentries_figures/github-repo-after-first-push.svg)

### Step 7. Add remote and push (classroom-safe local remote)

In class we use a local bare repository so everyone can practice the real commands without account/login setup.

```bash
cd ..
git clone --bare recipes recipes-remote.git
cd recipes
git remote add origin ../recipes-remote.git
git remote -v
git push origin main
```

Collaboration works because each person has their own clone and syncs through the shared remote.

![Add collaborators (hosted platforms)](carpentries_figures/github-add-collaborators.png)
![Collaboration flow](carpentries_figures/github-collaboration.svg)

### Step 8. Simulate collaborator change (`hummus.md`)

```bash
cd ..
git clone recipes-remote.git alflin-recipes
cd alflin-recipes
nano hummus.md
```

Paste this content:

```text
# Hummus
## Ingredients
* chickpeas
* lemon
* olive oil
* salt
```

Then run:

```bash
git add hummus.md
git commit -m "Add ingredients for hummus"
git push origin main
```

### Step 9. Pull collaborator change into owner copy

```bash
cd ../recipes
git pull --no-rebase origin main
ls
```

Checkpoint: `hummus.md` should now be present in `recipes`.

## 3) Block 3: Conflict workflow

Carpentries lesson used: [09 Conflicts](https://swcarpentry.github.io/git-novice/09-conflict.html)

Conflicts happen when two commits modify overlapping lines. Git shows both versions and waits for you to decide the final text.

![Conflict model](carpentries_figures/conflict.svg)

### Step 10. Collaborator edits instructions line and pushes

```bash
cd ../alflin-recipes
nano guacamole.md
```

Set content to:

```text
# Guacamole
## Ingredients
* avocado
* lime
* salt
## Instructions
* put one avocado into a bowl.
```

Then run:

```bash
git add guacamole.md
git commit -m "First step on the instructions"
git push origin main
```

### Step 11. Owner makes a different edit and then pulls

```bash
cd ../recipes
nano guacamole.md
```

Set content to:

```text
# Guacamole
## Ingredients
* avocado
* lime
* salt
## Instructions
* peel the avocados
```

Then run:

```bash
git add guacamole.md
git commit -m "Add first step"
git pull --no-rebase origin main
git status
cat guacamole.md
```

When the conflict appears, the markers mean:
- `<<<<<<< HEAD` is your local version.
- `=======` separates the two versions.
- `>>>>>>>` marks the incoming version.

### Step 12. Resolve conflict and complete merge

Edit `guacamole.md` so it becomes:

```text
# Guacamole
## Ingredients
* avocado
* lime
* salt
## Instructions
* peel the avocados and put them into a bowl.
```

Then run:

```bash
git add guacamole.md
git commit -m "Merge changes from GitHub"
git push origin main
git log --oneline --graph -5
```

Checkpoint: you should see the merge commit in the graph.

## 4) End-of-lesson recap

Git gives you a reliable history, clear collaboration workflow, and a safe way to resolve overlapping edits. The key rhythm is: inspect with `status`, stage with `add`, save with `commit`, synchronize with `push`/`pull`, and resolve conflicts when needed.

Recommended self-study in Carpentries:
- Episode 5 (more history tools)
- Episode 7 (full hosted remote setup)
- Episode 8 (collaboration workflow practice)
- Episode 9 (more conflict scenarios)
- Episodes 10-14 (Open Science, licensing, citations, hosting, etc)
