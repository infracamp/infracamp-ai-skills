# First npm publication

Before treating a package as new, verify its exact `package.json` name and query
the intended registry. Check package access, repository metadata, output
directory, and package contents.

Trusted publishing configuration generally requires the package identity to
exist in the registry. If an initial authenticated publication is required, the
developer completes npm authentication and publishes from the verified package
output directory, for example:

```bash
npm login
cd dist/packages/<package>
npm publish --access public
```

Use `--access public` only for a scoped package intended to be public. Do not
assume `dist/packages/<package>`; inspect the Nx build output first. After the
package exists, configure trusted publishing using
[trusted-publishing.md](trusted-publishing.md) and use the CI release workflow
for later versions.
