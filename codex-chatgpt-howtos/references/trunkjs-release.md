# TrunkJS release handoff from Codex in ChatGPT Work

Codex does not create TrunkJS package versions, release commits, tags, or npm publications. When a release is needed, ask
the developer to create and publish it from an authenticated development environment. Codex may inspect configuration,
prepare the implementation PR, provide the exact commands, and verify the result afterwards.

## Codex responsibilities before handoff

1. Read `nx-release-and-npm-config/SKILL.md`, the repository `nx.json`, `.github/workflows/publish.yml`, and the target
   package's `package.json`.
2. Confirm the implementation PR is merged and its required CI is green.
3. Determine the package's Nx project name, current version, intended bump, and release-tag pattern.
4. Check for known configuration problems that the developer should expect.
5. Give the developer the release commands without executing commands that version, commit, tag, push, or publish.

Use a patch bump unless the developer requested another release type. For `@trunkjs/browser-utils`, the Nx project and
tag prefix are `browser-utils`.

## Commands for the developer

Ask the developer to run the following from an authenticated, clean checkout of TrunkJS `main`:

```bash
npm ci
npm --version
npx nx release patch --skip-publish -p browser-utils
git push --follow-tags origin main
```

TrunkJS currently installs npm `11.15.0` in `.github/workflows/publish.yml`. The developer should use the same version
before allowing npm to update `package-lock.json`.

The generated release tag for this package is:

```text
browser-utils@<version>
```

Pushing that tag triggers the Publish workflow; `--skip-publish` only prevents a local npm publication.

## Checks the developer should make before pushing

Ask the developer to inspect the release once after `nx release`:

- the package and lockfile contain the requested version;
- the lockfile contains only intentional changes;
- the changelog describes the main feature as well as fixes;
- an `Unreleased` entry was not left below the newly generated version; and
- the annotated tag points to the final release commit.

An npm version older than the workflow version can remove `libc` metadata from optional packages while updating only a
workspace version. Broad lockfile normalization is not part of a package release and should not be pushed.

Nx may also try to resolve contributor email addresses through `ungh.cc` while rendering changelogs. If this is not
desired, the repository release configuration should set `applyUsernameToAuthors: false` before the developer releases.
Do not work around this by sending contributor data through another service.

## Known ChatGPT Work limitations

These explain why Codex must hand the release off instead of attempting it inside ChatGPT Work:

- the Nx daemon can fail to create its Unix socket with `EPERM`;
- isolated Nx plugin workers can exit before their connection is established;
- repository-wide pre-version builds can include unrelated Sass projects whose embedded compiler cannot run in the
  sandbox;
- the root `@nextrap/source` build can receive an unsupported `--outputPath` option from current target defaults;
- GitHub connector authorization is not available to `git` or `gh` in the shell; and
- the connector may not expose creation of Git tags even when it can create commits and update branches.

Do not respond to these limitations by narrowing the pre-version command, reconstructing release commits through GitHub
Git-data actions, moving `main`, or creating tags through alternate refs. Report the relevant limitation and ask the
developer to perform the normal release.

## Verification after developer publication

After the developer confirms that the version and tag were pushed, Codex should:

1. verify the tag exists;
2. wait for `.github/workflows/publish.yml` to succeed;
3. verify `npm view @trunkjs/browser-utils version` returns the new version;
4. update the downstream dependency and lockfile only after npm serves that version;
5. rerun downstream CI; and
6. merge the downstream PR only when it is green and separately authorized.

For npm authentication, trusted-publishing failures, or a first publication, follow `nx-release-and-npm-config` and keep
the actual version creation and publication with the developer.
