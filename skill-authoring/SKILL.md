---
name: skill-authoring
description: Create, restructure, or review Agent Skills and their SKILL.md files. Use when defining skill boundaries, improving activation descriptions, organizing references or scripts, validating a skill collection, or migrating legacy AI guidance into skills.
---

# Skill authoring

Create skills for specialized knowledge and repeatable workflows. Do not turn
rules that apply to every repository task into an always-triggered skill; place
those in repository instructions instead.

## Workflow

1. Identify realistic requests the skill should and should not handle.
2. Choose one coherent task or audience. Split only when activation intent or
   required context differs materially.
3. Write a discriminating description that says what the skill does and when it
   applies.
4. Keep essential routing and constraints in `SKILL.md`. Move conditional
   procedures to focused references and deterministic repeated work to scripts.
5. Validate the skill and exercise its real workflow.
6. Update `SKILL_INDEX.md` through `scripts/validate_skills.py --write-index`.

Avoid generic advice the agent already knows, exhaustive edge-case catalogs,
duplicated instructions, placeholder directories, and environment-specific
paths without a compatibility declaration.

For package-distributed skills, use `package-skill-authoring` in
`create-package-skills`. For the detailed legacy migration considerations, read
[references/legacy-ai-usage-info.md](references/legacy-ai-usage-info.md) only
when `.ai-usage-info.md` is present.

## Evaluation

Test activation with realistic positive and close negative prompts. Test output
quality against observable criteria such as required artifacts, commands,
invariants, and prohibited side effects. Prefer evidence from real repository
tasks, review comments, incidents, and successful fixes over generic templates.
