# Infracamp AI Skills

Reusable programming and operations workflows for coding agents. The skills
follow the open [Agent Skills specification](https://agentskills.io/specification)
and are intended to work from a shared `.agents/skills` directory.

Use repository instructions such as `AGENTS.md` for rules that apply to every
task. Use a skill for specialized knowledge or a repeatable workflow that should
only be loaded when relevant.

## Install as a submodule

```bash
git submodule add -b main git@github.com:infracamp/infracamp-ai-skills.git .agents/skills/infracamp-ai-skills
```

Dann - damit du nicht immer manuell gegen origin pushen musst:

```bash
cd .agents/skills/infracamp-ai-skills
git fetch origin
git switch main
git branch --set-upstream-to=origin/main main
``

Update an existing checkout with:

```bash
git submodule update --init --recursive --remote
```

When changing this repository through a submodule checkout, commit and push the
skill repository first, then update the submodule commit in the consuming
repository.

## Skill categories

- Coding workflows: verification, debugging, review, and dependency upgrades
- TypeScript and Nx: library layout, monorepo setup, and releases
- Skill distribution: authoring package skills and consuming published skills
- Runtime operations: ChatGPT Work and browser screenshots
- Repository knowledge: architecture contracts and opt-in onboarding caches

See [SKILL_INDEX.md](SKILL_INDEX.md) for the generated catalog.

## Validate

```bash
python3 scripts/validate_skills.py
```

The validator checks frontmatter, directory names, descriptions, relative
Markdown links, index freshness, and empty placeholder directories.

## Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md) before adding or restructuring a skill.
