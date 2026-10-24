# barkcli-skills

Community registry of skills for [barkcli](https://github.com/AkshatNaruka/barkcli) —
small markdown files the autonomy loop prepends to agent prompts when a task
matches their triggers.

## Install

```shell
barkcli skills install AkshatNaruka/barkcli-skills
```

Everything installed is pinned in your project's `skills.lock` (source, rev,
sha256). Re-run after a registry update to refresh pinned copies.

## Submit

```shell
barkcli skills publish my-skill
```

Opens a PR (a git branch + `gh pr create`) against this repo.
