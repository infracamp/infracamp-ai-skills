# `AGENT_CONTEXT.md` reference format

Place this file at the repository root:

```text
AGENT_CONTEXT.md
```

The cache should contain stable project facts and frequently used paths that are repeatedly needed by coding agents and expensive or noisy to rediscover. Keep the file at or below 500 lines.

## Recommended structure

```md
# Agent Context Cache

Last updated: YYYY-MM-DD

> This file was created automatically by a coding agent as an onboarding context cache.
> Cached repository facts for coding agents. Use as a baseline before running
> broad discovery commands. Verify and update focused sections when errors or
> task requirements indicate stale information.

## Project identity

| Key | Value |
| --- | --- |
| Repository root | `/path/to/repo` |
| Git remote | `git@github.com:owner/repo.git` |
| Default branch | `main` |
| Package manager | `npm` |
| Node requirement | `>=22` |

Last verified: YYYY-MM-DD

## Workspace and tools

| Tool | Configuration |
| --- | --- |
| Nx preset | `nx/presets/npm.json` |
| Workspace packages | `packages/*` |
| Release relationship | `independent` |
| Release pre-version command | `npx nx run-many -t build` |
| Publish workflow | `.github/workflows/publish-tags.yml` |

Last verified: YYYY-MM-DD

## Packages

| Package | Path | Version | Notes |
| --- | --- | --- | --- |
| `@scope/package-a` | `packages/package-a` | `0.1.0` | public npm package |
| `@scope/package-b` | `packages/package-b` | `0.0.0` | private/demo/reference package |

Last verified: YYYY-MM-DD

## Frequently used files

| Purpose | Path | Notes |
| --- | --- | --- |
| Root package manifest | `package.json` | workspace scripts and dev dependencies |
| Nx config | `nx.json` | workspace layout and release settings |
| Publish workflow | `.github/workflows/publish-tags.yml` | npm trusted publishing identity |
| Main package entrypoint | `packages/package-a/index.ts` | public exports |

Last verified: YYYY-MM-DD

## Monorepo package/component paths

| Name | Path | Description |
| --- | --- | --- |
| `@scope/package-a` | `packages/package-a` | short package purpose |
| `ComponentA` | `packages/package-a/src/component-a.ts` | main web component implementation |
| `PackageATests` | `packages/package-a/src/component-a.spec.ts` | component tests |

Use this section project-specifically: add packages, components, modules, tests, docs, or config files that future agents are likely to open frequently. Keep descriptions short.

Last verified: YYYY-MM-DD

## Release and publish commands

```bash
# targeted checks
npx nx run-many -p <package-name> -t lint typecheck test build

# first manual publish, if package has never existed on npm
cd packages/<package>
npm publish --access public

# configure trusted publishing after first npm publish
npm trust github <package-name> \
  --repo <owner>/<repo> \
  --file <workflow-file>.yml \
  --allow-publish \
  --yes

# normal release preparation after trusted publishing exists
npx nx release patch --skip-publish -p <package-name>
git push --follow-tags origin main
```

## Known facts from previous sessions

- `@scope/package-a` was not published on npm as of YYYY-MM-DD. Verify before first publish or trust setup.
- The publish workflow is tag-based and expects tags matching `*@*.*.*`.
- `npm login` is the user-facing login command for npm authentication in the container.

## Cache maintenance notes

- Update package versions after release preparation.
- Update npm publish/trust status after npm commands succeed.
- Update workflow names when `.github/workflows/*` changes.
- Add frequently used paths when they save future agents broad discovery work.
- In monorepos, keep package/component paths current after moves, renames, or new packages.
- Keep this file at or below 500 lines.
- If it exceeds 500 lines, warn the developer and suggest an optimization: merge tables, remove low-value entries, move detailed package knowledge to package-local skills, or keep only high-frequency paths.
- Remove stale facts instead of keeping contradictory history.
```

## What belongs in the cache

Good cache entries:

- facts read from `package.json`, `nx.json`, and workflow files
- package names and directories
- frequently used file paths with short descriptions
- monorepo package/component/module paths with short descriptions
- repository URL and workflow filename for npm trusted publishing
- known command sequences that already worked in this repository
- task-relevant caveats discovered in previous sessions

Avoid:

- secrets or auth tokens
- personal npm login state, except a generic note that login is required
- large file listings
- exhaustive source trees instead of curated high-value paths
- generated command output dumps
- guesses without a verification date
- content that makes the file longer than 500 lines without strong value
