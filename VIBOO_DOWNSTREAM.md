# Viboo downstream release

This branch contains Viboo-specific changes on top of Canonical Argo Operators.

The changes are maintained internally and have not been submitted to the upstream repository.

## Base

- Upstream repository: `canonical/argo-operators`
- Upstream tag: `argo-controller/rev971`
- Upstream commit: `6205ea8da9bac1f27c687ab8f635020ffc46c133`

## Downstream concerns

- `fix(argo-controller): accept bucket from S3 provider`
- `fix(argo-controller): honor archive key format config`

Each concern is a separate commit so it can be retained, changed, or removed independently during an upgrade.

## Verification

Pushes to `release/**` run `.github/workflows/viboo-downstream-ci.yaml`.

The workflow lints and tests `argo-controller`, packs the charm, and stores the `.charm` file as a GitHub Actions artifact.

## Upgrade procedure

1. Create a new release branch from the exact new upstream tag or commit.
2. Evaluate each downstream concern against the new upstream source.
3. Omit a concern if the new upstream source already provides equivalent behavior.
4. Cherry-pick each remaining concern separately and resolve any semantic changes.
5. Run the downstream CI workflow.
6. Deploy the packed charm to DEV with the existing `juju refresh --path` process.
7. Promote the same source commit to PROD only after DEV verification.
