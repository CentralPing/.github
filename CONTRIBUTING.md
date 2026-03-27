# Contributing to CentralPing

Thank you for your interest in contributing. This guide covers the process for
all CentralPing repositories (ergo, ergo-router, json-api-query).

## Reporting Bugs

Open a [GitHub Issue](https://docs.github.com/en/issues) on the affected
repository. Include:

- Node.js version (`node -v`)
- Package version
- Minimal reproduction (code snippet or repo link)
- Expected vs actual behavior

## Reporting Security Vulnerabilities

**Do not** open a public issue. Follow the process in our
[Security Policy](SECURITY.md).

## Development Setup

All repositories require **Node.js >= 22** and use **npm** for package
management.

```bash
git clone <repo-url>
cd <repo>
npm install
npm test
```

Each repository's README has a **Development** section with the full list of
available scripts.

## Code Style

- **Formatter**: Prettier (`printWidth: 100`, `singleQuote: true`)
- **Linter**: ESLint (code-quality rules only, no formatting)
- **Module system**: Pure ESM (`import`/`export`, no `require`)
- **Documentation**: JSDoc with `@fileoverview`, `@module`, `@param`, `@returns`

Run `npm run format` and `npm run lint` before submitting a PR. The CI pipeline
enforces both.

## Testing

- **Framework**: Node.js built-in `node:test` (no external runner)
- **Coverage**: `c8` with enforced thresholds (branches 80%, functions 100%,
  lines 80%, statements 80%)
- **Philosophy**: Black-box only — test inputs and outputs, never internal
  implementation

Run `npm test` to execute the full suite (lint + format check + tests with
coverage).

## Pull Request Process

1. Fork the repository and create a branch from `main`.
2. Make your changes with tests covering any new behavior.
3. Ensure `npm test` passes locally.
4. Open a pull request against `main`.

All repositories enforce:

- **Signed commits** (GPG or SSH)
- **Required CI checks** (Node.js 22 and 24)
- **Linear history** (squash or rebase merge only, no merge commits)

## License

By contributing, you agree that your contributions will be licensed under the
[MIT License](https://opensource.org/licenses/MIT) that covers each project.
