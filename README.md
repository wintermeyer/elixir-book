# Elixir

Source for the standalone Elixir book at
<https://wintermeyer-consulting.de/elixir/book/>.

Content was lifted from the Elixir chapter of
[_An Elixir, Phoenix and Ash Beginner's Guide_](https://github.com/wintermeyer/phoenix-book).
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

## Where the content is edited

In this repo, under `modules/ROOT/pages/`. The Phoenix book no
longer has an Elixir chapter — this repo is the one source of truth.

## License

See individual files for attribution.
