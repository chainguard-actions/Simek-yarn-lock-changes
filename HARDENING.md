<!-- markdownlint-disable -->

# Hardening Report: Simek--yarn-lock-changes/v0.12.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Simek--yarn-lock-changes/v0.12.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference GitHub Actions using mutable tag-based refs (@v4) instead of full 40-character commit SHA pins. This exposes the workflow to supply-chain attacks if the upstream action tag is moved or compromised. Failing references: .github/workflows/main.yml uses actions/checkout@v4; .github/workflows/tests.yml uses actions/checkout@v4 and actions/setup-node@v4.

Locations:

- `.github/workflows/main.yml:10`
- `.github/workflows/tests.yml:8`
- `.github/workflows/tests.yml:11`

### missing-permissions (severity: medium)

The workflow file tests.yml has no top-level `permissions:` key and its only job (`test`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository default token permissions, which may be overly broad. A minimal explicit permissions block should be added.

Locations:

- `.github/workflows/tests.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all findings in both workflow files:
1. unpinned-uses: Pinned actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 # v4 in main.yml and tests.yml; pinned actions/setup-node@v4 → @49933ea5288caeca8642d1e84afbd3f7d6820020 # v4 in tests.yml.
2. missing-permissions: Added top-level `permissions: {}` to tests.yml to restrict default token permissions, with a job-level `permissions: pull-requests: write` for the test job (required since the action posts PR comments about yarn lock changes).

