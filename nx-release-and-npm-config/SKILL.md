---
name: nx-release-and-npm-config
description: Prepare and troubleshoot Nx package releases and npm trusted publishing in monorepos. Use for version preparation, release tags, first npm publication, publish workflows, or npm trust configuration; do not use for ordinary Nx workspace setup.
compatibility: Requires an Nx workspace and, for registry operations, a current Node/npm runtime plus npm and GitHub access.
---

# Nx release and npm publishing

First identify which mode applies:

- For a normal release after publishing is configured, read
  [references/normal-release.md](references/normal-release.md).
- If the package does not yet exist on npm, read
  [references/first-publication.md](references/first-publication.md).
- To configure or repair npm trusted publishing, read
  [references/trusted-publishing.md](references/trusted-publishing.md).
- When a publish workflow fails, read
  [references/publish-troubleshooting.md](references/publish-troubleshooting.md).

Resolve the exact packages, Nx release relationship, registry, repository slug,
workflow filename, and package metadata before proposing commands. Prefer
targeted releases when only selected packages are requested.

## Authorization boundary

Version creation, release commits, tags, and publication are externally
meaningful mutations. Follow the active environment's authorization policy and
the user's explicit request. Never infer permission to merge, publish, or move
the default branch merely from permission to prepare a pull request.

Make it explicit which commands require the developer's authenticated session
and which read-only verification the agent performed. Never expose credentials
or persist login state in repository files.
