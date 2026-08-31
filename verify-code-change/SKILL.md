---
name: verify-code-change
description: Verify that a completed code change works through the repository's narrowest meaningful build, test, lint, demo, runtime, or visual checks. Use after implementation or when the user asks to validate a change; do not use as a substitute for implementing or reviewing it.
---

# Verify a code change

Verify the behavior that changed, not merely that the repository still parses.

1. Identify the changed behavior, affected package, and user-visible success
   criteria from the request and diff.
2. Discover existing verification commands from repository instructions,
   manifests, CI workflows, and neighboring packages. Reuse them instead of
   inventing a parallel harness.
3. Run the narrowest checks that exercise the change. Expand only when the
   dependency graph or failure evidence warrants it.
4. For UI changes, exercise the running demo or application and inspect the
   affected states and responsive variants. Use visual evidence when layout or
   styling matters.
5. Distinguish failures caused by the change from missing dependencies,
   environment limitations, and pre-existing failures.
6. Report each check and result. If meaningful verification was impossible,
   state exactly what remains unverified and why.

Do not add tests, fixtures, dependencies, or unrelated fixes unless the user
requested them or they are necessary parts of the implementation scope.
