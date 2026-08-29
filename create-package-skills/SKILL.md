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

Create at most two or three skills per package. Usually create:

- one usage skill for package consumers
- optionally one setup/integration skill when setup is handled by a different audience
- only when necessary, one additional skill for another clearly distinct audience

Create a separate skill only when its target audience differs. For example, application developers and theme designers
may need separate skills because theming is irrelevant to ordinary application development. A separate concern, large
API, or different workflow alone does not justify another skill. Group all guidance for the same audience in one skill
and use references to split its details.

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

- name the package in the frontmatter description
- list every supported public feature in the frontmatter description using its exact exported class, function, or custom-element name
- identify each feature as a **programmatic API**, **element**, or both
- stay concise
- give package consumers a quick API index

The body of the consumer-facing usage skill should contain only:

- the list of public API methods, classes, functions, and elements
- one short functional description and intended use for each entry
- a direct link for each entry to its detailed reference or repository demo

Use exact identifiers such as `FormDataAccessor`, `createFormDataAccessor()`, or `<nte-form>`. Do not replace them with
generic labels. If one feature has both an element and a programmatic API, name and classify both entrypoints.

Do not place full examples, repeated explanations, installation steps, or detailed API documentation in the main
`SKILL.md`. Put those details in references or demos and link them from the corresponding API entry.

Recommended compact format:

```markdown
---
name: form-usage
description: Use @scope/form: FormDataAccessor (programmatic API), createFormDataAccessor() (programmatic API), and <nte-form> (element).
---

# Form usage

- `FormDataAccessor` — Reads and writes structured form data. See [reference](references/form-data-accessor.md).
- `createFormDataAccessor()` — Creates an accessor for programmatic form handling. See [demo](../../demo/form-data-accessor.ts).
- `<nte-form>` — Provides declarative form behavior. See [reference](references/nte-form.md).
```

## What should not bloat the main skill

Installation details, setup steps, and longer supporting material should not clutter the main skill.

These should be stored as **references** instead.

Use references for things like:

- installation
- setup
- migration notes
- API details and edge cases
- examples for individual classes, functions, methods, and elements
- external docs
- supporting snippets that are useful but not core to the quick package understanding

Prefer an existing repository demo when it fully documents the API. Otherwise add a focused reference. Every public API
entry listed in the usage skill must link to one of these sources. Keep information in one place and avoid repeating the
same explanation in the main skill, references, and demos.

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
        form-data-accessor.md
        nte-form.md
    form-setup/
      SKILL.md
      references/
        installation.md
        integration.md
```

Make sure `skills/` is shipped with the package. The directory must be included in the relevant Vite/Nx asset configuration and in `package.json` publishing metadata if such filtering is used.

## Writing guidelines

- Keep the main `SKILL.md` short and avoid repetitive rule variants.
- Limit each package to two or three skills and create more than one only for distinct target audiences.
- Combine all related APIs for the same audience in one skill; move its detailed modes or workflows into references.
- Prefer one concise general rule over multiple near-duplicate rules for individual APIs, versions, tools, or cases.
- Put the package name, every public feature with its exact identifier, and its programmatic/element classification into the frontmatter description.
- Keep the consumer skill body to an API index with a short purpose and a reference or demo link for every entry.
- Prefer package-specific instructions over generic framework explanations.
- Move installation, setup, detailed explanations, and examples into `references/` files or repository demos.
- Keep references focused and reusable.
- Mention `skills-npm` only briefly in the creator skill; detailed consumption/setup belongs into `link-package-skills`.

## Agent rules

- Prefer package-local skills over central package usage notes when available.
- When creating a new package skill, use the `<packagename>-<what>` naming scheme.
- Create no more than two or three skills per package and create a separate skill only for a distinct target audience, such as application developers, theme designers, or setup maintainers.
- Create new package skills under `packages/<package>/skills/<skillname>/` by default.
- The `skills/` directory must live next to `package.json`.
- Make sure `skills/` is included in Vite/Nx assets and in `package.json` publish metadata when needed.
- Treat `packages/<package>/.agents/skills/` as legacy unless the user explicitly wants to keep or migrate it.
- Make the main package skill concise: list the exact public API identifiers, their short purpose, and their reference/demo links.
- In the frontmatter description, list all supported functionality by exact class, function, or element name and mark each as programmatic API, element, or both.
- Combine similar guidance into one sentence instead of adding separate rules for every version, tool, or case.
- Put installation, setup, examples, and API details into references or demos, not into the main `SKILL.md`.
- Use existing `.ai-usage-info.md` content as source material when useful, but treat package-local skills as the successor model.
