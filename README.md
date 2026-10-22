# CDD Lab Experiment 3

**Aim:** To perform Git branching, merging, rebasing, and merge conflict resolution.

## Operations Performed

1. **Branching and merging:** Created `feature/profile`, added `profile.txt`, and merged the branch into `main`.
2. **Rebasing:** Created `feature/contact`, committed a separate update on `main`, rebased the feature onto the updated branch, and merged it.
3. **Conflict resolution:** Made different changes to the same line of `settings.txt` on `main` and `feature/title`. Resolved the conflict and completed the merge commit.

## Key Commands

```bash
git switch -c <branch>
git merge <branch>
git rebase main
git status
git add <file>
git commit -m "message"
```

## Result

All three operations are represented in the repository history. The final `main` branch contains `profile.txt`, `contact.txt`, `status.txt`, and the resolved `settings.txt`.
