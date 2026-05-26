# Import progress (agent-forge)

- Remote add attempted: `git remote add biu1-ragme-github https://github.com/sinwulok/biu1-ragme-github.git` (remote already existed)
- Fixed remote URL: `git remote set-url biu1-ragme-github https://github.com/sinwulok/biu1-ragme-github.git`
- Fetched remote (branches & tags): `git fetch biu1-ragme-github --tags`
- Listed remote branches: `git ls-remote --heads biu1-ragme-github` (to choose branch to import)

Next steps (one command at a time, waiting for confirmation):
1. Run subtree add for selected branch into `labs/gh-ragme` (preserve history, no --squash).
2. Repeat process for `sinwulok/biu1-gh-rag2skill` into `tools/gh-rag2skill`.

Rules to follow: preserve full commit history, never use `--squash`, do not modify imported contents, show one command at a time, wait for user after each step.
