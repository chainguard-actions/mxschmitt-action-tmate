<!-- markdownlint-disable -->

# Hardening Report: mxschmitt--action-tmate/v3.23

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mxschmitt--action-tmate/v3.23** was hardened automatically. 6 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow uses action references pinned to mutable tags instead of immutable full-length SHA commit hashes. This exposes the workflow to supply-chain attacks if the tag is moved. Failing references: `actions/checkout@v4`, `actions/setup-node@v3`.

Locations:

- `.github/workflows/checkin.yml:11`
- `.github/workflows/checkin.yml:13`

### unpinned-uses (severity: high)

Workflow uses action references pinned to mutable tags instead of immutable full-length SHA commit hashes. Failing reference: `actions/checkout@v4`.

Locations:

- `.github/workflows/manual-detached-test.yml:8`

### unpinned-uses (severity: high)

Workflow uses action references pinned to mutable tags instead of immutable full-length SHA commit hashes. Failing references: `msys2/setup-msys2@v2`, `actions/checkout@v4` (appears twice).

Locations:

- `.github/workflows/manual-test.yml:44`
- `.github/workflows/manual-test.yml:55`
- `.github/workflows/manual-test.yml:62`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/checkin.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions.

Locations:

- `.github/workflows/manual-detached-test.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions.

Locations:

- `.github/workflows/manual-test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 6 findings across 3 workflow files:

1. checkin.yml: Pinned actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 and actions/setup-node@v3 → @3235b876344d2a9aa001b8d1453c930bba69e610. Added top-level `permissions: {}`.

2. manual-detached-test.yml: Pinned actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262. Added top-level `permissions: {}`.

3. manual-test.yml: Pinned msys2/setup-msys2@v2 → @66cd2cce69caa17b53920067426061ca1de3a884 and both occurrences of actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262. Added top-level `permissions: {}`. All original tag names preserved as inline comments.

