<!-- markdownlint-disable -->

# Hardening Report: Simek--yarn-lock-changes/v0.14.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Simek--yarn-lock-changes/v0.14.1** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow files reference GitHub Actions using mutable version tags (@v6) instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit. Affected references: actions/checkout@v6 and actions/setup-node@v6.

Locations:

- `.github/workflows/lint.yml:9`
- `.github/workflows/lint.yml:11`
- `.github/workflows/main.yml:9`
- `.github/workflows/tests.yml:10`
- `.github/workflows/tests.yml:11`

### missing-permissions (severity: medium)

lint.yml has no top-level `permissions:` key and its only job ('test') also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the default repository permissions, which may be overly broad (e.g. write access to contents).

Locations:

- `.github/workflows/lint.yml:1`

### missing-permissions (severity: medium)

tests.yml has no top-level `permissions:` key and its only job ('test') also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the default repository permissions, which may be overly broad.

Locations:

- `.github/workflows/tests.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all three workflow files: (1) Pinned actions/checkout@v6 to SHA d23441a48e516b6c34aea4fa41551a30e30af803 and actions/setup-node@v6 to SHA 249970729cb0ef3589644e2896645e5dc5ba9c38 in lint.yml, main.yml, and tests.yml. (2) Added top-level `permissions: {}` to lint.yml and tests.yml to prevent inheriting overly broad default repository permissions. main.yml already had a job-level `permissions: pull-requests: write` block which is the minimum needed for its function.

