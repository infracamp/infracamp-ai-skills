# Normal Nx release

Inspect `nx.json` and the affected projects before choosing fixed or independent
release commands. If the user did not specify a SemVer bump and repository rules
do not derive it automatically, use patch as the proposed default.

Typical preparation without registry publication:

```bash
nx release patch --skip-publish --projects=<project>
```

Use the option spelling supported by the installed Nx version. Run a dry run
first when the release configuration or affected set is uncertain.

Confirm that configured pre-version checks succeeded and inspect the resulting
version, changelog, commit, and tags once. Do not repeat the release command
until it is clear whether the first attempt created a commit or tags.

Push the release commit and tags through the repository's established protected
branch workflow. A common direct flow is:

```bash
git push --follow-tags origin <branch>
```

Do not hard-code `main` when the repository uses another release branch.
