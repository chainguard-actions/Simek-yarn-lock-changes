<!-- markdownlint-disable -->

# Hardening Report: Simek--yarn-lock-changes/v0.13.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Simek--yarn-lock-changes/v0.13.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files use action references pinned to mutable version tags instead of immutable 40-character commit SHAs. In main.yml: `actions/checkout@v6`. In tests.yml: `actions/checkout@v6` and `actions/setup-node@v6`. These tags can be moved to point to different (potentially malicious) commits, enabling supply-chain attacks.

Locations:

- `.github/workflows/main.yml:10`
- `.github/workflows/tests.yml:7`
- `.github/workflows/tests.yml:9`

### missing-permissions (severity: medium)

The workflow file tests.yml has no top-level `permissions:` key and its only job (`test`) also has no job-level `permissions:` key. Without explicit permissions, the job inherits the default repository token permissions, which may be overly broad (e.g., write access to contents). A minimal explicit permissions block should be added.

Locations:

- `.github/workflows/tests.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all findings in both workflow files:
1. main.yml: Pinned `actions/checkout@v6` → `actions/checkout@d23441a48e516b6c34aea4fa41551a30e30af803 # v6`
2. tests.yml: Pinned `actions/checkout@v6` → `actions/checkout@d23441a48e516b6c34aea4fa41551a30e30af803 # v6` and `actions/setup-node@v6` → `actions/setup-node@249970729cb0ef3589644e2896645e5dc5ba9c38 # v6`
3. tests.yml: Added top-level `permissions: {}` to explicitly restrict the default token permissions to none.

