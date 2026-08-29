---
name: architecture-decisions
description: "Use before coding or changing complex components, package structure, data flow, DOM/layout behavior, or other foundational design. Search repository and relevant package roots for ARCHITECTURE.md next to language-independent project manifests such as package.json, composer.json, pyproject.toml, Cargo.toml, go.mod, or project files; read every applicable file and treat its decisions and invariants as binding unless the maintainer explicitly requests an architecture change."
---

# Architecture Decisions

Use this skill before implementation when a task can affect a project's or package's fundamental structure.

## Discovery

Search for `ARCHITECTURE.md` in:

- the repository root;
- the root of each package or project touched by the task;
- the nearest parent directory that contains a project manifest or workspace configuration.

Ignore generated, dependency, build, vendor, and workspace-mirror directories. Keep discovery scoped to the repository and packages relevant to the task.

Read every applicable `ARCHITECTURE.md` completely before proposing or making changes. A repository-root contract applies globally. A package-local contract adds more specific rules for that package; it does not silently override a global contract unless the documents explicitly say so.

## Binding contract

Treat documented architecture decisions, invariants, ownership boundaries, lifecycle rules, and prohibited alternatives as requirements.

- Preserve the established structure during ordinary feature work, fixes, refactoring, tests, demos, and styling changes.
- Prefer an implementation that fits the contract over a locally simpler alternative that changes the model.
- Do not migrate, replace, bypass, or gradually erode the architecture as incidental cleanup.
- If the requested work conflicts with the contract, stop and explain the conflict before editing.
- Change an architecture contract only when the maintainer explicitly asks for or approves an architecture change.
- When an approved architecture change is implemented, update the applicable `ARCHITECTURE.md` and related skills, references, tests, and examples in the same work.

## Documentation placement

Store durable architecture decisions in `ARCHITECTURE.md` at the repository or relevant package root. Do not place them in runtime/onboarding caches such as `AGENT_CONTEXT.md`.

Keep the document focused on stable decisions: component model, ownership, boundaries, data flow, layout/DOM contracts, lifecycle, invariants, and deliberate non-goals. Operational facts that are merely expensive to rediscover remain in the project context cache.
