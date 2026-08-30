# Publish troubleshooting

Resolve the exact workflow run, failed job, package, version, and registry.
Inspect the first actionable publish error rather than treating all `Not Found`
or authentication-looking messages as the same cause.

Check, in order supported by the evidence:

1. the version does not already exist;
2. the built package name, version, access, and registry are correct;
3. the workflow has the permissions required for OIDC/trusted publishing;
4. the trusted-publisher repository and workflow filename match;
5. Node and npm versions meet current requirements;
6. package ownership and repository metadata are correct;
7. the release tag pattern selected the intended package.

Use `npm login` only when an authenticated npm CLI operation is actually needed;
trusted CI publishing should not be repaired by adding a long-lived registry
token. After a configuration correction, verify the trust entry and the next
authorized workflow run.
