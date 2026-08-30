# `AGENT_CONTEXT.md` reference format

Adapt this structure to the repository and omit sections that add no value.

```markdown
# Agent Context Cache

Last updated: YYYY-MM-DD

> Operational onboarding cache for coding agents. Verify focused sections when
> task requirements or errors indicate stale information.

## Project identity

| Key | Value |
| --- | --- |
| Repository | `owner/repository` |
| Default branch | `main` |
| Package manager | `npm` |
| Runtime requirement | `Node >=22` |

Last verified: YYYY-MM-DD

## Workspace and packages

| Package | Path | Purpose |
| --- | --- | --- |
| `@scope/package` | `packages/package` | Short description |

## Frequently used files

| Purpose | Path |
| --- | --- |
| Workspace configuration | `nx.json` |
| Package entrypoint | `packages/package/index.ts` |
| Publish workflow | `.github/workflows/publish.yml` |

## Common commands

```bash
npm test
npm run build
```

## Verified operational caveats

- Record only durable, repository-specific facts that change an agent's work.
```

Keep the cache factual, curated, and below 500 lines. Do not include absolute
checkout paths, secrets, current login state, transient command output, or
release status that can be obtained cheaply unless it is dated and repeatedly
useful.
