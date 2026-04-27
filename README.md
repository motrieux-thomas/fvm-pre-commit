# fvm-pre-commit

[Pre-commit](https://pre-commit.com/) hooks that wrap common Flutter / Dart
CLI commands through [FVM](https://fvm.app/), so every contributor uses the
project-pinned Flutter SDK.

## Hooks

| `id`         | Runs                       | Purpose                                                    |
| ------------ | -------------------------- | ---------------------------------------------------------- |
| `check-fvm`  | `fvm doctor`               | Fails fast if FVM is not installed / not configured.       |
| `fvm-format` | `fvm dart format`          | Formats staged Dart files.                                 |
| `fvm-analyze`| `fvm flutter analyze`      | Runs the Dart analyzer over the project.                   |

## Usage

Add the following to your `.pre-commit-config.yaml`:

```yaml
- repo: https://github.com/motrieux-thomas/fvm-pre-commit
  rev: v1.2.0
  hooks:
    - id: check-fvm
    - id: fvm-format
    - id: fvm-analyze
```

## Passing extra flags

Both `fvm-format` and `fvm-analyze` forward any arguments you provide via
pre-commit's `args:` directly to the underlying `fvm dart format` /
`fvm flutter analyze` invocation. Quoting is preserved, so paths with spaces
work correctly.

### `fvm-analyze` — info-visible, non-blocking (lint migration mode)

```yaml
- repo: https://github.com/motrieux-thomas/fvm-pre-commit
  rev: v1.2.0
  hooks:
    - id: fvm-analyze
      args: [--no-fatal-infos, lib/, test/]
```

`--no-fatal-infos` keeps **info**-level diagnostics visible in the output
without failing the hook — handy while migrating a codebase to a stricter
lint set. Despite being the
[documented default](https://dart.dev/tools/dart-analyze), it is often still
required in practice; see
[flutter/flutter#20855](https://github.com/flutter/flutter/issues/20855)
for context.

### `fvm-format` — strict CI mode

```yaml
- repo: https://github.com/motrieux-thomas/fvm-pre-commit
  rev: v1.2.0
  hooks:
    - id: fvm-format
      args: [--set-exit-if-changed]
```

`--set-exit-if-changed` makes the hook exit non-zero if any file would be
rewritten, instead of silently formatting in place. Useful in CI to enforce
"already formatted" as a hard gate.

## License

MIT — see [LICENSE](./LICENSE).
