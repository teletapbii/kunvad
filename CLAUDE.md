# KUNVAD personal site

Live personal site for Tap KunvaD, deployed via Vercel, pushed from this repo to
`github.com/teletapbii/kunvad`.

## Structure

- `index.html` — the actual site. Self-contained single-page app (home / project /
  blog views toggled via internal state, no build step). Depends on `support.js`.
- `support.js` — shared runtime that powers the custom `<x-dc>` / `<sc-if>` /
  `{{ }}` template tags used across these pages. Don't remove even though
  `index.html` looks like plain HTML.
- `doc-page.js` — separate web component (`<doc-page>`) for printable/paginated
  documents. Only used by `KUNVAD-ClaudeCode-Guide.dc.html`.
- `KUNVAD-*.dc.html` — standalone page exports (Home, Me, Project, Blog, Hi, CMS,
  ClaudeCode-Guide) authored separately from `index.html`. **Not yet wired into
  the router in `index.html`** — currently only reachable by loading the file
  directly. Treat as drafts/content-in-progress until linked in.
- `uploads/` — images referenced by the `.dc.html` pages.
- `profile.jpg` — leftover from an earlier single-page version of the site;
  check before removing in case anything still references it.

## Source of truth

The parent folder (`../KUNVAD CMS/`, `../Kunvad v2/`, zips, Figma file, mood
images in `../ref style for website/`) holds drafts and reference material.
This `deploy/` folder is the one that actually ships — copy finished work in
here rather than editing in two places.

## Known issue

The git remote previously had a GitHub PAT embedded in the URL
(`https://<user>:<token>@github.com/...`). If you see this again, switch to SSH
or the OS credential helper and rotate the token — a plaintext token in
`.git/config` is a local leak risk (backups, zips, screen shares).
