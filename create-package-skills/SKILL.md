---
name: create-package-skills
description: Use this skill when defining or maintaining package-local skills for libraries, components, or packages in this repository.
---

# Create Package Skills

This skill is the successor to the old `ai-usage-info` approach.

Package-specific knowledge should live close to the package itself.
That includes:

- what the package does
- how it should be used
- important implementation patterns
- package-specific constraints
- examples for common use cases

## Preferred format

Create one or more focused package-local skills per package.

Naming convention:

```text
<packagename>-<what>
```

Examples:

```text
form-usage
form-plugins
demo-viewer-navigation
responsive-variants
```

## Preferred location

Preferred new location inside a package:

```text
packages/<package>/skills/<skillname>/
```

Important:

- the `skills/` directory must live on the same level as `package.json`
- do not place package skills under `src/`
- the `skills/` directory must be included in the package build/publish setup
- make sure it is considered both in Vite/Nx asset handling and in the published package metadata from `package.json`

Example:

```text
packages/form/skills/form-usage/SKILL.md
packages/form/skills/form-usage/references/installation.md
```

## Upgrade note

Older package skills may still live under:

```text
packages/<package>/.agents/skills/
```

This is considered the older format.

Prefer the new format instead:

```text
packages/<package>/skills/<skillname>/
```

Do **not** migrate existing `.agents/skills` package skills automatically.
Only migrate them when the user explicitly asks for that migration.

When relevant, mention that the package skill can later be consumed via `skills-npm`.
See the `link-package-skills` skill for that workflow.

## What belongs into the main package skill

The main skill should stay short and focused.

It should:

- clearly state the **element/package name** already in the description
- clearly state the **function/purpose** already in the description
- stay concise
- give the agent a quick understanding of what the package is for
- prefer examples over long explanations

The main skill should usually cover:

- package purpose
- main public API or entrypoints
- important usage patterns
- package-specific do and don'ts
- short examples

## What should not bloat the main skill

Installation details, setup steps, and longer supporting material should not clutter the main skill.

These should be stored as **references** instead.

Use references for things like:

- installation
- setup
- migration notes
- larger examples
- external docs
- supporting snippets that are useful but not core to the quick package understanding

## Rules inherited from ai-usage-info

Most libraries in the organisation may still provide `.ai-usage-info.md` files.
These can still be useful as source material, but package-local skills are now preferred.

### Observe existing package guidance

When working on a package:

- look for package-local skills first
- also check for `.ai-usage-info.md` files when they exist
- use them as input to understand how the package should be used
- prefer package-local skill content as the maintained source of truth going forward

### Report missing or bad package guidance

Always report unclear, missing, or outdated package guidance.

If a package is missing a proper package-local skill, suggest creating one.

### Do not put too much into one file

Do not turn one package skill into a large documentation dump.
Split package knowledge into focused skills and references when needed.

## Recommended package-skill structure

```text
packages/<package>/
  package.json
  vite.config.ts
  skills/
    <packagename>-usage/
      SKILL.md
      references/
        installation.md
        setup.md
        examples.md
```

Make sure `skills/` is shipped with the package. The directory must be included in the relevant Vite/Nx asset configuration and in `package.json` publishing metadata if such filtering is used.

## Writing guidelines

- Keep the main `SKILL.md` short and avoid repetitive rule variants.
- Prefer one concise general rule over multiple near-duplicate rules for individual versions, tools, or cases.
- Put the package name and purpose already into the frontmatter description.
- Use concrete examples.
- Prefer package-specific instructions over generic framework explanations.
- Move installation and setup into `references/` files.
- Keep references focused and reusable.
- Mention `skills-npm` only briefly in the creator skill; detailed consumption/setup belongs into `link-package-skills`.

## Agent rules

- Prefer package-local skills over central package usage notes when available.
- When creating a new package skill, use the `<packagename>-<what>` naming scheme.
- Create new package skills under `packages/<package>/skills/<skillname>/` by default.
- The `skills/` directory must live next to `package.json`.
- Make sure `skills/` is included in Vite/Nx assets and in `package.json` publish metadata when needed.
- Treat `packages/<package>/.agents/skills/` as legacy unless the user explicitly wants to keep or migrate it.
- Make the main package skill concise and descriptive.
- Combine similar guidance into one sentence instead of adding separate rules for every version, tool, or case.
- Put installation and setup into references, not into the main `SKILL.md`.
- Use existing `.ai-usage-info.md` content as source material when useful, but treat package-local skills as the successor model.
