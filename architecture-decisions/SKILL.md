---
name: architecture-decisions
description: "Use only when developing inside a concrete repository or package and changing complex components, package structure, data flow, DOM/layout behavior, or other foundational design. Search repository and relevant package roots for ARCHITECTURE.md next to language-independent project manifests; read every applicable file and treat it as binding. Do not use for consuming or integrating a published library. Editing ARCHITECTURE.md itself requires explicit developer approval."
---

# Architecture Decisions

Use this skill only while developing the concrete source project when a task can affect its fundamental structure. Do not invoke it merely because an application consumes, imports, configures, or integrates a published library.

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
- Never edit, rename, move, or delete an applicable `ARCHITECTURE.md` without explicit developer approval for that architecture-document change. General approval to implement a feature, fix, or refactor is not sufficient.
- Change an architecture contract only when the developer explicitly asks for or approves the exact architecture change.
- When an approved architecture change is implemented, update the applicable `ARCHITECTURE.md` and related internal references, tests, and examples in the same work.

## Documentation placement

Store durable architecture decisions in `ARCHITECTURE.md` at the repository or relevant package root. Do not place them in runtime/onboarding caches such as `AGENT_CONTEXT.md`.

`ARCHITECTURE.md` is internal source-project guidance for maintainers and coding agents. Do not publish or bundle it in npm, Composer, PyPI, crate, binary, documentation-site, or other consumer-facing package artifacts. It is not part of a library's public usage documentation or API and must not influence ordinary library-consumer decisions.

Keep the document focused on stable decisions: component model, ownership, boundaries, data flow, layout/DOM contracts, lifecycle, invariants, and deliberate non-goals. Operational facts that are merely expensive to rediscover remain in the project context cache.
