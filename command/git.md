# Git Command Notes

This document collects useful Git commands for daily work.

---

## 1. Undo Last Commit

There are two common ways to undo the last commit, depending on whether it has been pushed or not.

### 1.1 Local Only (Commit Not Pushed)

If the commit has not been pushed to a remote, you can reset the branch to the previous commit:

```bash
git reset --soft HEAD~1   # Undo commit, keep changes staged
git reset --mixed HEAD~1  # Undo commit, keep changes unstaged
git reset --hard HEAD~1   # Undo commit, discard changes
```

### 1.2 Remote (Commit Already Pushed)

If the commit has been pushed, you should not reset history (to avoid breaking others’ clones).
Instead, create a new commit that reverts the changes:

```bash
git revert <commit-hash>
```

This will open an editor to confirm the revert message, then create a new commit that undoes the changes.

---
