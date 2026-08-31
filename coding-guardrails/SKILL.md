---
name: coding-guardrails
description: MUST be read before every task that may modify code, configuration, dependencies, builds, workflows, tests, or implementation documentation. Enforces minimal scope, simple solutions, and escalation instead of workarounds when expected packages, APIs, methods, exports, or artifacts are unavailable.
---

# Coding guardrails

- Change only what the user requested or what is strictly necessary for it.
- Prefer the simplest intended solution; avoid speculative abstractions, unrelated cleanup, and broad refactoring.
- Do not hide missing packages, APIs, methods, exports, configuration, or artifacts with workarounds - ask the user to escalate instead.
- Do not add undeclared packages or install transitive dependencies directly to mask a dependency defect.
- If something expected is unavailable, stop, report the evidence, and ask whether setup, version, publication, generation, or source is missing.
- Ask before expanding scope or making structural changes.
- Document public library APIs with a usage example in the header, or link to a maintained example. Include important usage guidance.
- When editing code, flag outdated related examples and ask whether to update them.
- DO NOT change code inside `node_modules`, `dist`, `vendor`, `workspaces` unless explicitly requested - ask if changes are needed there.
- DO NOT read or change code inside package-locked or package-generated files unless explicitly requested - ask if changes are needed there - normally `npm <command>` or `npm update` should be used instead.

Keep this skill very compact. Retain only universal, high-impact rules and move specialized guidance into focused skills.

