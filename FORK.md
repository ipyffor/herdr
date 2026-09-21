# FORK

This is a personal fork of [ogulcancelik/herdr](https://github.com/ogulcancelik/herdr).

## differences from upstream

- **Show agent working directory in sidebar** — sidebar agent rows append the agent pane's working directory basename in parentheses to the workspace name, so agents running in different subdirectories of the same workspace can be told apart.
- **Accent bar on focused sidebar items** — the focused workspace and agent rows carry an accent half-block on their left edge. The active-row background fill on its own is barely distinguishable from the panel background.

Both are client-side rendering changes. Neither touches shared runtime state or
the protocol.

## dropped: server-side remote mirror

An earlier branch (`dev-server-hub-merge`) mirrored remote Herdr servers into the
local server's own state, so remote workspaces became first-class local
workspaces for any local API consumer.

Upstream 0.9.0 shipped `herdr machine` (#3670) with the same user-facing goal — one
window for Local and several saved SSH servers — using a client-side
multi-endpoint design instead. It covers bridging, workspace and agent listing,
navigation, reconnects, and CLI routing, and adds things the fork never had:
incremental surface streaming (vs. 300 ms full-screen polling), health checks,
SSH compression, Windows hosts, and client/server capability negotiation.

The fork's approach was dropped in favour of upstream's. The two are mutually
exclusive architectures, so keeping both would mean maintaining a parallel
remote stack for no additional user-facing capability. Do not revisit this
without a concrete capability that saved machines cannot provide.

## versioning

Fork versions use the format `<upstream>-fork.<n>` (e.g., `0.9.1-fork.1`):

- `0.9.1` — the upstream release this fork is based on
- `fork.1` — the fork iteration number

When upstream releases a new version and the fork rebases, reset the counter:
`0.9.2-fork.1`.

`Cargo.toml` always mirrors upstream's version and is never diverged; only
release tags carry the `-fork.<n>` suffix.

## creating a fork release

```bash
# Tag and push:
git tag v0.9.1-fork.1
git push origin v0.9.1-fork.1
```

The `fork-release.yml` workflow builds Linux (x86_64, aarch64) and macOS
(x86_64, aarch64) binaries and creates a GitHub Release.

## syncing with upstream

```bash
git remote add upstream https://github.com/ogulcancelik/herdr.git
git fetch upstream
git checkout master
git rebase upstream/master
git checkout fork
git rebase master
```

If upstream restructures the files a fork commit touches, that rebase can
produce unresolvable conflicts. Rebuilding from `upstream/master` and
re-applying the fork's changes on the new structure is usually faster than
fighting them — that is what the 0.9.1 sync did.
