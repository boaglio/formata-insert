# AGENTS.md

Guidance for coding agents working in this repo.

## What this is

A single-page tool that pretty-prints SQL `INSERT` statements (one
column/value per line, still valid SQL you can run as-is). The entire
app is `index.html` — HTML, CSS, and
vanilla JS in one file, no build step, no dependencies, no package.json.
Keep it that way; do not introduce a bundler, framework, or npm packages
unless explicitly asked.

## Files

- `index.html` — the whole app (markup, styles, and script inline).
- `.github/workflows/jekyll-gh-pages.yml` — deploys `main` to GitHub
  Pages (via the Jekyll passthrough build) on every push.
- `README.md` — user-facing description, in Portuguese (matches the UI).
- `formata-insert.png` — screenshot used in the README.

## The parser (inside `index.html`'s `<script>`)

The core logic is a small hand-written tokenizer, not a single regex:

- `skipQuoted` / `findMatchingParen` / `splitTopLevel` — generic
  quote- and paren-aware scanning helpers.
- `splitStatements` — splits input into individual `INSERT` statements
  on top-level `;`.
- `parseInsertStatement` — parses one statement: table name, optional
  column list, and one or more `VALUES (...)` tuples (multi-row insert).
- `formatParsedStatement` — turns a parsed statement back into
  pretty-printed, valid SQL (columns and, for single-row inserts,
  values each on their own line; multi-row inserts keep one row per
  line).
- `formatarSQL` / `copiarResultado` / `limpar` — DOM glue (button
  handlers) plus a debounced `input` listener for auto-formatting.

When touching the parser, preserve support for: commas/parens inside
quoted strings, escaped quotes (`''`), nested function calls in values
(e.g. `NOW()`, `CONCAT(a,b)`), multi-row `VALUES (...), (...)`, and
multiple statements separated by `;`.

## Testing changes

There is no test suite or CI test step. To verify parser changes without
a browser, extract the `<script>` contents from `index.html` and `eval`
them in Node — the parsing functions (`splitStatements`,
`parseInsertStatement`, `formatParsedStatement`) have no DOM dependency,
only `formatarSQL`/`copiarResultado`/`limpar` touch `document`. Example
harness:

```js
const fs = require('fs');
const html = fs.readFileSync('index.html', 'utf8');
const script = html.match(/<script>([\s\S]*?)<\/script>/)[1];
eval(script.replace(/document\.getElementById\('sqlInput'\)[\s\S]*$/, ''));
// now call splitStatements(sql), parseInsertStatement(stmt), etc.
```

For actual UI verification (button clicks, clipboard, live styling),
serve the file (`python3 -m http.server`) and drive it with a real
or headless browser — this sandbox may not have one available; say so
explicitly rather than claiming the UI was tested if it wasn't.

## Conventions

- UI strings (labels, placeholders, error messages) are in Portuguese —
  keep new user-facing text consistent with that.
- No comments explaining *what* code does; only note non-obvious *why*
  (e.g. why an escape rule or edge case is handled a certain way).
- Don't add a build step, TypeScript, or a JS framework for a change
  that doesn't need one — this project's value is staying a single
  static file.
