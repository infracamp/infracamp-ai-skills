# Contributing

Create a skill only for non-obvious expertise or a repeatable workflow that an
agent should load for a specific class of task. Put rules that apply to every
task in repository instructions instead.

## Skill requirements

- Use a lowercase, hyphenated directory name matching the frontmatter `name`.
- Describe both what the skill does and when it should activate.
- Keep the entrypoint concise and move conditional detail to focused
  `references/` files.
- Link every reference from `SKILL.md` and state when it should be read.
- Include scripts only when deterministic execution is materially better than
  regenerating commands. Document their dependencies and failure behavior.
- Avoid generic programming advice, project-specific incidents, absolute local
  paths, duplicated rules, and empty resource directories.
- Add `compatibility` when a skill requires a particular runtime, service,
  network path, or system package.

## Review checklist

1. Test the description with realistic prompts that should and should not
   activate the skill, including close negative cases.
2. Exercise changed scripts and the observable workflow they support.
3. Run `python3 scripts/validate_skills.py`.
4. Update generated files through their generator; do not hand-edit the skill
   index.
5. Confirm the diff contains no credentials, login state, temporary paths, or
   incident-specific data.
