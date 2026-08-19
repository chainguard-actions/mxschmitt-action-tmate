<!-- markdownlint-disable -->

# Hardening Report: mxschmitt--action-tmate/v3.20

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **mxschmitt--action-tmate/v3.20** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All three workflow files reference actions using mutable tag refs instead of full 40-character commit SHA pins, making them vulnerable to supply-chain attacks if the upstream tag is moved.

Failing references:
- checkin.yml: `actions/checkout@v4` and `actions/setup-node@v3`
- manual-detached-test.yml: `actions/checkout@v4`
- manual-test.yml: `actions/checkout@v4` (used twice)

Locations:

- `.github/workflows/checkin.yml:11`
- `.github/workflows/checkin.yml:13`
- `.github/workflows/manual-detached-test.yml:6`
- `.github/workflows/manual-test.yml:14`
- `.github/workflows/manual-test.yml:30`

### missing-permissions (severity: medium)

None of the three workflow files define a top-level `permissions:` block, and no job within them defines job-level `permissions:` either. Without explicit permissions, workflows run with the default (potentially broad) token permissions granted by the repository or organization settings, violating the principle of least privilege.

Locations:

- `.github/workflows/checkin.yml:1`
- `.github/workflows/manual-test.yml:1`
- `.github/workflows/manual-detached-test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 3 workflow files: (1) Pinned all unpinned action references to full 40-char commit SHAs — actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 (5 occurrences across 3 files) and actions/setup-node@v3 → @3235b876344d2a9aa001b8d1453c930bba69e610 (1 occurrence in checkin.yml). (2) Added top-level `permissions: {}` block to all three workflow files (checkin.yml, manual-detached-test.yml, manual-test.yml) to enforce least privilege.

