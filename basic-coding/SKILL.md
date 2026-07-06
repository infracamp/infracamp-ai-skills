---
name: basic-coding
description: Always use this skill whenever you have to code php,ts,scss,html,css,js or any other programming language.
---

# Basic Coding

This is the fundamental skill for coding. 


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


## Approach to fulfill a task

- Think about how many files need to be changed to fulfill the task. If it is more than 3 or it is a big change 
  to a single file, Provide the user with a short plan and ask if you are allowed to do it.
- Scan the project for existing files. Exclude the node_modules and vendor and workspaces folders.
- Find inconsistencies or unclear within the prompt and ask the user for clarification if found.
- Perform the Job.
- Give a short summary of what you did and what files you changed.

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
- 


