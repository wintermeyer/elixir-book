# Elixir

Source for the standalone Elixir book at
<https://wintermeyer-consulting.de/elixir/book/>.

Content was lifted from the Elixir chapter of the
[_Phoenix_ book](https://github.com/wintermeyer/phoenix-book).
The Phoenix book used to render the same pages under
`/phoenix/book/elixir/*`; those URLs now 301-redirect here.

## Build

The book is built with [Antora](https://antora.org). The chrome
(Tailwind v4 theme, sidebar, right TOC, pagination, mobile nav)
comes from the shared UI bundle at
[`wintermeyer/wincon-antora-ui`](https://github.com/wintermeyer/wincon-antora-ui).

```sh
npm install
npx antora --fetch antora-local-playbook.yml
```

Open `build/site/book/index.html` to preview.

## Deployment

Pushing to `main` triggers `.github/workflows/deploy.yml`, which
runs on the self-hosted runner `bremen2-eliph-elixir-book` on
bremen2. The runner fetches the wincon nav/footer (stamping
`data-book-current="elixir"`), renders with Antora, copies into
`/var/www/elixir-book/releases/<ts>/`, and atomically swaps the
`current` symlink. Nginx serves `/elixir/book/` from there.

Before the swap the deploy pre-compresses every text asset
(`.html`, `.css`, `.js`, `.svg`, `.xml`, `.json`, `.mjs`, `.txt`,
`.map`) into `.br` (brotli q11) and `.gz` (gzip -9) siblings so
nginx's `brotli_static` / `gzip_static` can serve the response
without spending CPU on the hot path. The brotli module is
already loaded site-wide on bremen2 via the wincon vhost.

## Where the content is edited

In this repo, under `modules/ROOT/pages/`. The Phoenix book no
longer has an Elixir chapter, this repo is the one source of truth.

## Chapter layout

The book is organised so each concept is introduced before it is used.
The top-level sections are, in reading order:

1. First Steps (iex, hello world, basic calculations, basic debugging)
2. Basic Data Types (integers & floats, booleans, atoms, strings)
3. Operators (arithmetic, comparison, boolean, pipe, match, range, capture, cons, and the two string operators)
4. Modules and Functions (plus higher-order functions, variables, scopes, immutability)
5. Collections (lists, tuples, keyword lists, maps, structs, type conversions)
6. Pattern Matching (overview, guards, multi-clause functions)
7. Control Flow (if, case, cond, with, for)
8. Enumerables (Enum, Stream, recursion, logical expressions)
9. More (error handling, binaries and charlists, sigils, Mix, testing with ExUnit)

Processes, GenServer, and OTP are intentionally out of scope here and live in the Phoenix book.

## License

See individual files for attribution.
