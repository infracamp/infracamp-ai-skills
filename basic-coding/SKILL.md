---
name: basic-coding
description: Always use this skill whenever you have to code php,ts,scss,html,css,js or any other programming language.
---

# Basic Coding

This is the fundamental skill for coding.

## Core principles

- Prefer simple, readable and maintainable solutions.
- Do not rebuild or refactor large parts unless the user explicitly wants that.
- Work incrementally instead of doing broad rewrites.
- Keep diffs small and understandable.
- Adapt existing solutions before introducing new abstractions or architectures.
- Avoid clever solutions when a straightforward one is sufficient.
- Reuse existing patterns, utilities, APIs, and file structures whenever possible.
- Ask early if requirements are ambiguous or if multiple valid implementation directions exist.
- Stop early and ask before continuing when follow-up work goes beyond the original request.

## When to ask first

Ask the user before proceeding when:

- requirements are ambiguous
- a refactoring would go beyond the requested change
- existing structures, APIs, or file formats would need to change
- additional follow-up work is obvious but not explicitly requested
- both a minimal fix and a larger cleanup are possible
- a change would affect more than 3 files or would be a larger structural change

## Basic rules

- Keep it short and simple
- Ask if unsure or big changes are needed
- Prevent excessive mapping of key/property/action/etc-names from one entity to another (Like mapping form-names to database to helper objects). Try to unify names across objects, frontend, backend, database, etc. Aks the user if you are allowed to unify the names across the project
- Prevent universal tool-methods in the business logic. If you need helper Methods that are not part of the specific task,
  aks the user to add them to a library or alternative to create a tool class / file that can be used across the project.
- Aks the user if you want to install additional packages or libraries. Do not install them without asking the user!
- When creating or editing HTML, prefer existing utility classes from the project (e.g. bootstrap-like classes such as `d-flex`, `flex-*`, `gap-*`, `m-*`, `p-*`, `text-*`, `w-*`, etc.) instead of creating new custom classes.
- For spacing, prefer existing margin/padding utility classes (`m-*`, `mt-*`, `mb-*`, `p-*`, etc.) even if the spacing is not a 100% exact visual match.
- For responsive utilities, use the project's trunkjs/responsive notation instead of bootstrap breakpoint notation. Example: use `xl:col-5` and `-xl:col-12` rather than `col-xl-*`, `col-lg-*`, `col-md-*`, etc.
- Meaning of the responsive prefixes in general: `xl:<class>` means that `<class>` applies from breakpoint `xl` and up. `-xl:<class>` means that `<class>` applies below `xl`.
- Bootstrap breakpoint classes like `col-md-*`, `col-lg-*`, `col-xl-*`, `d-md-*`, `d-lg-*` should be considered replaced by the trunkjs/responsive syntax.
- Only add custom classes or `<style>` blocks in exceptional cases, e.g. when nested/sub-elements must be targeted, project utilities are not sufficient, or reusable component styling is required.
- If a `<style>` block defines custom CSS variables, declare those variables together at the top of the style block or at the top-level selector first, before the other rules that use them.
- Wenn Styles für ein wiederverwendbares Beispiel oder eine Variante erstellt werden, bevorzugt ein SCSS-Mixin anlegen und dieses über eine semantische Klasse einbinden, statt Styles direkt lose auf die Klasse zu schreiben.
- Bei Folgefragen zu bereits bearbeiteten Dateien die betroffenen Dateien erneut einlesen, bevor Änderungen vorgeschlagen oder umgesetzt werden. Der User kann zwischenzeitlich selbst Änderungen gemacht haben.
- Wenn CSS-Varianten über Klassen aktiviert werden, die Klasse sprechend benennen und alle dazugehörigen Styles zusammenhalten.
- Ein Element sollte immer nur eine `style-*` Klasse gesetzt haben.
- Für Demo-Styles keine unnötigen globalen Selektoren verwenden; möglichst am Demo-Root-Element oder an der konkreten Komponentenklasse scopen.\n- Wenn Markdown Kramdown-Blockattribute wie `{: layout="..."}` verwendet, muss die Attributzeile ohne Leerzeile direkt auf den zugehörigen Block folgen. Das gilt für horizontale Linien (`---`), Tabellen, Absätze und alle anderen Blöcke, zum Beispiel `---` unmittelbar gefolgt von `{: layout="..."}`.



## Command discipline

- Avoid repeated state checks like `git status`, `git log`, `git tag`, `git diff`, `git remote`, or package-manager info commands.
- Verify only at clear boundaries: before risky operations, after state-changing commands, or before the final response if needed.
- Reuse already observed state and `AGENT_CONTEXT.md`; re-check only after relevant changes, failures, ambiguity, explicit user request, or to avoid destructive actions.
- Bundle needed checks into one compact command instead of several separate calls.
- Wenn ein vorhandener Package-Import oder ein erwarteter Dependency-Link nicht aufgelöst wird, weise zuerst darauf hin, dass vermutlich `npm install` vergessen wurde, und frage, ob es bereits ausgeführt wurde. Biete nicht an, das Problem durch direktes/manuelles Ändern der Lockfile zu beheben; `npm install` auszuführen ist erlaubt, wenn es passend ist.
- Ermittle Paketversionen mit gezielten Befehlen. Öffne oder lies Lockfiles niemals vollständig, sofern keine umfassende Lockfile-Analyse verlangt wird. Bevorzuge `npm pkg get`, `npm ls`, `jq` oder eine kurze Node-Abfrage. Verwende `rg` nur zur Lokalisierung relevanter Einträge und begrenze ausgegebene Zeilen.

## Approach to fulfill a task

- Think about how many files need to be changed to fulfill the task. If it is more than 3 or it is a big change 
  to a single file, provide the user with a short plan and ask if you are allowed to do it.
- Scan the project for existing files. Exclude the node_modules and vendor and workspaces folders.
- Check for existing patterns, helpers, APIs, and structures before introducing something new.
- Find inconsistencies or unclear within the prompt and ask the user for clarification if found.
- Prefer the smallest fitting change over a broad rewrite.
- Perform the job.
- Give a short summary of what you did and what files you changed.

## CSS / SCSS

- We use mobile-first approach. D.h. modifier-classen gelten erst mal für alle Breakpoints. Sollten variationen für breakpoints exisiteren, werden diese für desktop und tablet angelegt z.B. `reverse` und `reverse-desktop` oder `reverse-desktop`.

## General Do and Dont`s

### Do`s

- If temporary files are needed, use the /tmp folder.
- If you need to install additional packages, ask the user to do it.
- Correct typos in prompts. (e.g. asked to edit a file or edit a class, use the correct spelling of the class or file name.
- Reuse existing markup patterns and utility classes before introducing new CSS.
- Keep inline or local CSS minimal and only use it where utilities cannot express the requirement.


### Dont`s

- Do not modify stuff in `vendor` or `node_modules` folders or files in `workspaces`. If you need changes to be made here, ask the user to do it.
- Do not excessive scanning or opening of files. 
- Do not excessive programming code snippets to perform a task. Try to use bash or the existing coding tools
- Do not import from "workspaces" or "node_modules" folders directly. Always use the package name to import from. (e.g. `import { MyComponent } from '@my-package/my-component'` instead of `import { MyComponent } from 'workspaces/my-package/src/MyComponent'`). If you find relative imports of packages, ask the user if you should fix them. 


