# npm shrinkwrap bug testcase

Under certain circumstances, production dependencies will be excluded from npm-shrinkwrap.json.

**Scenario**: 

`top-level-pkg` has a dev dependency on `es6-promise`, and a regular dependency on `server-pkg` (which is installed via a local path, though I've tested the issue with packages from the registry as well).

`server-pkg` has a regular dependency on `es6-promise`.

When running `npm shrinkwrap` in `top-level-pkg`, `es6-promise` gets removed from `npm-shrinkwrap.json`, with the warning below: 

    npm WARN shrinkwrap Excluding devDependency: es6-promise { 'server-pkg': 'file:../server-pkg' }

**Result:**

A `npm-shrinkwrap.json` that cannot install a valid set of deps, as `es6-promise` is missing, but required, by `server-pkg`.
