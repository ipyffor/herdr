# FORK

This is a personal fork of [ogulcancelik/herdr](https://github.com/ogulcancelik/herdr).

## differences from upstream

- **Show agent working directory in sidebar** — the sidebar agent detail panel displays the agent's current working directory basename in parentheses next to the workspace name, making it easier to distinguish multiple agents running in different subdirectories of the same workspace.

## syncing with upstream

```bash
git remote add upstream https://github.com/ogulcancelik/herdr.git
git fetch upstream
git rebase upstream/master
```
