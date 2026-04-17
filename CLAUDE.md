# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static single-page personal website for Felix Parker, served at felixparker.com. No build system, no package manager, no tests — raw HTML/CSS deployed via GitHub Pages (the `CNAME` file pins the custom domain).

## Local preview

Open `index.html` directly, or run a local server from the repo root:

```
python3 -m http.server 8000
```

A server (rather than `file://`) is needed because abstracts are loaded via `fetch` and browsers block that on the file protocol.

## Architecture

The whole site is `index.html` + `main.css` + assets under `imgs/`. There is no templating — every project is an inline `<div class="project">` block.

**Lazy-loaded abstracts.** Each project that shows a "¶ Abstract" link wires `onclick="toggle_visibility('<slug>-abstract')"` to a `<p id="<slug>-abstract" class="abstract-text">`. The `toggle_visibility` function in `index.html` fetches `abstracts/<slug>-abstract.txt` on first open and injects the text. To add an abstract for a new project:

1. Give the `<p>` a unique id ending in `-abstract`.
2. Create `abstracts/<same-id>.txt` containing the abstract text.
3. The filename (minus `.txt`) **must** match the element id exactly, or the fetch 404s silently.

**`oldprojects.html`** is not linked from anywhere and is not a standalone page — it's a scratch file holding markup for projects that have been removed from the live site. Treat it as an archive/snippet store, not as content to serve.

**Layout responsiveness.** `main.css` switches from a two-column desktop layout to a top-fixed-header mobile layout at `max-width: 700px`. Changes to the sidebar (`#sidebar`, `#nav`, `#social`, `#title`, `#felix`) usually need a matching tweak inside that media query.

**Navigation anchors.** Sidebar links use `#home`, `#aboutme`, `#projects-ongoing`, `#projects-completed`, `#contact`. Each section has both `id="..."` and a legacy `<a name="...">` anchor — keep both when adding sections so existing links don't break.

## SEO / crawler surface

`robots.txt`, `sitemap.xml`, and the `<meta name="robots">` / canonical tags in `index.html` are intentionally permissive (including `Content-Signal: ai-train=yes`). If you change site structure, update `sitemap.xml`'s `lastmod` and add any new top-level pages there.
