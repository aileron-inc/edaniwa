# Repository Guide

This repo is a small wrapper around bare clones in `core/` and checked-out worktrees in `tree/`, with helper scripts in `bin/` to keep them in sync.

## bin/
- `clone`: `bin/clone <owner/repo>` clones the given repository into `core/<repo>` as a bare repo (skips if it already exists).
- `worktree`: `bin/worktree <owner/repo> <branch> [base-ref=main]` adds a worktree at `tree/<repo>/<branch>`, fetching first; creates the branch from the base ref if it does not exist.
- `update-core`: `bin/update-core <owner/repo>` fetches and prunes the bare repo under `core/`.
- `update-tree`: `bin/update-tree <owner/repo> <branch>` fetches the worktree at `tree/<repo>/<branch>` and rebases it onto its upstream (fails if the worktree is dirty or on a different branch).
- `remove-tree`: `bin/remove-tree <owner/repo> <branch> [--force]` or `bin/remove-tree tree/<repo>/<branch> [--force]` removes a worktree (checks branch match; fails if dirty unless `--force`); also prunes stale worktree metadata in the bare repo.

### Typical flow
1. `bin/clone <owner/repo>` once to create the bare repo in `core/`.
2. `bin/worktree <owner/repo> <branch>` to create a working directory under `tree/` for your branch.
3. Work inside `tree/<repo>/<branch>`, commit/push as usual.
4. Keep things fresh with `bin/update-core` before adding new worktrees and `bin/update-tree` to rebase an existing one.
5. When you are done with a branch, `bin/remove-tree <owner/repo> <branch>` (or the `tree/<repo>/<branch>` path) to drop the worktree safely.

## core/ と tree/
- `core/` 配下は bare clone の保管場所だよ。ここは直接作業しないでバックエンドとして扱ってね。
- `tree/` 配下は `bin/worktree` で作る各ブランチの作業ディレクトリだよ。中身は作業者やブランチごとに変わるから、この README では具体的な構成には触れていないよ。

## License
- MIT
