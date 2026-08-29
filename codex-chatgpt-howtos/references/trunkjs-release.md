# TrunkJS releases from Codex in ChatGPT Work

Use this procedure only when the developer explicitly requests a release or publish. Creating a PR, asking for a PR to be
pushed, or merging an implementation PR is not sufficient release authorization.

## Preconditions

1. Read `nx-release-and-npm-config/SKILL.md`, the repository `nx.json`, `.github/workflows/publish.yml`, and the target
   package's `package.json`.
2. Confirm the implementation PR is merged, its required CI is green, and local `main` matches remote `main`.
3. Use a targeted patch release unless the developer requested another bump.
4. Run `npm ci` from the lockfile. Compare `npm --version` with the version installed by `publish.yml` before allowing npm
   to rewrite the lockfile. TrunkJS currently uses npm `11.15.0` in that workflow.
5. Verify the target package with its tests and build before versioning.

Do not accept unrelated lockfile normalization. In particular, an older npm can remove `libc` metadata from optional
packages while updating only a workspace version. If the lockfile diff contains broad metadata churn, stop and use the
repository's npm version.

## Normal authenticated flow

For `@trunkjs/browser-utils`, the Nx project and release tag prefix are `browser-utils`:

```bash
NX_DAEMON=false NX_ISOLATE_PLUGINS=false \
  ./node_modules/.bin/nx release patch --skip-publish -p browser-utils

git push --follow-tags origin main
```

The environment flags are useful in ChatGPT Work because the Nx daemon can fail to create its Unix socket with `EPERM`,
and isolated plugin workers can exit before their connection is established. They do not change release contents.

Run a dry run first when the release configuration, npm version, or changelog behavior has not already been verified.

## Targeted programmatic fallback

TrunkJS currently configures a repository-wide pre-version build. In ChatGPT Work that can fail for projects unrelated to
the requested package, including Sass builds whose embedded compiler cannot run in the sandbox and the root
`@nextrap/source` target receiving an unsupported `--outputPath` option.

Do not silently bypass a failing target that belongs to the release. For a genuinely targeted release, the official Nx
programmatic API may temporarily override the pre-version command only when:

- the developer explicitly requested that package release;
- the target package's own tests and build passed;
- every skipped failure is demonstrably outside the selected package; and
- the override is kept outside the repository and removed after the run.

The important configuration shape is:

```js
const fs = require('node:fs');
const path = require('node:path');
const { createAPI } = require(
  path.join(repoRoot, 'node_modules/nx/dist/src/command-line/release/release.js'),
);

const config = JSON.parse(fs.readFileSync(path.join(repoRoot, 'nx.json'), 'utf8')).release;
config.version.preVersionCommand =
  'CI=true NX_DAEMON=false NX_ISOLATE_PLUGINS=false ./node_modules/.bin/nx run browser-utils:build';
config.changelog.projectChangelogs = {
  renderOptions: { applyUsernameToAuthors: false },
};

const release = createAPI(config, true);
await release({
  specifier: 'patch',
  projects: ['browser-utils'],
  dryRun: true,
  skipPublish: true,
  verbose: true,
  preid: '',
});
```

Clone the complete `nx.json` release configuration and call `createAPI(config, true)`. Passing only a partial override can
fail because Nx cannot deep-merge an object into the repository's Boolean `projectChangelogs: true` value.

Keep `applyUsernameToAuthors: false`. Otherwise Nx may send contributor email addresses to `ungh.cc` to resolve GitHub
usernames. Author names can remain in the changelog without this external lookup.

After a successful dry run, repeat with `dryRun: false`. Delete the temporary script afterwards.

## Inspect before pushing

Check the release once, after Nx has changed state:

- the package and lockfile contain the requested version;
- only intended lockfile fields changed;
- the changelog describes the main feature as well as fixes;
- an `Unreleased` entry was not left below the newly generated version;
- the release commit and annotated tag point to the same final contents.

If the changelog needs correction, amend the still-local release commit and recreate the still-local tag before pushing.
Never move a published tag without separate explicit authorization.

## GitHub connector and approval boundaries

The GitHub connector session is not automatically available to `git` or `gh` in the shell. After
`could not read Username for 'https://github.com'`, do not keep retrying shell pushes.

Prefer one of these paths:

1. Run the release in an authenticated shell and use `git push --follow-tags origin main`.
2. Push a release branch and merge it through a PR, then create the release tag from an authenticated environment.
3. Use connector Git-data actions only when they expose every required operation, including tag creation, and the exact
   default-branch mutation has been approved.

Connector-created commits have new SHAs even when their trees and messages match local commits. Create the remote commit
first, then request approval for that actual SHA. Approval for a local SHA does not authorize a different connector SHA.
Large lockfiles also make connector-only commit reconstruction fragile; prefer an authenticated git push or release PR.

At the time this was written, the ChatGPT GitHub connector could create blobs, trees, commits, branches, and update branch
refs, but exposed no action for creating a Git tag. Discover current actions instead of assuming this limitation remains.

## Publish and downstream verification

Pushing `browser-utils@<version>` triggers `.github/workflows/publish.yml`. The workflow extracts `browser-utils` from the
tag, runs its tests and build, and publishes through `nx release publish` with npm provenance.

Do not update or merge a downstream repository merely because the tag exists:

1. wait for the Publish workflow to succeed;
2. verify `npm view @trunkjs/browser-utils version` returns the new version;
3. update the downstream dependency and lockfile with the published version;
4. rerun downstream CI; and
5. merge the downstream PR only after it is green and separately authorized.

For npm authentication, trusted-publishing failures, or a first publish, follow `nx-release-and-npm-config` rather than
inventing a ChatGPT-specific workaround.
