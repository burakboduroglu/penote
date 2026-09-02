# Changelog

All notable changes to penote are recorded here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the project
follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [3.0.1] - 2026-09-02

### Fixed

- Republished `@burakboduroglu/penote` so the npm packument is complete and
  `npm install @burakboduroglu/penote` / `npm view` resolve correctly. The
  earlier `3.0.0` tarball existed without a usable package root document.

## [3.0.0] - 2026-09-02

### Added

- Brand assets in the same visual language as the other repositories:
  `assets/social-preview.svg` / `.png` (GitHub link preview, 1280x640) and
  `assets/demo.svg` / `.png` (README terminal card). The SVG is the source; the
  PNG is rendered from it.
- CI smoke job that runs the documented `bun` development commands on Ubuntu and
  macOS, alongside the existing Node matrix.

### Changed

- Product renamed to **penote**. npm package is now
  [`@burakboduroglu/penote`](https://www.npmjs.com/package/@burakboduroglu/penote);
  CLI binary is `penote`. The previous unscoped name `devnotetr` / `devnote` is
  retired. The GitHub repository was renamed `dev-notes` -> `penote`; GitHub
  redirects the old URLs.
- Repository surface aligned with the rest of the open-source set: English
  README positioned as agentic learning docs, `CHANGELOG.md`, `SECURITY.md`,
  `CODE_OF_CONDUCT.md`, Conventional Commits in `CONTRIBUTING.md`, YAML issue
  forms, pull request template, and a CI smoke workflow.
- License file renamed from `LICENSE.md` to `LICENSE`.
- App icon redesigned as a lowercase `pn` monogram with an AI sparkle on a
  rounded indigo tile (`assets/penote-logo.svg`); the Web UI favicon and the
  social preview card use the same mark.
- `bun` is the package manager and local runner throughout: install
  (`bun add -g`), scripts (`bun run start` / `bun run dev`) and every documented
  development command (`bun library/cli.js …`). The published binary still
  targets Node.js 18+ built-ins, and CI keeps the Node 18/20/22 matrix.
- The npm tarball ships only `assets/penote-logo.svg` and `assets/demo.png`; the
  social preview card is repository-only, halving the package to ~130 kB.

### Removed

- Tracked `.vscode/` settings (editor-local; ignored going forward).

## [2.1.0] - 2026-05-04

### Added

- Packaged CLI and notes as the `devnotetr` npm package (`devnote` binary)
  — superseded by `@burakboduroglu/penote` / `penote`.
- Category folders for Java, JavaScript, Python, SQL, and MongoDB notes.
- Zero-dependency CLI with list, search, open (editor / TUI / browser).
- Single-file Web UI with category filter and instant search.

[3.0.1]: https://github.com/burakboduroglu/penote/compare/v3.0.0...v3.0.1
[3.0.0]: https://github.com/burakboduroglu/penote/compare/v2.1.0...v3.0.0
[2.1.0]: https://github.com/burakboduroglu/penote/releases/tag/v2.1.0
