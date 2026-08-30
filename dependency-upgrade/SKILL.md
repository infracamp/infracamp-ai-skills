---
name: dependency-upgrade
description: Upgrade or migrate project dependencies using authoritative release notes, the repository's package manager, and focused compatibility verification. Use when changing dependency versions or adapting code to a dependency release; do not use for adding an unrelated new library.
---

# Dependency upgrade

1. Identify the current version, requested target, package manager, workspace
   scope, and all direct manifests that own the dependency.
2. Read authoritative release notes and migration documentation for the versions
   crossed. Pay particular attention to breaking changes, runtime requirements,
   peer dependencies, deprecated configuration, and security notes.
3. Inspect existing usage before changing manifests so the migration work is
   scoped to APIs the repository actually uses.
4. Update dependencies through the repository's package manager. Do not hand-edit
   lockfile entries.
5. Adapt code and configuration only for relevant documented changes.
6. Run focused package-manager diagnostics plus the affected build, tests, lint,
   or runtime verification.
7. Report the version transition, migrations performed, verification, and any
   remaining deprecation or compatibility risk.

Ask before introducing replacement packages, changing package managers, or
expanding a targeted upgrade into a broad dependency refresh.
