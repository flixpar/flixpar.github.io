# Repository Guidelines

## Project Structure & Module Organization
This repository is a simple static personal site. The main entry point is `index.html`, with shared styling in `main.css`. Supporting pages such as `oldprojects.html`, plus site metadata files like `robots.txt`, `sitemap.xml`, `CNAME`, and `favicon.ico`, live at the repo root. Research abstracts are stored in `abstracts/*.txt` and loaded on demand by the inline JavaScript in `index.html`. Images and icons live in `imgs/`. It is hosted on GitHub Pages.

## Build, Test, and Development Commands
There is no build step or package-based toolchain in this repo.

- `python3 -m http.server 8000`
  Runs a local static server from the repository root.
- `open http://localhost:8000`
  Opens the site locally on macOS for a quick visual check.
- `git diff`
  Review HTML, CSS, text, and asset path changes before committing.

## Coding Style & Naming Conventions
Follow the existing style in the repo: use tabs for indentation in `index.html` and `main.css`, keep HTML/CSS formatting compact, and prefer clear, descriptive IDs and class names. Use lowercase, hyphenated identifiers for project sections and related assets, for example `counts-project`, `counts-abstract`, and `imgs/counts.png`. When adding a new abstract toggle, keep the `id` in `index.html` aligned with the matching `abstracts/<id>.txt` filename.
