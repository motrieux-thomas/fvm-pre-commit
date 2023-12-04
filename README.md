# fvm-pre-commit
Pre-commit hook to check the fvm installation and running useful hooks (analyze, format...)

This repo contain three pre-commit hooks.

###	 Check fvm

The first hook check if fvm is installed and ready to be used.

```
- repo: https://github.com/motrieux-thomas/fvm-pre-commit
  rev: "main"
  hooks:
    - id: check-fvm
```

### Code analyzing using fvm _(fvm flutter analyze)_

Add the following in your .pre-commit config file.

```
- repo: https://github.com/motrieux-thomas/fvm-pre-commit
  rev: "main"
  hooks:
    - id: fvm-analyze
      args: [lib/*, test/*]
```

### Code formatting using fvm _(fvm dart format)_

Add the following in your .pre-commit config file.

```
- repo: https://github.com/motrieux-thomas/fvm-pre-commit
  rev: "main"
  hooks:
    - id: fvm-format
      args: [lib/*, test/*]
```
