<!-- markdownlint-disable -->

# Hardening Report: mxschmitt--action-tmate/v3.22

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mxschmitt--action-tmate/v3.22** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable tag-based refs (@v4, @v3) instead of immutable 40-character SHA commit digests. This exposes the workflow to supply-chain attacks if the upstream action tag is moved or compromised. Failing references: actions/checkout@v4 and actions/setup-node@v3 in checkin.yml; actions/checkout@v4 (×2) in manual-test.yml; actions/checkout@v4 in manual-detached-test.yml.

Locations:

- `.github/workflows/checkin.yml:11`
- `.github/workflows/checkin.yml:13`
- `.github/workflows/manual-test.yml:17`
- `.github/workflows/manual-test.yml:35`
- `.github/workflows/manual-detached-test.yml:7`

### missing-permissions (severity: medium)

None of the workflow files define a top-level `permissions:` block, and no individual job within them defines job-level permissions either. Without explicit permissions, workflows run with the default (potentially broad) GITHUB_TOKEN permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/checkin.yml:1`
- `.github/workflows/manual-test.yml:1`
- `.github/workflows/manual-detached-test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 3 workflow files: (1) Pinned all mutable action refs to full SHA digests — actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 (5 occurrences across checkin.yml, manual-test.yml, manual-detached-test.yml) and actions/setup-node@v3 → @3235b876344d2a9aa001b8d1453c930bba69e610 (1 occurrence in checkin.yml). Original tag names preserved as inline comments. (2) Added top-level `permissions: {}` block to all three workflow files to enforce least-privilege GITHUB_TOKEN access.

