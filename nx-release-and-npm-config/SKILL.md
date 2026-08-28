---
name: nx-release-and-npm-config
description: Use this skill when the user wants to prepare Nx releases, publish packages to npm, or configure npm trusted publishing for packages in a monorepo.
---

# Nx Release and npm Config

Use this skill when the task is about:

- building package releases with `nx release`
- preparing version bumps and git tags
- publishing packages to npm
- first-time npm package release setup
- configuring npm trusted publishing for GitHub Actions

## Nx release flow

If the user asks for a release via Nx and does not specify the release type, default to a **patch release**.

Preferred commands:

```bash
nx release patch --skip-publish
```

For selected packages:

```bash
nx release patch --skip-publish -p <package>
nx release patch --skip-publish -p <package-a>,<package-b>
```

If the user explicitly asks for something else, use that instead, e.g.:

```bash
nx release minor --skip-publish -p <package>
nx release major --skip-publish -p <package>
nx release prerelease --preid rc --skip-publish -p <package>
```

## What `nx release` usually does

Typical flow:

1. runs the configured pre-version checks/builds
2. updates package versions
3. updates dependent package versions if configured
4. updates changelogs
5. updates lockfiles if needed
6. creates a git commit
7. creates git tags
8. skips publishing when `--skip-publish` is used

## After a successful Nx release

Always tell the user to run:

```bash
git push --follow-tags origin main
```

Do not forget this. Without the tags, the publish workflow will usually not run.

## Important release notes

- If the pre-version command fails, the release is not complete.
- Check whether Nx created a commit or tags before retrying.
- In monorepos, prefer targeted releases with `-p <package>` if the user only wants specific packages.
- If a package build is intentionally disabled or replaced, note that clearly before releasing.

## First-time npm publish for a new package

When a package has never been published to npm before, the trusted publishing setup cannot be created in the same step.

Required process:

1. run npm authentication in the container
2. finish login in the browser
3. publish the package once manually
4. configure trusted publishing afterwards

### Step 1: authenticate in the container

```bash
npm auth <username>
```

This opens the login flow. Complete the browser login.

### Step 2: publish the package manually

Publish from the actual package directory that should go to npm.
In Nx library setups this is often the built output directory, for example:

```bash
cd dist/packages/<package>
npm publish --access public
```

If the package is not published from `dist`, use the correct package root explicitly.
Always verify the directory before publishing.

Important:

- this manual `npm publish` should only be done **once** for the initial package publication
- after the package exists on npm and trusted publishing is configured, releases should go through `nx release` and the GitHub Actions workflow
- do not keep publishing regular releases manually from the package directory after the initial setup

## Trusted publishing requirements

Trusted publishing requires:

- `npm >= 11.15.0`
- the package must already exist on npm
- GitHub Actions workflow-based publishing

Important limitations:

- every package must have been published at least once already
- the first manual `npm publish` cannot create the trust configuration at the same time
- `npm trust` does **not** automatically configure workspaces in bulk
- you must iterate over package names yourself
- a monorepo subdirectory is **not** the trusted publishing identity
- the relevant identity is the **repository + workflow file**
- in this repository, check the actual workflow under `.github/workflows/publish.yml`

## Configure npm trusted publishing

Example:

```bash
packages=(
  "@meine-org/core"
  "@meine-org/react"
  "@meine-org/cli"
)

for package in "${packages[@]}"; do
  npm trust github "$package" \
    --repo meine-org/mein-monorepo \
    --file <workflow-file>.yml \
    --allow-publish \
    --yes

  sleep 2
done
```

Notes:

- the first call will require 2FA confirmation
- npm provides a roughly five-minute 2FA window
- according to the documentation, around 80 packages can usually be configured within that window

## Repository metadata in package.json

If the user means package paths inside the monorepo, store them as metadata in `package.json`:

```json
{
  "repository": {
    "type": "git",
    "url": "git+https://github.com/meine-org/mein-monorepo.git",
    "directory": "packages/core"
  }
}
```

This can also be set with npm workspaces:

```bash
npm pkg set repository.directory=packages/core --workspace @meine-org/core
```

Important:

- `repository.directory` only describes where the package lives in the monorepo
- it is **not** the trusted publishing selector
- `npm trust` still needs package name, repository, and workflow file

Example:

```bash
npm trust github @meine-org/core \
  --repo meine-org/mein-monorepo \
  --file <workflow-file>.yml \
  --allow-publish
```

## Agent rules

- Prefer `nx release <bump> --skip-publish` for version preparation.
- Default to **patch** when the user does not specify the bump type.
- After a successful release, always ask the user to run:

```bash
git push --follow-tags origin main
```

- For first-time npm releases, do not claim trusted publishing is already active unless the package was already published and `npm trust` was configured successfully.
- When configuring trust in a monorepo, iterate over package names explicitly.
- Verify the workflow filename and repository slug carefully before running `npm trust github`.
