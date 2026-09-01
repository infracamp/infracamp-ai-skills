---
name: coding-guardrails
description: MUST be read before every task that may modify code, configuration, dependencies, builds, workflows, tests, or implementation documentation. Enforces minimal scope, simple solutions, and escalation instead of workarounds when expected packages, APIs, methods, exports, or artifacts are unavailable.
---

# Coding guardrails

- Change only what the user requested or what is strictly necessary for it.
- Before changing code, read all comments in the affected section. Check them for invariants, dependencies, compatibility constraints, workarounds, and coupled functionality. If the planned change could violate such guidance or impair other functionality, inform the user before making the change and wait for their decision.
- When user feedback identifies a required correction to code you wrote, add a brief code comment if the corrected behavior is not fully self-explanatory. Explain the requirement or invariant, not the conversation or change history.
- Prefer the simplest intended solution; avoid speculative abstractions, unrelated cleanup, and broad refactoring.
- Before recommending or running any non-standard command or action that may cause side effects, warn the user and get explicit approval.
- Do not hide missing packages, APIs, methods, exports, configuration, or artifacts with workarounds - ask the user to escalate instead.
- Do not add undeclared packages or install transitive dependencies directly to mask a dependency defect.
- If something expected is unavailable, stop, report the evidence, and ask whether setup, version, publication, generation, or source is missing.
- Ask before expanding scope or making structural changes.
- Document public library APIs with a usage example in the header, or link to a maintained example. Include important usage guidance.
- When editing code, flag outdated related examples and ask whether to update them.
- Before changing a skill, read `skill-authoring` and get user approval for the exact wording before applying it.
- DO NOT change code inside `node_modules`, `dist`, `vendor`, `workspaces` unless explicitly requested - ask if changes are needed there.
- DO NOT read or change code inside package-locked or package-generated files unless explicitly requested - ask if changes are needed there - normally `npm <command>` or `npm update` should be used instead.

Keep this skill very compact. Retain only universal, high-impact rules and move specialized guidance into focused skills.
