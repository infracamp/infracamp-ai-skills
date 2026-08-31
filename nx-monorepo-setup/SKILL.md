---
name: nx-monorepo-setup
description: Create or maintain Nx workspaces, project configuration, generators, targets, caching, and new Nx library packages. Use for root Nx configuration or package scaffolding; do not use for implementation inside an existing TypeScript library or for publishing releases.
compatibility: Requires an Nx workspace; bundled reference snapshots assume Node.js, npm, Vite, and the Infracamp Kickstart environment.
---

# Nx monorepo setup

Inspect the installed Nx version, existing workspace configuration, local
generators, and neighboring projects before changing configuration. Prefer the
repository's generators and conventions over bundled snapshots.

## Route the work

- For root targets, release groups, caching, TypeScript paths, Vite/Vitest,
  ESLint, or Kickstart configuration, consult `references/nx-repo-config/` and
  adapt it rather than copying project names or paths.
- For a new library package, consult `references/nx-base-package/` only after
  checking for a repository-local generator or template.
- For TypeScript public API, exports, declaration output, implementation layout,
  and tests, use `coding-typescript-library`.
- For versioning and publishing, use `nx-release-and-npm-config`.

## Nx-specific requirements

- Register projects, targets, dependencies, path aliases, and release settings
  according to the current workspace model.
- Keep target inputs and outputs accurate so Nx caching and affected commands do
  not reuse stale artifacts or miss dependents.
- Adapt package names, scopes, ports, runtime commands, and output paths to the
  target repository.
- Add optional demo, style, documentation, or package-skill files only when the
  user requested them or the repository's generator defines them.
- If package-local skills exist, ensure the package build and npm metadata ship
  the `skills/` directory.
- In repositories using Kickstart, run project commands in the configured
  container rather than starting a parallel host runtime.

Verify the affected Nx graph or project configuration plus the narrowest
relevant target. Do not restructure unrelated workspace configuration as part of
creating or updating one package.
