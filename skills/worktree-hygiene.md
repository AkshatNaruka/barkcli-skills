---
id: worktree-hygiene
name: Worktree Hygiene
description: Keep bark worktrees and branches disposable
triggers: [worktree, branch, merged, cleanup]
---
# Worktree Hygiene

The runner lives by the worktree/merge-train pattern. Keep the workspace sane:

1. **Branches are disposable.** `bark/<task-id>` branches merge or are
   re-dispatched; a branch that lingers after a terminal outcome is stale —
   delete it and cut fresh next attempt.
2. **Never commit in main.** The main checkout stays clean; agents never
   inherit a dirty tree (the runner refuses worktree acquisition otherwise).
3. **Rebase > merge** inside a worktree when tracking main; the runner does
   the final `--no-ff` merge itself.
4. **One change per branch.** Mixed refactors + features poison gate reruns
   and conflict resolution.
