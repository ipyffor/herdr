# FORK

This is a personal fork of [ogulcancelik/herdr](https://github.com/ogulcancelik/herdr).

## differences from upstream

- **Show agent working directory in sidebar** — the sidebar agent detail panel displays the agent's current working directory basename in parentheses next to the workspace name, making it easier to distinguish multiple agents running in different subdirectories of the same workspace.

## versioning

Fork versions use the format `<upstream>-fork.<n>` (e.g., `0.7.1-fork.1`):

- `0.7.1` — the upstream release this fork is based on
- `fork.1` — the fork iteration number

When upstream releases a new version and the fork rebases, reset the counter: `0.7.2-fork.1`.

## creating a fork release

```bash
# Bump the fork version in Cargo.toml, then tag and push:
git tag v0.7.1-fork.1
git push origin v0.7.1-fork.1
```

The `fork-release.yml` workflow builds Linux (x86_64, aarch64) and macOS (x86_64, aarch64) binaries and creates a GitHub Release.

## syncing with upstream

```bash
git remote add upstream https://github.com/ogulcancelik/herdr.git
git fetch upstream
git checkout master
git rebase upstream/master
git checkout fork
git rebase master
```
