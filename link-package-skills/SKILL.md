---
name: link-package-skills
description: Use this skill when linking or consuming package-provided skills from installed npm libraries via skills-npm.
---

# Link Package Skills

Use this skill when the user wants to consume skills that are shipped inside npm packages.

The recommended tool for this is:

- `skills-npm`

## What skills-npm does

`skills-npm` scans installed packages for skills and creates symlinks into the selected agent skill directories.

The generated symlink names follow this pattern:

```text
npm-<package-name>-<skill-name>
```

## Install

```bash
npm install --save-dev skills-npm
npx skills-npm setup
```

## What setup does

`npx skills-npm setup` does three things:

1. it adds the `prepare` hook to `package.json`
2. it performs the first scan
3. it adds the generated skill links to `.gitignore`

After that, sync runs again automatically on `npm install` or `npm ci` through the root `prepare` hook:

```json
{
  "scripts": {
    "prepare": "skills-npm --yes"
  }
}
```

Use `--yes` in lifecycle hooks so `npm install`/`npm ci` never opens an interactive confirmation prompt.

If the root project already has a `prepare` script, append `skills-npm --yes` there instead of replacing existing commands:

```json
{
  "scripts": {
    "prepare": "husky && skills-npm --yes"
  }
}
```

When workspace-linked packages should also be scanned, make the source explicit in the hook and force a fresh scan so a stale cache from a narrower source cannot clean up valid links:

```json
{
  "scripts": {
    "prepare": "husky && skills-npm --source node_modules --yes --force"
  }
}
```

Do not add `postinstall` or `prepare` hooks to published library packages just to link skills. Packages should only ship their `skills/` directory; the consuming/root project decides centrally when and which package skills are linked.

In monorepos, configure `skills-npm` exclusively in the private root package config (`package.json` with `"private": true`). Do not add `skills-npm`, `skills-npm.config.ts`, or skill-linking lifecycle hooks to individual workspace packages.

## Package skill source layout

When creating package skills for npm consumption, prefer this package-internal layout:

```text
packages/<package>/skills/<skillname>/
```

Important:

- the `skills/` directory must live on the same level as `package.json`
- do not place package skills under `src/`
- the `skills/` directory must be included in the package build/publish setup so `skills-npm` can discover it after installation
- make sure it is considered both in Vite/Nx asset handling and in the published package metadata from `package.json`

Example:

```text
packages/form/skills/form-usage/SKILL.md
```

This is the preferred newer format.

Older package-local skill locations like:

```text
packages/<package>/.agents/skills/
```

should only be migrated on explicit user request.

## Configuring selected packages and skills

Use `skills-npm.config.ts` in the root project to choose which packages and skills should be linked:

```ts
import { defineConfig } from 'skills-npm'

export default defineConfig({
  source: 'package.json',
  agents: ['universal'],
  include: ['@leuffen/*', '@nextrap/*', '@trunkjs/*'],
  gitignore: true,
  yes: true,
  force: true,
})
```

`agents: ['universal']` links to `.agents/skills`, which is the shared project skill directory used by several agents. `skills-npm` currently does not provide a native option to choose an arbitrary target subdirectory such as `.agents/skills/npm/` or to change the `npm-` link prefix.

More selective examples:

```ts
import { defineConfig } from 'skills-npm'

export default defineConfig({
  source: 'package.json',
  agents: ['universal'],
  yes: true,

  include: [
    '@vueuse/skills',
    '@company/*',
    {
      package: '@slidev/cli',
      skills: ['presenter-mode'],
    },
  ],

  exclude: [
    '@company/legacy-tools',
    {
      package: '@company/*',
      skills: ['internal-deployment'],
    },
  ],
})
```

## Real package examples mentioned in the README

The official README already mentions real npm packages with built-in skills, including:

- `@slidev/cli`
- `@vueuse/skills`
- `@vitejs/devtools-kit`
- `eslint-vitest-rule-tester`

## Agent rules

- Prefer `skills-npm` when the goal is to consume skills from installed npm packages.
- Use `npm install --save-dev skills-npm` and `npx skills-npm setup` for the initial setup.
- Configure and run `skills-npm` in the root project, not in individual published packages.
- In monorepos, only configure `skills-npm` in the private root package config (`"private": true`); never in workspace package configs.
- Use the root `prepare` script for automatic sync, for example `"prepare": "skills-npm --yes"` or `"prepare": "husky && skills-npm --yes"` when an existing prepare command must be preserved.
- Always include `--yes` in install lifecycle hooks so `npm install`/`npm ci` does not ask interactive questions.
- When using `--source node_modules` in lifecycle hooks to include workspace-linked package skills, also include `--force` so a stale cache from a previous narrower scan cannot remove valid links.
- Do not add package-level `postinstall` or `prepare` hooks that link skills for consumers.
- Explain that the setup modifies root `package.json`, runs the first scan, and updates `.gitignore`.
- Mention that generated links are symlinks named `npm-<package-name>-<skill-name>`.
- Prefer the package-internal `skills/<skillname>/` layout for newly created package skills.
- The `skills/` directory must live next to `package.json`.
- Make sure `skills/` is included in Vite/Nx assets and in `package.json` publish metadata so installed packages still expose the skills.
- Treat `.agents/skills` inside packages as older layout and migrate it only on explicit user request.
