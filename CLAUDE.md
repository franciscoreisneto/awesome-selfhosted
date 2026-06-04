# CLAUDE.md

Guidance for AI assistants (Claude Code and others) working in this repository.

## What this repository is

`awesome-selfhosted` is a curated [awesome list](https://github.com/sindresorhus/awesome)
of **Free Software** network services and web applications that can be hosted on
your own server(s). The list is published in two forms:

- **HTML version (recommended):** <https://awesome-selfhosted.net/>
- **Markdown version (legacy):** the `README.md` in this repository.

Non-Free software is listed separately in `non-free.md`.

## ⚠️ Most important thing to understand: this repo is GENERATED output

`README.md` and `non-free.md` are **build artifacts**. They are generated
automatically by a bot from the upstream data repository
[`awesome-selfhosted/awesome-selfhosted-data`](https://github.com/awesome-selfhosted/awesome-selfhosted-data).

You can see this in the git history — most commits look like:

```
[bot] build markdown from awesome-selfhosted-data <sha>
```

**Consequences for any work you do here:**

- **Do NOT hand-edit `README.md` or `non-free.md` to add, remove, or change a
  software entry.** Such edits will be overwritten by the next bot build and are
  rejected by the project. The canonical source is the YAML data in
  `awesome-selfhosted-data` (one file per software entry under `software/`, plus
  `tags/`, `platforms/`, and `licenses.yml`).
- The upstream project **does not accept pull requests or issues in this repo.**
  - `.github/PULL_REQUEST_TEMPLATE.md` says: *"Please do not submit pull requests
    in this repository. Use awesome-selfhosted-data instead."*
  - `.github/ISSUE_TEMPLATE/config.yml` disables blank issues and redirects to
    `awesome-selfhosted-data`.
  - Contributing guidelines live at
    <https://github.com/awesome-selfhosted/awesome-selfhosted-data/blob/master/CONTRIBUTING.md>.

If a user asks you to add/edit/remove a listing, the correct action is to point
them to (or work against) `awesome-selfhosted-data`, **not** to patch the
Markdown here.

> Note: This is a personal fork (`franciscoreisneto/awesome-selfhosted`). The
> upstream is `awesome-selfhosted/awesome-selfhosted`. The two repositories above
> remain the authoritative locations for the list's source data and contributions.

## Repository layout

```
.
├── README.md                     # GENERATED — the Free Software list (~315 KB)
├── non-free.md                   # GENERATED — the Non-Free Software list
├── LICENSE                       # CC-BY-SA-3.0 (the list content license)
├── _static/awesome.png           # "Awesome" badge image used in README
├── pseg/                         # Unrelated static site added in this fork (see below)
│   └── index.html
└── .github/
    ├── PULL_REQUEST_TEMPLATE.md  # Redirects contributors upstream
    └── ISSUE_TEMPLATE/config.yml # Redirects issues upstream
```

### The `pseg/` directory (fork-specific, unrelated to the list)

`pseg/index.html` is a **standalone marketing website** for a clinical research
center ("PSEG Centro de Pesquisa Clínica", a neurology clinic in São Paulo),
written in Portuguese. It is a single self-contained HTML file that renders a
React 18 app via in-browser Babel (CDN `unpkg` scripts) — no build step.

This is completely unrelated to the awesome-selfhosted list and was added in this
fork. When working on `pseg/`, treat it as an independent project:

- It is a single HTML file; edit it directly.
- React/JSX is transpiled in the browser via `@babel/standalone` — there is no
  bundler, package manager, or test suite.
- To preview it locally, open the file in a browser or serve the directory with
  any static server (e.g. `python3 -m http.server` from inside `pseg/`).

## Markdown list conventions (for reference)

Even though you should not hand-edit the generated files, understanding the format
is useful when reading or answering questions about them. Both `README.md` and
`non-free.md` share the same structure:

1. **Header** — title, description, links to HTML/Markdown versions.
2. **Table of contents** — links to every category.
3. **`## Software`** — entries grouped by `### Category` (alphabetical), each
   category having a "back to top" link and a short description, sometimes with a
   `_Related: [...]_` cross-reference line.
4. **`## List of Licenses`** — SPDX identifier → license name + spdx.org link.
5. **`## Anti-features`** — legend for warning markers.
6. **`## External Links`**, **`## Contributing`**, **`## License`**.

### Anatomy of a software entry

```
- [Name](homepage-url) `⚠` - Description, max ~250 chars. ([Demo](url), [Source Code](url), [Clients](url)) `License-SPDX` `Language/Platform`
```

- **Name + homepage link** come first.
- An optional **`⚠`** marker means *"Depends on a proprietary service outside the
  user's control"* (the only anti-feature legend defined).
- **Description** is a single sentence; "(alternative to X, Y)" is a common suffix.
- Optional **parenthesized links**: `Demo`, `Source Code`, `Clients`, etc.
- One or more **license tags** in backticks (SPDX IDs, slash-separated for
  multi-licensed projects, e.g. `Apache-2.0/MIT`).
- One or more **language/platform tags** in backticks, slash-separated
  (e.g. `Nodejs/Docker`, `Go`, `PHP`).

Entries are sorted alphabetically (case-insensitive) within each category.

## Development workflow & conventions

- **No build system, dependencies, tests, or linters** live in this repository —
  it is a published mirror of generated Markdown plus the fork's `pseg/` site. All
  list tooling (generation, dead-link checks, unmaintained-project checks) runs in
  `awesome-selfhosted-data`.
- **Default branch:** `master`.
- **Content license:** the list is **CC-BY-SA-3.0** (see `LICENSE`), *not* a code
  license. Keep this in mind when discussing reuse of the list.

### Git / branching for AI-assisted work in this fork

- Do all work on the designated feature branch and never push directly to `master`
  without explicit permission.
- Create the branch locally if it does not exist.
- Push with `git push -u origin <branch-name>`; retry transient network failures
  with exponential backoff.
- **Do not open a pull request unless the user explicitly asks for one.** (And
  remember: PRs that change the list belong upstream in `awesome-selfhosted-data`,
  not here.)

## Quick decision guide

| If the user wants to…                                  | Do this |
|--------------------------------------------------------|---------|
| Add / edit / remove a software listing                 | Direct them to `awesome-selfhosted-data` (edit YAML there); do **not** patch `README.md`/`non-free.md`. |
| Fix a typo in a list entry                             | Same as above — the fix must be made to the upstream YAML source. |
| Understand the list format / answer a question         | Read `README.md` / this file; no changes needed. |
| Work on the clinic website                             | Edit `pseg/index.html` directly (standalone React-via-CDN site). |
| Change PR/issue redirect behavior                      | Edit files under `.github/`. |
