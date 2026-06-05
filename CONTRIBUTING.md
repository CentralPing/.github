# Contributing to CentralPing

Thank you for your interest in contributing. This guide covers the process for
all CentralPing repositories (@centralping/ergo, @centralping/ergo-router,
@centralping/json-api-query).

## Design Philosophy

ergo and ergo-router exist to help developers build APIs that follow
established best practices — IETF RFCs, OWASP security guidelines, and
RESTful design principles. The libraries are intentionally opinionated:
every middleware implements a specific standard, the pipeline enforces a
deliberate [Fast Fail](https://centralping.github.io/concepts/fast-fail/)
stage ordering, and defaults are secure by design.

**Guiding principles:**

- **Standards over conventions** — behavior is backed by an IETF RFC,
  W3C specification, or industry standard (OWASP, JSON:API), not
  invented patterns.
- **Fast Fail by design** — requests are rejected at the earliest
  possible stage. Authorization runs before body parsing; negotiation
  runs before authorization. This ordering is not configurable.
- **Secure defaults** — security headers, input bounding, prototype
  pollution prevention, and error redaction are enabled out of the box.
  Weakening a default requires an explicit opt-out.
- **Defense in depth** — multiple independent layers (transport
  security, pipeline ordering, input validation, output sanitization)
  protect against the [OWASP API Security Top 10](https://owasp.org/API-Security/).

**What this means for contributions:**

Contributions that strengthen these principles — improving RFC
compliance, hardening security defaults, adding standard-backed
functionality, or making it easier for consumers to follow best
practices — are especially welcome.

Contributions that would weaken these principles — introducing
non-standard patterns, bypassing the pipeline stage ordering, relaxing
security defaults, or adding conveniences that make it easier to build
non-compliant APIs — will not be accepted regardless of implementation
quality.

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

## Package Namespace

All CentralPing packages are published under the `@centralping` npm scope:

- [`@centralping/ergo`](https://github.com/CentralPing/ergo) — Fast Fail REST
  API middleware toolkit
- [`@centralping/ergo-router`](https://github.com/CentralPing/ergo-router) —
  REST-compliant router
- [`@centralping/json-api-query`](https://github.com/CentralPing/json-api-query)
  — JSON:API query parameter validator

## License

By contributing, you agree that your contributions will be licensed under the
[MIT License](https://opensource.org/licenses/MIT) that covers each project.
