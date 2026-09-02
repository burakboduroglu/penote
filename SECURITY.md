# Security Policy

## Supported versions

Only the latest release is supported. There are no maintenance branches — a fix
ships in the next version rather than as a patch to an older one.

| Version | Status               |
| ------- | -------------------- |
| 2.1.x   | Supported            |
| < 2.1   | Unsupported, upgrade |

## What this project touches

Worth knowing before you report, and before you install:

- **It is a notes library plus a local CLI.** The published package ships Markdown
  notes, `library/cli.js`, and `library/index.html`. There is no remote server
  and no account system.
- **The CLI runs as you.** It lists and opens local files under the package (or
  a clone). It does not escalate privileges and does not shell out beyond what
  Node needs to spawn your editor or open a browser.
- **The Web UI is local.** `penote open --editor` serves static content for
  browsing notes in a browser. Treat it as local-only tooling for as long as
  you leave it running.
- **Runtime dependencies.** The CLI and Web UI use Node.js built-ins only. There
  is no production `node_modules` tree for the tool itself.
- **Distribution.** The npm package is published from GitHub Actions when a
  release is published. Prefer installing tagged releases over ad-hoc copies.

## Reporting a vulnerability

Please do **not** open a public issue for a security problem.

Report it privately in one of these ways:

1. **GitHub Security Advisories** — open a private draft advisory from the
   [Security tab](https://github.com/burakboduroglu/penote/security/advisories/new).
   This is preferred.
2. **Email** — <info@burakboduroglu.com.tr>.

A useful report includes:

- What the issue is and where it lives (file, function, or dependency).
- Steps to reproduce, or a proof of concept.
- The impact you believe it has.
- Any suggested fix, if you have one.

## What to expect

This is a personal project maintained in spare time, so treat these as
intentions rather than guarantees: an acknowledgement within a few days, an
assessment of whether it is reproducible, and a fix in the next release if it
is. You will be credited in the release notes unless you would rather not be.
