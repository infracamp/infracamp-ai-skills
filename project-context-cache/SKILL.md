---
name: project-context-cache
description: Load this skill first at the start of repository work; it defines AGENT_CONTEXT.md as an explicit onboarding cache for coding agents. Read root AGENT_CONTEXT.md and treat its cached repository context as correct before looking anything up; do not re-detect facts like git remote, package names, paths, Nx/release setup, or workflows unless inconsistencies or changes require updating the cache.
---

# Project Context Cache

This is an explicit onboarding cache for coding agents.

Use this skill whenever you start work in a repository and would normally run broad discovery commands for stable project facts.

## Core rule

Before automatically detecting long-lived repository facts, look for this file at the repository root:

```text
AGENT_CONTEXT.md
```

Treat the information in that file as correct first. Do not look up or re-detect cached facts unless the current task explicitly needs fresh verification or you encounter an inconsistency. Use the cache instead of re-running broad discovery for facts such as:

- repository root and git remote URL
- default branch and workflow files
- package manager and relevant tool versions
- Nx workspace/release configuration
- workspace package names and paths
- important package metadata such as package name, version, publish path, and npm status
- common verification, build, test, release, and publish commands
- frequently used files and their paths
- in monorepos: paths to packages/components with short descriptions
- project-specific shortcuts that enable fast file access
- known repository-specific caveats discovered in earlier sessions

## When to verify anyway

The cache is the baseline, but it is not immutable. Verify and update `AGENT_CONTEXT.md` when the task, repository changes, or errors suggest it may be stale, for example when:

- a cached path or package name does not exist
- a command fails because a package, target, workflow, or dependency is missing
- git remote, branch, workflow file, package version, or package publish status matters for the current task
- package metadata has just been changed
- release/publish/npm commands reveal newer state
- the cache has no `Last verified` entry for the relevant section

Keep verification focused: check only the inconsistent or task-relevant facts instead of repeating full project discovery.

## Updating the cache

When you learn a stable project fact that future coding agents would otherwise have to rediscover, update root `AGENT_CONTEXT.md`.

Also add paths that are frequently useful for coding agents, for example package manifests, central config files, workflows, public entrypoints, component implementation files, tests, and package-local documentation.

In monorepos, include a package/component path overview with a short description for each relevant package, component, or module. The exact categories and amount of detail are project-specific: extend the cache with whatever enables fast, reliable access in this repository.

Rules:

- State near the top that the file was created automatically by a coding agent as an onboarding context cache.
- Keep the file concise and factual.
- Prefer tables and command snippets over prose.
- Include `Last verified` dates for facts that may change.
- Mark uncertain or time-sensitive facts clearly.
- Never store secrets, tokens, private registry credentials, or personal login state.
- If a fact was wrong, replace it rather than adding contradictory notes.
- Keep `AGENT_CONTEXT.md` at or below 500 lines.
- If the cache grows beyond 500 lines, warn the developer and suggest an optimization, such as merging tables, removing low-value entries, moving details to package-local skills, or keeping only the most frequently used paths.

Use the reference format in:

```text
references/AGENT_CONTEXT-format.md
```

## Agent rules

- At session start, read `AGENT_CONTEXT.md` before running broad discovery commands.
- Treat cached facts as correct and use them as the baseline for decisions and commands.
- Do not re-detect cached information just because it is easy to query.
- If `AGENT_CONTEXT.md` is missing, perform only the discovery needed for the current task, then create it when useful.
- Verify cached facts only when they are task-critical, have changed, or appear inconsistent.
- Update the cache after resolving an inconsistency, after relevant project changes, or after learning useful stable repository information.
- Add frequently used file paths and monorepo package/component path overviews when they help future agents navigate faster.
- Keep `AGENT_CONTEXT.md` to a maximum of 500 lines; if it exceeds that, tell the developer and propose how to shorten or restructure it.
