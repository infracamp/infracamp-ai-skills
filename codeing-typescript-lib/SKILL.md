---
name: codeing-typescript-lib
description: Use this skill when creating or extending TypeScript libraries in monorepos such as Nx workspaces.
---

# TypeScript Library Coding

Use this skill when creating or adapting TypeScript libraries, especially in Nx monorepos.

## Core structure

Important rule:

- `index.ts` must always live in the **package root** next to `package.json`
- do **not** place the public entrypoint under `src/`

Reason:

- the library should work both via `npm install` and via workspace linking
- consumers should not need to manually adjust import paths depending on whether the package is consumed from npm or from the monorepo

## Recommended library layout

```text
packages/<library>/
  package.json
  index.ts
  index.scss ## ONly if the library exports global styles
  vite.config.ts
  tsconfig.json
  tsconfig.lib.json
  tsconfig.spec.json
  src/
    components/<component-name>/
        <component-name>.ts
        <component-name>.spec.ts
        <component-name>.scss
    lib/<helper-name>.ts
  style/  ## only if the library exports global styles
     <mixin-name>.scss  
  tests/
```

## Source code placement

- put the actual implementation into `src/`
- put web components under `src/components/`
- keep `index.ts` as the public export surface
- re-export from root `index.ts` only what should be public API

Example:

```ts
export * from './src/components/my-element';
export * from './src/lib/my-helper';
```

## Tests

- unit tests live next to the implementation files as `*.spec.ts`
- keep tests intentionally **small and focused**, unless the user explicitly asks for broader coverage
- avoid large, over-engineered test suites by default

Examples:

```text
src/lib/my-helper.ts
src/lib/my-helper.spec.ts

src/components/my-element.ts
src/components/my-element.spec.ts
```

## Integration tests

If integration or end-to-end tests are needed, place them under:

```text
tests/e2e/
```

Only add them when needed.

## Bundler standard

- use **Vite** as the standard bundler
- orient new libraries to the existing Vite/Nx setup in the repository
- prefer small, repository-consistent Vite configs over custom build setups

## Decorators

- always use the new native ES decorators
- do not introduce legacy TypeScript decorator syntax or old decorator patterns
- when working with decorators, stay compatible with the current native decorator standard used by modern TypeScript and JavaScript tooling

## Agent rules

- keep the package entrypoint at `./index.ts` in the package root
- keep implementation in `src/`
- keep web components in `src/components/`
- keep unit tests as small `*.spec.ts` files next to the source files
- put integration tests under `tests/e2e/` only when required
- prefer Vite for build/dev/test integration unless the user explicitly asks for something else
- always use the new native ES decorators
- follow the existing repository structure and avoid inventing a different package layout without a clear reason
