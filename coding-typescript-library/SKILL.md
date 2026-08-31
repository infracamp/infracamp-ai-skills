---
name: coding-typescript-library
description: Create or extend publishable TypeScript libraries, including their public exports, source layout, declaration output, module compatibility, and focused tests. Use for library packages; do not use for ordinary TypeScript applications or Nx workspace configuration.
---

# TypeScript library coding

Follow the target repository's established package layout and build tooling.
The conventions below are Infracamp defaults when the repository has no more
specific rule.

## Public package surface

- Keep the public entrypoint at package root as `index.ts` next to
  `package.json`; keep implementation under `src/`.
- Export only supported public APIs from the entrypoint.
- Keep internal helpers unexported and avoid consumers depending on source
  paths.
- Ensure `package.json` exports, type declarations, and built output agree with
  the public entrypoint.
- Check ESM/CommonJS expectations and browser or Node runtime compatibility
  from the existing package before changing build settings.

## Implementation and verification

- Put web components under `src/components/` when that matches the package.
- Keep focused unit tests next to implementation as `*.spec.ts`.
- Put integration or end-to-end coverage under `tests/e2e/` only when the
  behavior crosses package or runtime boundaries.
- Prefer the repository's existing Vite setup. Do not introduce or replace a
  bundler as incidental cleanup.
- Preserve the decorator model already used by the repository; for new code,
  prefer current standard decorators when the configured toolchain supports
  them.
- Verify imports from the package entrypoint, declaration generation, and the
  relevant build or test target.

Use `nx-monorepo-setup` for workspace configuration, generators, `project.json`,
or new Nx packages.
