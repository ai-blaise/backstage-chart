# backstage-chart (command-center fork)

This is the ai-blaise command-center Helm chart for deploying the
[`ai-blaise/backstage`](https://github.com/ai-blaise/backstage) fork. It is
forked from upstream [`backstage/charts`](https://github.com/backstage/charts)
(specifically `charts/backstage`) so the command-center platform can ship
images and behavior that differ from upstream without carrying the entire
charts monorepo.

## Versioning: `<upstream-ver>-cc.N`

All chart versions in this repo are tagged as `<upstream-ver>-cc.N`:

- `<upstream-ver>` mirrors the upstream `backstage/charts` chart version
  (taken from `charts/backstage/Chart.yaml`).
- `cc.N` is the command-center revision (1, 2, 3 ...) — bump for any
  fork-only edit that does not move `<upstream-ver>`.
- When the upstream chart version moves, reset `cc.N` to `1` after the
  rebase merge.

Tag every release `v<upstream-ver>-cc.N` (e.g. `v2.7.0-cc.1`). The
publish-chart workflow packages and pushes to
`oci://ghcr.io/ai-blaise/charts/`.

## Rebase cadence

- Watch upstream `backstage/charts` on a **monthly** cadence (or sooner if a
  CVE drops). Track upstream `main` against the `upstream/` remote.
- Each rebase: `git fetch upstream && git merge upstream/main`, resolve, bump
  `<upstream-ver>` to the new upstream version, reset `cc.N` to `1`, update
  `MODIFICATION.md`, and cut a new tag.
- Open the rebase PR with the upstream commit range in the description.

## Relationship to upstream

| Aspect              | Upstream `backstage/charts`            | This fork                                       |
|---------------------|----------------------------------------|-------------------------------------------------|
| Chart name          | `backstage`                            | `backstage` (same — drop-in)                    |
| Default image       | `ghcr.io/backstage/backstage`          | `ghcr.io/ai-blaise/backstage`                   |
| Versioning          | `M.m.p`                                | `M.m.p-cc.N`                                    |
| Distribution        | `oci://ghcr.io/backstage/charts/`      | `oci://ghcr.io/ai-blaise/charts/`               |
| Maintainer          | Backstage                              | ai-blaise (command-center)                      |

See `MODIFICATION.md` for the divergence catalog.
