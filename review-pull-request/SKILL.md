---
name: review-pull-request
description: Review a pull request or code diff for concrete correctness, regression, security, compatibility, and verification problems. Use when the user asks for code review, PR review, or review findings; do not activate for ordinary implementation work unless review is explicitly part of the request.
---

# Review a pull request

Review the requested diff in the context of applicable repository instructions,
architecture contracts, public APIs, and neighboring implementation patterns.

Prioritize findings that can cause incorrect behavior, regressions, data loss,
security exposure, accessibility failures, or broken compatibility. Check tests
and documentation only where their absence conceals or creates a concrete risk.

For each finding:

- identify the affected file and smallest useful location;
- describe the observable failure or risk;
- explain the conditions under which it occurs;
- suggest a direction for correction without rewriting the entire patch.

Do not report subjective style preferences, speculative edge cases without a
plausible path, or issues outside the changed scope as defects. Put findings in
severity order. If no material findings remain, say so and mention any material
verification limitation.
