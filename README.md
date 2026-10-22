# CDD Lab Experiment 3: Branching, Merging, Rebasing, and Merge Conflict Resolution

**Course:** CDD Lab  
**Experiment No.:** 3  
**Aim:** To implement Git branching, merging, rebasing, and resolve merge conflicts.

---

## 1. Objectives

- Create and switch between Git branches.
- Make commits on separate branches and merge a feature branch into `main`.
- Rebase a feature branch onto an updated base branch.
- Create a merge conflict, resolve it manually, and verify the final result.
- Inspect branch history and repository status using Git commands.

## 2. Requirements

- Git installed on the system
- A GitHub account
- Terminal (macOS/Linux Terminal or Windows Git Bash)
- This repository: [CDD-lab-exp3](https://github.com/r-samarth/CDD-lab-exp3)

Check the installation:

```bash
git --version
```

## 3. Key Concepts

| Concept | Meaning |
|---|---|
| Branch | An independent line of development pointing to a commit |
| Merge | Combines the changes from one branch into another |
| Fast-forward merge | Moves the target branch pointer forward when no divergent history exists |
| Three-way merge | Combines histories using a common ancestor |
| Rebase | Replays commits onto a new base, creating new commit IDs |
| Merge conflict | Occurs when Git cannot automatically combine competing changes |
| HEAD | Points to the currently checked-out commit or branch |

> **Important:** Rebasing rewrites commit history. Avoid rebasing commits that other people already depend on unless the team has agreed to it.

---

## 4. Experiment A — Create and Merge Branches

### Step 1: Clone the repository

```bash
git clone https://github.com/r-samarth/CDD-lab-exp3.git
cd CDD-lab-exp3
```

If the repository is empty when you first start the lab, clone it after the README has been added. If you already have a local copy, use that copy.

### Step 2: Check the current branch and status

```bash
git branch
git status
git log --oneline --all --graph
```

These commands show the current branch, working-tree status, and commit history.

### Step 3: Create a feature branch

```bash
git switch -c feature/profile
```

Create a sample file and commit it:

```bash
echo "Profile feature: user details" > profile.txt
git add profile.txt
git commit -m "Add profile feature"
```

### Step 4: Return to main and merge

```bash
git switch main
git merge feature/profile
```

If your default branch is named `master`, use `master` instead of `main`.

Verify the result:

```bash
git log --oneline --graph --all
git status
```

**Expected result:** The profile feature is included in the target branch. Git may perform a fast-forward merge if the target branch has not advanced independently.

---

## 5. Experiment B — Rebase a Feature Branch

This exercise demonstrates how a feature branch can be updated on top of a newer base commit.

### Step 1: Create a feature branch and commit

```bash
git switch main
git switch -c feature/contact
echo "Contact feature: email and phone" > contact.txt
git add contact.txt
git commit -m "Add contact feature"
```

### Step 2: Add a separate commit to main

```bash
git switch main
echo "Project status: active" > status.txt
git add status.txt
git commit -m "Add project status"
```

### Step 3: Rebase the feature branch

```bash
git switch feature/contact
git rebase main
```

Git replays the contact feature commit on top of the latest `main` commit.

### Step 4: Inspect the history

```bash
git log --oneline --graph --decorate --all
git status
```

**Expected result:** The feature branch contains the latest `main` history followed by the contact feature commit. The rebased commit has a new commit ID.

To finish integrating the feature:

```bash
git switch main
git merge feature/contact
```

Because the feature branch has been rebased on top of `main`, this merge can usually be fast-forwarded.

---

## 6. Experiment C — Create and Resolve a Merge Conflict

A conflict can occur when two branches edit the same lines in the same file.

### Step 1: Create a common starting file

Start from a clean working tree:

```bash
git switch main
echo "Application title: CDD Demo" > settings.txt
git add settings.txt
git commit -m "Add application settings"
```

If Git reports that there is nothing to commit, the file may already exist. Inspect it with `cat settings.txt` and continue using a clean, committed starting point.

### Step 2: Change the same line on a feature branch

```bash
git switch -c feature/title
echo "Application title: Branching Demo" > settings.txt
git add settings.txt
git commit -m "Update title on feature branch"
```

### Step 3: Make a different change on main

```bash
git switch main
echo "Application title: Git Lab Demo" > settings.txt
git add settings.txt
git commit -m "Update title on main"
```

### Step 4: Attempt to merge

```bash
git merge feature/title
```

**Expected result:** Git reports a content conflict in `settings.txt`. The file may contain conflict markers similar to:

```text
<<<<<<< HEAD
Application title: Git Lab Demo
=======
Application title: Branching Demo
>>>>>>> feature/title
```

- `<<<<<<< HEAD` marks the version from the current branch.
- `=======` separates the competing versions.
- `>>>>>>> feature/title` marks the incoming branch version.

### Step 5: Resolve the conflict

Open `settings.txt` in a text editor and choose the final content. For example:

```text
Application title: Git Lab Demo
```

Remove all conflict markers, then stage and commit the resolution:

```bash
git add settings.txt
git commit -m "Resolve title merge conflict"
```

### Step 6: Verify the resolution

```bash
cat settings.txt
git status
git log --oneline --graph --decorate --all
```

**Expected result:** The file contains the selected final title, no conflict markers remain, and the working tree is clean.

If you need to cancel a merge before resolving it, use `git merge --abort`. During a rebase conflict, resolve the files, stage them, and run `git rebase --continue`; use `git rebase --abort` to cancel the rebase.

---

## 7. Useful Commands

| Command | Purpose |
|---|---|
| `git branch` | List local branches |
| `git switch -c <name>` | Create and switch to a branch |
| `git switch <name>` | Switch branches |
| `git merge <branch>` | Merge a branch into the current branch |
| `git rebase <branch>` | Replay current-branch commits on another base |
| `git status` | Inspect working-tree and conflict status |
| `git diff` | View unstaged changes |
| `git diff --staged` | View staged changes |
| `git log --oneline --graph --decorate --all` | Visualize commit history |
| `git merge --abort` | Cancel an in-progress merge |
| `git rebase --continue` | Continue after resolving a rebase conflict |
| `git rebase --abort` | Cancel an in-progress rebase |

## 8. Troubleshooting

- **Uncommitted changes prevent switching branches:** Run `git status`; commit the changes or temporarily save them with `git stash`.
- **Branch name is not found:** Run `git branch --all` and check the spelling.
- **Conflict is still present:** Edit the file, remove every conflict marker, then run `git add <file>`.
- **Merge is not complete:** Check `git status` and follow Git's instructions to complete or abort it.
- **The default branch is not `main`:** Use the repository's actual default branch name in the commands.

## 9. Result

Git branching, merging, rebasing, and merge conflict resolution were studied and demonstrated. The resulting commit history and repository status were inspected to verify the operations.

## 10. Conclusion

This experiment demonstrates how Git supports parallel development through branches, integrates changes through merging, updates feature work through rebasing, and provides conflict markers and staging tools to resolve incompatible edits. These operations are essential for individual version control and collaborative software development.

---

**Repository:** [r-samarth/CDD-lab-exp3](https://github.com/r-samarth/CDD-lab-exp3)  
**Previous lab repositories:** [Experiment 1](https://github.com/r-samarth/CDD-lab-exp1) · [Experiment 2](https://github.com/r-samarth/CDD-lab-exp2) · [Experiments 4 & 5](https://github.com/r-samarth/CDD-lab-exp-4-and-5)
