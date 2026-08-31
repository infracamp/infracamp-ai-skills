# npm trusted publishing

Check current authoritative npm requirements before changing trust. Verify at
least:

- installed Node and npm versions support the required trust commands;
- the authenticated account can maintain the package and has required 2FA;
- the package already exists on the intended registry;
- repository metadata in `package.json` is correct;
- the GitHub repository and workflow filename match the actual publisher.

Inspect current state before replacing it:

```bash
npm view <package> version
npm owner ls <package>
npm trust list <package>
```

Configure the exact workflow identity:

```bash
npm trust github <package> \
  --repo <owner>/<repository> \
  --file <workflow>.yml \
  --allow-publish \
  --yes
```

If an existing trust entry points to the wrong workflow, record its identity,
revoke only that entry, recreate it, and verify the resulting list once. Iterate
explicitly over package names in monorepos; a package directory is metadata, not
the trusted-publisher identity.

Authentication and 2FA prompts must be completed by the developer. Stop rather
than attempting to bypass a failed login, permission denial, or protected
workflow.
