# MODIFICATION.md — divergence catalog

Tracks every intentional divergence between this fork and upstream
`backstage/charts` (path `charts/backstage`).

## Per-file divergence

### `Chart.yaml`
- `version: 2.7.0-cc.1` (vs upstream `2.7.0`).
- `appVersion: 2.7.0-cc.1` — upstream omits `appVersion`; we pin it so
  Argo CD shows the command-center revision on the Application card.
- `name`: unchanged (`backstage`) — keeps drop-in compatibility for
  consumers that use the upstream chart name.
- `description`: rewritten to reference the command-center fork.
- `home` / `sources` / `maintainers`: re-pointed at `ai-blaise/*`.
- `keywords`: added `ai-blaise`, `command-center`.
- `annotations.artifacthub.io/links`: re-pointed at fork URLs but retain
  an `Upstream Chart Source` link for traceability.

### `values.yaml`
- `backstage.image.repository`: `backstage/backstage` -> `ai-blaise/backstage`
  (registry unchanged at `ghcr.io`; together they yield
  `ghcr.io/ai-blaise/backstage`, the command-center image, via the
  bitnami `common.images.image` helper).
- Everything else: held at upstream defaults — overlays live in the
  consumer (`gitops/.../values.yaml` on `ai-blaise/command-center`).

### `templates/`
- No fork edits at initialization (`v2.7.0-cc.1`).
- Any future edits MUST be added here with a short rationale.

### Added files (not in upstream)
- `CC_README.md` — fork relationship, versioning scheme, rebase cadence.
- `MODIFICATION.md` — this file.
- `.github/workflows/publish-chart.yml` — packages and pushes to
  `oci://ghcr.io/ai-blaise/charts/` on push to `main`.

## How to read this file during a rebase

1. Before `git merge upstream/main`, re-read each section above.
2. After the merge, re-apply or re-verify every divergence.
3. Update this file: bump dated entries, add any new divergences.
4. Bump `Chart.yaml` `version` / `appVersion` to the new
   `<upstream-ver>-cc.1`.
