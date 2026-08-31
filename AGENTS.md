# Agent instructions

These rules apply whenever an agent changes code in a repository that includes
this skill set. They are stable working conventions, not optional skills.

- Preserve the user's scope. Do not add unrelated refactors, dependencies,
  tests, documentation, or generated files.
- Prefer existing project patterns, utilities, APIs, and file structures over
  new abstractions.
- Keep changes focused and explain material scope expansion before doing it.
- Read applicable repository and package instructions before editing.
- Never edit generated dependencies in `node_modules` or `vendor`.
- Do not import package source through `node_modules`, `workspaces`, or another
  package's internal source path. Use its public package entrypoint.
- Use the repository's package manager for dependency and lockfile changes.
- Re-read files before follow-up edits because the developer may have changed
  them between turns.
- Verify the behavior affected by the change with the narrowest meaningful
  build, test, lint, demo, or runtime check available.
- Report what changed, how it was verified, and any remaining limitation.

Repository- or framework-specific conventions belong in the relevant project
instructions or a narrowly triggered skill, not in this file.
