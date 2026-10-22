# CDD Lab Experiment 3

**Aim:** To perform Git branching, merging, rebasing, and merge conflict resolution.

## Operations Performed

1. **Branching and merging:** Created `feature/profile`, committed `profile.txt`, and merged the feature into `main`.
2. **Rebasing:** Created `feature/contact`, added a separate commit on `main`, rebased the feature onto the updated `main`, and merged it.
3. **Conflict resolution:** Changed the same line in `settings.txt` on `main` and `feature/title`, resolved the conflict, and committed the final version.

## Commands Used

```bash
git switch -c feature/profile
git add . && git commit -m "Add profile feature"
git switch main && git merge feature/profile

git switch -c feature/contact
git rebase main
git switch main && git merge feature/contact

git merge feature/title
# Edit the conflicted file, then:
git add settings.txt
git commit -m "Resolve settings merge conflict"
```

## Result

Branching, merging, rebasing, and merge conflict resolution were performed and verified through the repository history and final file contents.
