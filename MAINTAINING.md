# Maintaining

## Source of truth

**This repository is the canonical source of the adapter.**

- Develop, test, tag, and release here (`main`).
- The fork `yaoyongli1974-dotcom/oh-my-cortex` branch `feat/opencode-v2-adapter` is a
  **submission snapshot only**. It exists to carry the adapter into an upstream PR; it is not a
  development branch.
- Installed copies (`~/.config/opencode/omx-v2`, project `.opencode/plugins/omx-v2.js`,
  project `.opencode/agents/`) are artifacts. Re-run `install.sh` after changing this repo.

## Changing the adapter

1. Edit `adapter.js` / scripts / `agents/` here on `main`.
2. Run the checks:

   ```bash
   node --check adapter.js
   for f in *.sh; do bash -n "$f"; done
   ```

3. Smoke test against a scratch project:

   ```bash
   ./install.sh /tmp/omx-smoke
   cd /tmp/omx-smoke
   opencode run --agent Chief---Deepworker -m <provider/model> "Say SMOKE-OK only."
   ```

4. Commit and push to `main`.
5. Tag releases with `vX.Y.Z` and publish release notes.

## Updating the upstream PR

The fork branch and this repo have unrelated histories; do not merge them.

When the PR needs a refresh:

1. Copy the changed files from this repo into the fork branch under `adapters/opencode-v2/`.
2. Squash or amend into a clean commit on `feat/opencode-v2-adapter`.
3. Force-push the branch. The open PR updates automatically.

Only the adapter directory is published to the fork. The standalone repository's own
`LICENSE.md` and `NOTICE.md` live at its root; the fork inherits the upstream root `LICENSE.md`.

## Generated agents

`agents/*.md` are generated from oh-my-cortex's config handler. When bumping the supported
oh-my-cortex version:

1. Install the new version into `~/.local/share/opencode/omx-v2`.
2. Delete the generated files in a scratch project and start OpenCode once to regenerate them.
3. Copy the regenerated files here and review the diff.
4. Update the version pin in `install.sh` and the README compatibility line.
