# KUNVAD personal site

Live personal site for Tap KunvaD, deployed via Vercel, pushed from this repo to
`github.com/teletapbii/kunvad`.

## Structure

- `index.html`, `me.html`, `blog.html`, `project.html`, `hi.html` — the site's
  five real pages (Home/Me/Blog/Project/Hi). Each is a standalone document
  (no build step), navigated via real links (`vercel.json` sets
  `cleanUrls: true`, so `/me` serves `me.html`, etc — this only works on
  Vercel, not a plain static server).
- `support.js` — shared runtime that powers the custom `<x-dc>` / `<sc-if>` /
  `{{ }}` template tags used across every page. Don't remove.
- `doc-page.js` — separate web component (`<doc-page>`) for printable/paginated
  documents. Only used by `KUNVAD-ClaudeCode-Guide.dc.html` (a personal
  reference doc, not part of site nav).
- `cms.html` — the content editor. Open it directly (not linked from the
  public site nav) to edit theme colors, nav labels, and per-page text/image.
- `content.json` — the published content every page fetches on load. This is
  what real visitors see; edits in `cms.html` only show live to *you*
  (via `localStorage`) until exported and committed here.
- `uploads/` — images referenced by the pages.
- `profile.jpg` — leftover from an earlier single-page version of the site;
  check before removing in case anything still references it.

## Editing content

1. Open `cms.html` in a browser (locally or the deployed `/cms` URL).
2. Edit fields on the left — the preview panel on the right updates live.
   This live-preview only affects your own browser (`localStorage`), not
   other visitors.
3. Click **Export** → downloads `kunvad-content.json`.
4. Replace `content.json` in this repo with the export, commit, push.
   Every page fetches `content.json` on load, falling back to any
   `localStorage` override, then to hardcoded defaults (`_D` in each page's
   script) if both are missing a field.

Known rough edge: on a browser that has never opened `cms.html` before,
the editor starts from `content.json`'s published values (seeded once on
first load) rather than a fresh blank state — if you want to start fully
fresh, clear `localStorage['kunvad_cms']` first.

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
