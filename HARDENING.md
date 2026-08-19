<!-- markdownlint-disable -->

# Hardening Report: mxschmitt--action-tmate/v3.24

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mxschmitt--action-tmate/v3.24** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable version tags instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced tag is moved or the repository is compromised. Affected references: checkin.yml uses actions/checkout@v4 and actions/setup-node@v4; manual-detached-test.yml uses actions/checkout@v4; manual-test.yml uses msys2/setup-msys2@v2 and actions/checkout@v4 (twice). All should be pinned to full SHA digests.

Locations:

- `.github/workflows/checkin.yml:11`
- `.github/workflows/checkin.yml:13`
- `.github/workflows/manual-detached-test.yml:8`
- `.github/workflows/manual-test.yml:47`
- `.github/workflows/manual-test.yml:50`
- `.github/workflows/manual-test.yml:58`

### missing-permissions (severity: medium)

None of the three workflow files define a top-level `permissions:` block, and no individual job within them defines job-level permissions either. Without explicit permissions, workflows inherit the default repository token permissions (which may be broad), violating the principle of least privilege. All three files — checkin.yml, manual-test.yml, and manual-detached-test.yml — are affected.

Locations:

- `.github/workflows/checkin.yml:1`
- `.github/workflows/manual-test.yml:1`
- `.github/workflows/manual-detached-test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 3 workflow files: (1) Pinned all unpinned action references to full 40-char SHAs — actions/checkout@v4 → @34e114876b0b11c390a56381ad16ebd13914f8d5, actions/setup-node@v4 → @49933ea5288caeca8642d1e84afbd3f7d6820020, msys2/setup-msys2@v2 → @66cd2cce69caa17b53920067426061ca1de3a884 — with original tag preserved in a comment. (2) Added top-level `permissions: {}` block to checkin.yml, manual-detached-test.yml, and manual-test.yml to enforce least privilege.

