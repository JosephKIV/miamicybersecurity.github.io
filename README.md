# miamicyber.org

The Miami University Cybersecurity Club website — a [Jekyll](https://jekyllrb.com)
site published with GitHub Pages at <https://miamicyber.org>.

**Adding a meeting, officer or sponsor? See [CONTRIBUTING.md](CONTRIBUTING.md).**
You do not need to install anything for that.

## Layout

```
_layouts/default.html   page shell: <head>, navbar, particle canvas, footer
_layouts/post.html      a meeting with a write-up
_layouts/redirect.html  a meeting that is only a link to a slide deck
_includes/ap-date.html  renders dates the way the old site did (Sept. 24, 2025)

index.html              homepage: welcome card + meetings by semester
about.html              executive board and alumni
sponsors.html           sponsors and how to support the club
muctf.html              CTFtime results
404.html                served for unknown URLs
admin.html              /admin/ — inherited joke, redirects to a music video

_posts/                 one file per meeting; filename sets date and URL
_data/                  officers, alumni, sponsors, banner, alert, ctftime
assets/                 css, js, images
```

Meeting pages live at top-level URLs (`/s26-m5/`), set by `permalink: /:slug/`
in `_config.yml`. That matches the URLs the previous site served, so existing
links in Discord, slides and flyers keep working — don't change it.

## Local development

```sh
bundle install
bundle exec jekyll serve   # http://localhost:4000
```

Requires Ruby 3.x. `_config.yml` is not reloaded automatically; restart the
server after editing it.

## Deployment

`.github/workflows/pages.yml` builds and publishes on every push to `main`.

The build deliberately uses our own Jekyll 4 rather than GitHub's built-in Pages
builder, which pins Jekyll 3.10 and lacks filters this site uses. Do not swap the
`jekyll` gem for the `github-pages` gem.

The custom domain is set by the `CNAME` file.

## History

This replaces a Django application (Docker Compose, Postgres, Traefik, a
DigitalOcean droplet) that served the same five pages. The visual design is a
direct port — same Bootstrap 4.6.1, same hand-written `styles.min.css`, same
typewriter and particle effects in `script.min.js`.

All 57 meetings from Fall 2023 onward were migrated out of the old database into
`_posts/`, keeping their dates, authors and URLs, along with the executive board
and alumni into `_data/` and the officer photos into `assets/img/exec/`. The
sponsor list in `_data/sponsors.yml` is the one thing still to fill in — it was
empty on the old site too.

## A note on the port

The migration was carried out with an agentic coding assistant, with the goal
of a fast, faithful 1:1 port rather than a rewrite.

The site is static, small and easy to reason about, so the practical cost of
that is low. A cleanup pass may happen later as maintainer time allows, but it
isn't a prerequisite for contributing. If something here is awkward enough to
slow you down, fix it in the pull request you're already making.
