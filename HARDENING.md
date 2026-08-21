<!-- markdownlint-disable -->

# Hardening Report: mxschmitt--action-tmate/v3.21

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mxschmitt--action-tmate/v3.21** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference external actions using mutable version tags instead of pinned 40-character SHA digests. This exposes the workflow to supply-chain attacks if the referenced tag is moved or the upstream repository is compromised. Failing references: checkin.yml uses `actions/checkout@v4` and `actions/setup-node@v3`; manual-test.yml uses `actions/checkout@v4`; manual-detached-test.yml uses `actions/checkout@v4`.

Locations:

- `.github/workflows/checkin.yml:10`
- `.github/workflows/checkin.yml:12`
- `.github/workflows/manual-test.yml:18`
- `.github/workflows/manual-detached-test.yml:7`

### missing-permissions (severity: medium)

None of the workflow files define a top-level `permissions:` block, and no individual job defines its own `permissions:` block. Without explicit permissions, workflows run with the default (potentially broad) token permissions. Affected files: checkin.yml, manual-test.yml, manual-detached-test.yml.

Locations:

- `.github/workflows/checkin.yml:1`
- `.github/workflows/manual-test.yml:1`
- `.github/workflows/manual-detached-test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all three workflow files:
1. checkin.yml: Pinned actions/checkout@v4 to SHA 11d5960a326750d5838078e36cf38b85af677262 and actions/setup-node@v3 to SHA 3235b876344d2a9aa001b8d1453c930bba69e610. Added top-level `permissions: {}` and job-level `permissions: contents: read`.
2. manual-test.yml: Pinned both actions/checkout@v4 references to SHA 11d5960a326750d5838078e36cf38b85af677262. Added top-level `permissions: {}` and job-level `permissions: contents: read` for both jobs.
3. manual-detached-test.yml: Pinned actions/checkout@v4 to SHA 11d5960a326750d5838078e36cf38b85af677262. Added top-level `permissions: {}` and job-level `permissions: contents: read`.

