---
name: ai-usage-info
description: Use this skill to detect the usage of libraries that should be used within the project.
---

# Basic Coding

Most libraries of the organisation offer a `.ai-usage-info.md` file in root directory of the package within the node_modules or vendor folder.
This file contains information about the usage of the library.


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