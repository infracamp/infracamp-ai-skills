---
name: codex-chatgpt-howtos
description: Use proven operational how-tos when Codex runs inside ChatGPT Work with a restricted filesystem, GitHub connector, or connector-backed repository workflow. Use for releases, pushes, tags, and recurring runtime-specific failures; do not apply to ordinary local Codex CLI sessions.
---

# Codex in ChatGPT Work

Use this skill for non-obvious behavior that is specific to Codex inside ChatGPT Work. Repository and package skills remain
the source of truth for the actual project; this skill only adds runtime-specific execution guidance.

## Operating rules

- Treat connector authorization, shell credentials, filesystem permissions, and mutation approval as separate concerns.
- Approval to create or push a pull request does not imply approval to merge it, update the default branch, publish a
  package, or push a release tag.
- Ask for approval only after the exact remote target is known. A commit recreated through a connector has a different SHA
  from the equivalent local commit.
- After a permission or risk rejection, stop that mutation. Do not retry through another endpoint as a workaround.
- Prefer a pull request when the connected GitHub interface cannot reproduce an authenticated Git operation safely.
- Do not store secrets, temporary commit hashes, workspace paths, or one-off incident details in this skill.

## How-to routing

- For a TrunkJS package release, read [references/trunkjs-release.md](references/trunkjs-release.md) completely before
  versioning, pushing, tagging, or publishing.
- For npm trusted-publishing setup or repair, also use `nx-release-and-npm-config`.

## Maintaining these how-tos

Add guidance only after behavior has been observed and the lesson changes a future decision. Record the invariant and the
safe fallback, not a transcript of the failure. Keep project-specific procedures in a focused reference and keep this
entrypoint short.
