---
name: link-package-skills
description: Configure a consuming npm project to discover skills shipped by installed packages through skills-npm. Use for initial setup, include/exclude configuration, workspace-linked skill discovery, or generated-link troubleshooting; do not use to author the package's source skills.
---

# Link package skills

Configure `skills-npm` only in the private root project, never in a published
workspace package.

## Setup

```bash
npm install --save-dev skills-npm
npx skills-npm setup
```

Setup adds the root lifecycle hook, performs the first scan, and ignores
generated links. Preserve an existing `prepare` command and append the
non-interactive sync:

```json
{
  "scripts": {
    "prepare": "husky && skills-npm --yes"
  }
}
```

Use root `skills-npm.config.ts` to limit packages and targets. Prefer the shared
`.agents/skills` target when several agents consume the same repository skills:

```ts
import { defineConfig } from 'skills-npm'

export default defineConfig({
  source: 'package.json',
  agents: ['universal'],
  include: ['@leuffen/*', '@nextrap/*', '@trunkjs/*'],
  gitignore: true,
  yes: true,
})
```

When scanning workspace-linked packages through `node_modules`, use the source
explicitly and force a fresh scan so stale cache state does not remove valid
links:

```json
{
  "scripts": {
    "prepare": "skills-npm --source node_modules --yes --force"
  }
}
```

Generated links are named `npm-<package>-<skill>`. Never edit them directly.
Resolve the symlink and edit the workspace source skill; if it points only into
`node_modules`, report that the source package must be updated.

Use `create-package-skills` for source layout and publishing requirements.
