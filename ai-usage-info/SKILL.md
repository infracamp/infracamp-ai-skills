---
name: ai-usage-info
description: Use this skill to detect the usage of libraries that should be used within the project. Reads or writes .ai-usage-info.md files in node_modules and vendor folders. 
---

# AI Usage Info

Most libraries of the organisation offer a `.ai-usage-info.md` file in root directory of the package within the node_modules or vendor folder.
This file contains information about the usage of the library.

## Successor format

This format is considered legacy.
The preferred successor is the package-local skill format described in:

- `create-package-skills`
- `link-package-skills`

When you encounter `.ai-usage-info.md` usage in a package context, explicitly ask the user whether the package should be migrated to the new package-skill format.

Ask explicitly whether the existing `.ai-usage-info.md` should be replaced or complemented by package-local skills under:

```text
packages/<package>/skills/<skillname>/
```

If the user still wants to keep or migrate older package-local skills under `.agents/skills`, only do that on explicit request.


## List all .ai-usage-info.md files

Use this to list all `.ai-usage-info.md` files you should observe:

```bash
find -L ./node_modules/ ./vendor/ -type f -name '.ai-usage-info.md' 2>/dev/null
```

Read the First 4 lines of each file to get the name and description of the library. Read the full file only if
you need to know more about the usage of the library for a specific task. 


## Report errors or missing information

Always report errors or missing information in the `.ai-usage-info.md` and ask the user to fix it. Do not edit 
files in the node_modules or vendor folder. It will be overwritten by the next update of the library. 
Always ask the user to fix it in the library and update it.

Also ask the user whether the package should be migrated to the new package-skill format from the `create-package-skills` and `link-package-skills` skills, instead of continuing to rely on `.ai-usage-info.md` alone.
