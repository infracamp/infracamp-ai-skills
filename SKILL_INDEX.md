<!-- Automatically generated and maintained from the frontmatter of the SKILL.md files below. -->

| Skill name | Description |
| --- | --- |
| `ai-usage-info` | Use this skill to detect the usage of libraries that should be used within the project. Reads or writes .ai-usage-info.md files in node_modules and vendor folders. |
| `architecture-decisions` | Use only when developing inside a concrete repository or package and changing complex components, package structure, data flow, DOM/layout behavior, or other foundational design. Search repository and relevant package roots for ARCHITECTURE.md next to language-independent project manifests; read every applicable file and treat it as binding. Do not use for consuming or integrating a published library. Editing ARCHITECTURE.md itself requires explicit developer approval. |
| `basic-coding` | Always use this skill whenever you have to code php,ts,scss,html,css,js or any other programming language. |
| `browser-screenshot-with-puppeteer` | Öffnet die aktuelle Website in einem Browser mit Puppeteer und erstellt Screenshots. Verwende diesen Skill, wenn du den aktuellen Stand einer Website visuell erfassen oder dokumentieren willst. |
| `codeing-typescript-lib` | Use this skill when creating or extending TypeScript libraries. |
| `codex-chatgpt-howtos` | Use proven operational how-tos when Codex runs inside ChatGPT Work with a restricted filesystem, GitHub connector, or connector-backed repository workflow. Use for releases, pushes, tags, and recurring runtime-specific failures; do not apply to ordinary local Codex CLI sessions. |
| `create-package-skills` | Use this skill when defining or maintaining package-local skills for libraries, components, or packages in this repository. |
| `explain-skill` | Use only if asked why you did something and how to optimize the skills. |
| `link-package-skills` | Use this skill when linking or consuming package-provided skills from installed npm libraries via skills-npm. |
| `nx-monorepo-setup` | Use this skill when creating, configuring, or maintaining Nx monorepos, root Nx workspace config, or new Nx library packages. |
| `nx-release-and-npm-config` | Use this skill when the user wants to prepare Nx releases, publish packages to npm, or configure npm trusted publishing for packages in a monorepo. |
| `project-context-cache` | Load this skill first at the start of repository work; it defines AGENT_CONTEXT.md as an operational onboarding cache for stable repository facts that are expensive to rediscover. Do not store architecture decisions or binding design contracts here; use the architecture-decisions skill and ARCHITECTURE.md for those. |

Agents without an integrated skill engine can use this index to select a relevant skill without scanning every subdirectory. Agents must update this file whenever a skill name or description below changes.
