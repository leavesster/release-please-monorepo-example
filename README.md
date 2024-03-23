# monorepo-changelog-example

a example that use release-please to auto generate independent changelog in JavaScript mono repo.

## how to use release-please

### prepare release-please config and manifest

add `release-please-config.json` in root.


`release-please-config.json`
```javascript
{
  "packages": {
    // write every package path in packages field
    "packages/a": {
      // component will specify the tag name by release-please.
      // if not set, release-please will use the package name and remove @scope prefix to tag.
      "component": "b"
    },
    "packages/b": {
      "component": "a"
    }
  },
  // it specify where to update version. in node, it will update package.json version field.
  "release-type": "node",
  // to support monorepo, we need to specify the workspace plugin.
  "plugins": ["node-workspace"],
  // schema to autocomplete, not used in release-please.
  "$schema": "https://raw.githubusercontent.com/googleapis/release-please/main/schemas/config.json"
}
```

add `.release-please-manifest.json` by self, not use `release-please bootstrap` command. because it will throw some error for monorepo.
```javascript
{
  // package's path, release-please will update version in this filed and also package.json
  "packages/a": "0.1.0",
  "packages/b": "0.1.0"
}

```

## Reference

- [release-please](https://github.com/googleapis/release-please)
- [release-please-action](https://github.com/google-github-actions/release-please-action)
- [Streamlining Development through Monorepo with Independent Release Cycles](https://devblogs.microsoft.com/ise/streamlining-development-through-monorepo-with-independent-release-cycles)
- [npm/cli](https://github.com/npm/cli)