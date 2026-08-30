---
name: repository-onboarding-cache
description: Create or refresh an AGENT_CONTEXT.md onboarding cache for stable repository facts that are expensive to rediscover. Use when the user asks to document repository context, improve agent onboarding, or refresh an existing cache; do not activate for ordinary repository edits.
---

# Repository onboarding cache

Maintain `AGENT_CONTEXT.md` as a concise operational map, not as an architecture
contract and not as an automatic side effect of unrelated work.

## Contents

Include only stable, useful facts that future agents would otherwise rediscover:

- package manager, workspace structure, and common commands;
- package names and paths;
- central configuration, workflows, entrypoints, and frequently used files;
- operational caveats that have been verified in the repository.

Do not duplicate facts that are already easy to obtain, and do not store
secrets, login state, temporary commit identifiers, architectural decisions, or
binding design contracts. Put architecture contracts in `ARCHITECTURE.md`.

Verify task-relevant facts from source files, label time-sensitive facts with a
last-verified date, replace stale information instead of appending conflicting
notes, and keep the result below 500 lines. Do not create or update the cache
unless the user requested onboarding/cache work or the current task explicitly
includes it.

Use [the reference format](references/AGENT_CONTEXT-format.md) as a starting
point, adapting its sections to the actual repository.
