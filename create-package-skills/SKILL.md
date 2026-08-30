---
name: create-package-skills
description: Author or maintain skills shipped inside an npm library or component package. Use when documenting a package's public APIs for agents, migrating legacy .ai-usage-info.md guidance, or ensuring package skills are included in published artifacts; do not use merely to consume installed skills.
---

# Package skill authoring

Keep package knowledge next to the package that owns it:

```text
packages/<package>/
  package.json
  skills/<skill-name>/
    SKILL.md
    references/
```

The `skills/` directory lives beside `package.json`, not under `src/`. Include it
in build assets and npm `files` when the package filters published content.

## Scope and audience

Create one concise usage skill for package consumers. Add a separate skill only
when another audience has a materially different intent, such as setup
maintainers or theme authors. Prefer two or fewer; use references to separate
detailed APIs and modes.

The description must name the package and the exact public identifiers that
should cause activation. Classify custom elements and programmatic APIs when the
distinction matters. The body should be a compact API index with one-line
purposes and links to focused references or maintained repository demos.

Do not duplicate complete examples, installation steps, and API documentation
between `SKILL.md`, references, and demos. Prefer the maintained source that best
exercises the API.

## Existing and generated skills

- Treat package `.agents/skills/` as a legacy location and migrate it only when
  requested.
- Use `.ai-usage-info.md` as migration input, not as the maintained successor.
- Never edit generated `.agents/skills/npm-*` links. Resolve the link and edit
  its workspace source; if it points into `node_modules`, change the source
  package repository instead.

Use `link-package-skills` when configuring a consumer to discover the published
skills.
