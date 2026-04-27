# Changelog

## v1.2.0

### ⚠️ Breaking — fixed swapped hook entries

In v1.1.0 and earlier, the `entry:` lines in `.pre-commit-hooks.yaml` were
swapped between `fvm-analyze` and `fvm-format`. Hooks silently did the
opposite of what their `id:` and `name:` advertised:

- `id: fvm-analyze` actually ran `fvm dart format`.
- `id: fvm-format`  actually ran `fvm flutter analyze`.

This release corrects the manifest so each `id:` runs the script it claims.
**Action required**: if your `.pre-commit-config.yaml` was relying on the
old (broken) behavior, swap the IDs to keep the same pipeline.

### Improvements

- Scripts use `set -eu` and quote `"$@"` for safer arg handling (paths with
  spaces and unset-variable surprises are now handled correctly).
- README documents the `args:` pattern, including `--no-fatal-infos` for
  migration-mode lint pipelines
  ([flutter/flutter#20855](https://github.com/flutter/flutter/issues/20855))
  and `--set-exit-if-changed` for strict-CI formatting.

## v1.1.0

- Fix `check-fvm` for FVM >= 3.x.x (the `fvm doctor` output changed).

## v1.0.0

- Initial release: `check-fvm`, `fvm-format`, `fvm-analyze` hooks.
