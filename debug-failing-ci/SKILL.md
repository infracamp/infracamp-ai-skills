---
name: debug-failing-ci
description: Diagnose and fix failing CI workflows by locating the relevant run and failed job, extracting the first actionable error, reproducing it locally when practical, and verifying the correction. Use for GitHub Actions or comparable CI failures; do not use for a generic local runtime bug without CI evidence.
---

# Debug failing CI

## Workflow

1. Resolve the exact repository, branch or pull request, workflow run, and failed
   job. Do not assume the most recent failure belongs to the requested change.
2. Read the failed step summary and a focused log segment around the first
   actionable error. Avoid loading complete logs unless the focused evidence is
   insufficient.
3. Separate the root failure from canceled jobs and downstream errors.
4. Compare the CI runtime, dependency installation, environment variables,
   working directory, and command with the repository's local setup.
5. Reproduce the failing command locally when the required environment is
   available.
6. If a declared package is unavailable after the repository's normal install,
   or one of its expected transitive dependencies is missing, stop and inform
   the developer that the package is not available as expected. Do not hide the
   packaging, publishing, registry, workspace-link, or lockfile defect by adding
   undeclared packages or explicitly installing transitive dependencies in CI.
7. Make only the fix supported by the evidence, then run the relevant local
   verification.
8. If authorized to update the pull request, inspect the new CI run. Otherwise
   report the expected verification step.

Never expose secrets from logs. Treat missing credentials, protected
environments, permission errors, and external service outages as blockers rather
than code defects unless evidence shows otherwise.
