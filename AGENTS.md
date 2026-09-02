# AGENTS.md

> Guide for AI agents working in this repository.
> Read this file before making any change.

---

## Project Summary

**penote** (CLI: `penote`, npm: `@burakboduroglu/penote`) is an **agentic
learning docs** library: programming notes in Markdown, organised by
language/topic, reachable via a zero-dependency Node.js CLI and a
browser-based Web UI.

The GitHub repository, the npm scope and the CLI binary are all **penote**.

- **No build step for the notes tooling.** Node.js 18+ is the only runtime
  requirement for the published CLI and Web UI.
- **Use `bun` for every local command** (`bun library/cli.js …`, `bun run dev`).
  Never write `npm`, `pnpm`, or `yarn` in docs or scripts. The published binary
  still targets Node.js built-ins, so do not introduce bun-only APIs.
- **Content is king.** The value of this repo is in the `.md` notes, not the
  tooling.
- **CLI entry point:** `library/cli.js` (binary name: `penote`)
- **Web UI entry point:** `library/index.html`
- **Human-facing repo docs** (README, CONTRIBUTING, SECURITY, …) are English.
  **Note bodies** stay Turkish (see below).

---

## Repository Structure

```
penote/                  # GitHub repo / local folder name
├── Java-Notes/          # Lombok, JPA/Hibernate, Spring Boot
├── Javascript-Notes/    # Array methods, closures, async, regex
├── Python-Notes/        # Basics, advanced topics, DB operations
├── SQL-Notes/           # Basic queries, advanced SQL, psql terminal
├── MongoDB-Notes/       # Basic CRUD and querying
├── library/
│   ├── cli.js           # CLI tool (Node.js, no dependencies)
│   └── index.html       # Web UI (vanilla HTML/JS/CSS)
├── assets/
│   ├── penote-logo.svg     # App icon; SVG is the source of truth
│   ├── social-preview.svg  # GitHub link preview card (1280x640)
│   ├── social-preview.png  # Rendered from the SVG; uploaded by hand
│   ├── demo.svg            # README terminal card (1000x620)
│   └── demo.png            # Rendered from the SVG
├── .github/             # Issue forms, PR template, CI / publish workflows
├── AGENTS.md
├── CHANGELOG.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── SECURITY.md
└── package.json         # npm package metadata for `@burakboduroglu/penote`
```

---

## Adding or Editing Notes

### Naming Convention

| Rule                                         | Example                                  |
| -------------------------------------------- | ---------------------------------------- |
| Lowercase, words separated by `_`            | `python_basic_1.md`                      |
| Suffix with `_1`, `_2` for multi-part series | `sql_advanced_1.md`, `sql_advanced_2.md` |
| Place in the correct category folder         | `Python-Notes/advanced_python_3.md`      |

### Note file template

Every new note should follow this shape:

```markdown
# Topic title

> One-sentence Turkish summary of this note.

---

## Section 1

Content here...

## Section 2

Content here...

---

**Kaynaklar**

- Source or documentation link (if any)
```

### Note content rules

- **Language: all notes must be written in Turkish.** Material taken from
  English sources still needs Turkish explanation and summary. Technical terms
  (`variable`, `function`, `query`, …) may stay in English; explanations must
  be Turkish.
- **When updating older English notes:** write the Turkish equivalent first,
  then keep the technical content accurate.
- **Code blocks:** always include a language identifier (```` ```java ````,
  ```` ```python ````, etc.).
- **No external images in notes.** If needed, use a relative path under
  `assets/`.
- **Stay focused:** one concept (or a tight related group) per file.
- **No frontmatter (YAML/TOML):** the CLI parses plain Markdown only.

---

## Working with the CLI (`library/cli.js`)

### What the CLI does

- Reads all `.md` files from the category folders.
- Provides list, search, open (editor / TUI / browser), and help commands.
- Parses file paths to derive category and note name — **folder and file naming
  directly affects CLI output.**

### Rules when modifying `cli.js`

- Do **not** introduce runtime dependencies. Use only Node.js built-in
  modules.
- Do **not** change the command interface (flags, subcommands) without updating
  `README.md`.
- Keep the TUI key bindings consistent with the table in `README.md`.
- Keep the published binary name `penote` unless an explicit rename is requested.
- Test every modified command manually before committing:

```bash
bun library/cli.js list
bun library/cli.js search <keyword>
bun library/cli.js open --tui
```

---

## Working with the Web UI (`library/index.html`)

- Single-file, vanilla HTML/CSS/JS. Do **not** split into separate files.
- Do **not** add external CDN dependencies.
- Category filtering and instant search must remain functional after any change.
- Test in a browser by starting the HTTP server:

```bash
bun library/cli.js open --editor
```

---

## Working with brand assets (`assets/`)

- The **SVG is the source of truth**; the PNG next to it is a render. Never edit
  a PNG by hand — change the SVG and re-render:

```bash
rsvg-convert -w 1280 -h 640 assets/social-preview.svg -o assets/social-preview.png
rsvg-convert -w 1000 -h 620 assets/demo.svg  -o assets/demo.png
```

- `social-preview.png` is the GitHub link preview. GitHub has no API for it, so
  it is uploaded by hand under **Settings > General > Social preview**.
- Terminal text inside `demo.svg` and `social-preview.svg` must match what
  `library/cli.js` actually prints — re-run the command before changing a line.
- Keep the indigo palette and the rounded-tile mark consistent across all three
  files and the Web UI favicon in `library/index.html`.
- SVG comments must not contain `--` (it is an XML parse error); write CLI flags
  in prose instead.

---

## What Agents Should NOT Do

- Do **not** rename existing category folders (`Java-Notes`, `Python-Notes`,
  etc.) — the CLI resolves categories from folder names.
- Do **not** add a dependency lockfile or package-manager toolchain for the
  notes CLI. The existing root `package.json` is publish metadata only; keep
  the CLI zero-dependency.
- Do **not** modify `LICENSE` unless the copyright holder asks.
- Do **not** add auto-generated files or compiled output to the repo.
- Do **not** edit `CONTRIBUTING.md`, `SECURITY.md`, or `CODE_OF_CONDUCT.md`
  unless explicitly asked (or the change is part of an approved repo-surface
  update).
- Do **not** create notes outside the established category folders without
  confirming with the user.

---

## Commit Message Convention

Follow [Conventional Commits](https://www.conventionalcommits.org):

```
<type>(<optional-scope>): <short description>
```

| Types | `feat` \| `fix` \| `docs` \| `refactor` \| `chore` \| `remove` |
| Scopes | `notes` \| `java` \| `javascript` \| `python` \| `sql` \| `mongodb` \| `cli` \| `web-ui` \| `docs` \| `ci` |

**Examples:**

```
feat(python): add advanced decorators note
fix(cli): search flag not filtering by category
docs: add new CLI command to README
chore(ci): smoke-test list and search on Node 22
```

---

## Quick Checklist Before Committing

- [ ] Note file follows the naming convention (`lowercase_with_underscores.md`)
- [ ] Note is placed in the correct category folder
- [ ] Code blocks have language identifiers
- [ ] CLI still runs without errors (`bun library/cli.js list`)
- [ ] Commit message follows Conventional Commits
- [ ] `README.md` updated if CLI commands or project structure changed
- [ ] `CHANGELOG.md` updated under `Unreleased` for user-visible changes
