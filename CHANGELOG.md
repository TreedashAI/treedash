# Changelog

## [Unreleased]

### Added

- **Browser tab switching** _(Sponsor)_ — in VS Code Remote Tunnel sessions in a browser, clicking a worker now switches to that worker's browser tab (or opens it in the right window) via the new **TreeDash Companion** extension (`subtrees-private/browser-ext`, Chrome/Edge dev build) with Convex as the rendezvous. Without the companion (or on free tier), clicks switch in place in the current tab — no more broken multi-window attempts on the web.
- **Worker branch namespaces** — worker branches are now `td/<worker>/<feature>` (the repo-name segment is gone), with a workspace-scoped `treedash.branchPrefix` toggle (default on, also in the panel's General settings) to disable the `td/` namespace and follow the repo's own branch convention.
- **Agent conventions in the repo** — on init, TreeDash writes a managed block into `AGENTS.md` and `CLAUDE.md` describing its worktree + branch-naming conventions, so any AI agent working in the repo follows them (gated by `treedash.branchPrefix`). Uninit removes the block; only TreeDash's delimited block is touched.
- **Services dashboard** — a "Services" card in the panel shows which developer CLIs (GitHub, Vercel, npm, Git, Convex) are installed and which account you're signed in as.
- **Hide worker action buttons** — `treedash.showWorkerActions` (default off) hides the per-worker Commit/Push/Rebase/Merge buttons, for agent-driven git workflows.

### Changed

- Corrected the `treedash.commitCommand` description — it runs as a background process (output streams into the Commit popup), not in a terminal

### Fixed

- Re-initializing now adopts the configured `treedash.mainBranch` (e.g. renaming a local repo's `main` to `dev`) instead of staying on the old branch

## [0.0.8] - 2026-03-20

### Changed

- Removed redundant API calls on webview ready — `fetchSync()` now handles all server data in one batched call

## [0.0.7] - 2026-03-19

### Added

- Worker instance IDs — each worker gets a unique ID, scoping merge history per user
- User ownership tracking — workers and changes are tied to the user who created them
- Cross-window auth sync — sign in/out in one window updates all open windows instantly
- Automated commit-rebase-merge flow — when Main has uncommitted changes during merge, prompts to commit then automatically rebases and merges
- Auto Commit inline spinner — closes popup immediately, shows spinner next to Changes heading with buttons disabled until done

### Changed

- Rebase button disabled when worker has uncommitted changes (tooltip: "Commit changes first before rebasing")
- Changes list scoped by user — signed-in users only see their own commits and merges, guests only see guest activity
- Uninit no longer deletes .git directory, preserving the repo for continued use
- Server sync optimized — single fetchSync() call replaces multiple separate API calls on auth change and startup
- Sign-in no longer flashes default worker names — customizations load before UI updates

### Fixed

- "wId is not defined" error when merging a worker
- Worker ID tag stripped from merge commit display in Changes list

## [0.0.6] - 2026-03-17

### Fixed

- Fix extension activation failure ("CONVEX_SITE_URL is not defined")

## [0.0.5] - 2026-03-16

### Initial Release

- Visual dashboard in VS Code secondary sidebar for managing git worktrees
- Up to 8 color-coded workers, each with its own isolated worktree and branch
- One-click rebase from main and merge back with conflict resolution
- Full task history with revert and remerge support
- Worker customization — names, initials, shapes, colors, text colors, and SVG icons (Sponsor tiers)
- GitHub OAuth sign-in with settings sync across devices
- Keyboard shortcuts for quick worker switching (`Alt+1`–`Alt+8`)
- In-panel settings with Main Branch and Commit Command configuration
- Searchable FAQ with expand/collapse
- Free tier: 2 workers. Patron ($10/mo): 4 workers + shortcuts. Patron Max ($20/mo): 8 workers + full customization.
