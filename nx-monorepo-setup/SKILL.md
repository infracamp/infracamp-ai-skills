---
name: nx-monorepo-setup
description: Use this skill when creating, configuring, or maintaining Nx monorepos, root Nx workspace config, or new Nx library packages.
---

# Nx Monorepo Setup

Use this skill for Nx workspace setup and for creating or checking new packages in an Nx monorepo.

## References

This skill contains two reference snapshots from a working Nx repository.

### Global Nx workspace config

Use this reference for root-level repository setup:

```text
references/nx-repo-config/
```

Included example files:

- `nx.json`
- `package.json`
- `project.json`
- `tsconfig.base.json`
- `tsconfig.json`
- `vite.config.ts`
- `vitest.workspace.ts`
- `eslint.config.mjs`

Use this for target defaults, release setup, workspace scripts, path aliases, root TypeScript config, root Vite/Vitest config, and ESLint setup. Do not copy project-specific package names or paths blindly; adapt them to the target repository.

### Minimal Nx package setup

Use this reference for new Nx library packages:

```text
references/nx-base-package/
```

Included example package files/templates:

- `project.json.template`
- `package.json.template`
- `README.md.template`
- `web-types.json.template`
- `index.ts.template`
- `vite.config.ts.template`
- `tsconfig.json.template`
- `tsconfig.lib.json.template`
- `tsconfig.spec.json.template`
- `src/components/__name__/__name__.ts.template`
- `src/components/__name__/__name__.spec.ts.template`
- `src/lib/utils.ts`

This package reference is intentionally minimal. It excludes outdated or optional files such as AI usage info, Kindergarden config, SCSS, HTML demos, and extra documentation fragments. Package-local skills remain optional, but the templates include `skills` in the npm package files/assets so they are published when present.

## Package structure rules

For new Nx TypeScript library packages:

- keep `index.ts` in the package root next to `package.json`
- do not place the public entrypoint under `src/`
- put implementation files under `src/`
- put unit tests next to implementation files as `*.spec.ts`
- use Vite for build/test setup when the repository already uses Vite
- keep package config close to the minimal package reference unless the target repo has stricter local templates

Recommended minimal shape:

```text
<package>/
  project.json
  package.json
  README.md
  web-types.json
  index.ts
  vite.config.ts
  tsconfig.json
  tsconfig.lib.json
  tsconfig.spec.json
  src/
    components/<component-name>/
      <component-name>.ts
      <component-name>.spec.ts
    lib/
      utils.ts
```

Do not add AI usage info, Kindergarden config, SCSS, HTML, demos, or package-local skills by default. Add optional files only when the user asks for them or the existing repository pattern requires them. If package-local skills exist under `skills/`, keep `skills` included in `package.json` `files` and Vite/Nx assets so they are published to npm.

## Workflow

When working on an Nx monorepo:

1. Check whether the repository already has generator/templates for packages.
2. Prefer repository-local generators/templates over the bundled references.
3. Use `references/nx-repo-config/` for root workspace setup patterns.
4. Use `references/nx-base-package/` for package-level setup patterns.
5. Keep changes small and avoid restructuring existing Nx config unless requested.
6. For new packages, register required path aliases or workspace references according to the repository's existing conventions.

## Agent rules

- Use this skill for Nx root config, Nx release config, package project config, and creating new Nx packages.
- Do not put Nx workspace setup guidance into generic TypeScript coding skills.
- Prefer the current repository's own config/generator over these reference snapshots when available.
- Adapt names, paths, ports, package scopes, and release settings to the target repository.
- Do not add optional package files by default.
