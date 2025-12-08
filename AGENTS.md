# Repository Agent Guide

- Base clone is managed via `bin/clone <owner/repo>`; it creates `core/<repo>` as a bare repo for worktree dispatch. Do not work directly in `core/`.
- Call Codex first for ideation,そしてコマンド発行も Codex に任せる。アイデアが固まったら Codex 経由で `bin/worktree <owner/repo> <branch> [base-ref]` を実行し、作業は `tree/<branch>` で行う。
- Always `git --git-dir=core/<repo> fetch --all --prune` before adding new worktrees if the repo may be stale.
- Avoid long-running servers; coordinate with the user if needed.

## Worktree quickstart
- Pattern: `tree/<project>/<topic>` for worktree paths; use branches `<project>/<topic>` to match.
- Create a worktree: `bash bin/worktree <RepoName> <project>/<topic> [base-ref=origin/main]` (script is non-executable by default).
- If network access blocks fetch, add from existing refs: `git --git-dir=core/<RepoName> worktree add -b <project>/<topic> tree/<project>/<topic> <base-ref>` (default base `main`).
