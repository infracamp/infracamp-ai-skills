# Migrating `.ai-usage-info.md`

`.ai-usage-info.md` is the legacy library-guidance format. Treat existing files
as source material, not as files to edit inside `node_modules` or `vendor`.

When migration is requested:

1. Locate relevant files without traversing unrelated dependencies.
2. Extract package-specific APIs, constraints, examples, and failure cases.
3. Create package-local skills next to the package's `package.json` using the
   `create-package-skills` workflow.
4. Ask whether the legacy file should be replaced or temporarily retained when
   that choice affects compatibility with existing consumers.
5. Make the change in the package source repository, never in an installed
   dependency.
