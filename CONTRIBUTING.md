# Contributing to penote

Thanks for looking. This repository is **agentic learning docs**: Turkish
Markdown notes organised by topic, plus a zero-dependency Node.js CLI and a
single-file Web UI so humans and coding agents can find and open the same
material.

Useful contributions are usually small — a clearer note, a missing example, a
CLI edge case, or a Web UI fix. Before building anything substantial, open an
issue and check the direction is wanted.

**Out of scope for drive-by PRs:** renaming category folders, adding a package
manager / build toolchain for the notes CLI, splitting the Web UI into multiple
files, or turning the project into a general CMS.

Please read the [Code of Conduct](CODE_OF_CONDUCT.md) before participating.

## Getting started

**Requirements:** [bun](https://bun.sh) for development, Node.js ≥ 18 for the
published binary. No `bun install` is required — the CLI has no dependencies.

```bash
git clone https://github.com/burakboduroglu/penote.git
cd penote
bun library/cli.js list
bun library/cli.js search hibernate
bun library/cli.js open --editor
```

| Command | What it does |
| ------- | ------------ |
| `bun library/cli.js list` | Discover every note |
| `bun library/cli.js search <kw>` | Full-library search |
| `bun library/cli.js open --tui` | Interactive TUI |
| `bun library/cli.js open --editor` | Local Web UI |
| `bun run start` | Same as `bun library/cli.js` |
| `bun run dev` | Open the Web UI |

CI runs list/search smoke checks on Node 18, 20, and 22.

## Where things live

```
*-Notes/              Topic Markdown (Turkish explanations)
library/cli.js        CLI / TUI — Node built-ins only
library/index.html    Web UI — single file, no CDN
assets/               Logo and static assets
AGENTS.md             Rules for coding agents editing this repo
```

## Adding or editing notes

- Place the file in the correct `*-Notes/` folder.
- Name it `lowercase_with_underscores.md`; use `_1`, `_2` for multi-part series.
- Follow the note template in [AGENTS.md](AGENTS.md): Turkish prose, fenced
  code blocks with a language tag, no YAML frontmatter, no external images.
- Do not rename existing category folders — the CLI derives categories from them.

## Commits

Commit messages follow [Conventional Commits](https://www.conventionalcommits.org):

```
feat(notes): add spring transaction boundaries note
fix(cli): search flag not filtering by category
docs: clarify TUI key bindings in README
chore(ci): run smoke checks on Node 22
```

| Type | Use for |
| ---- | ------- |
| `feat` | New note, CLI capability, or Web UI behaviour |
| `fix` | Incorrect behaviour or broken content |
| `docs` | README, contributing, comments that do not change behaviour |
| `refactor` | Internal cleanup with no user-visible change |
| `chore` | CI, tooling, release prep |

Optional scopes: `notes`, `java`, `javascript`, `python`, `sql`, `mongodb`,
`cli`, `web-ui`, `docs`, `ci`.

Use the imperative mood, keep the subject under ~72 characters, and put the
reasoning in the body when the change is not self-evident. No emoji.

## Pull requests

Branch from `main`, keep the change focused, and fill in the template. Say what
changed, why, and how you verified it.

- Update `README.md` when CLI flags, TUI keys, or project layout change.
- Add a `CHANGELOG.md` entry under `Unreleased` for anything a user would notice.
- Keep the CLI zero-dependency and the Web UI a single file unless the change
  is explicitly about that architecture.

Do not commit secrets, tokens, or machine-specific paths.

## Reporting

- **Bugs and ideas:** [the issue tracker](https://github.com/burakboduroglu/penote/issues)
- **Vulnerabilities:** privately, per [SECURITY.md](SECURITY.md) — never as a public issue

Thank you for contributing.
