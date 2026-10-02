# nechalmaggon.com

Personal website, served by GitHub Pages at [nechalmaggon.com](https://nechalmaggon.com). It is plain static HTML and CSS: no build step, no framework, no dependencies. Whatever is on `main` is what gets published.

## How URLs map to files

Every page is a folder containing an `index.html`. The folder path is the URL path, so URLs have no `.html` extension.

| URL | File |
| --- | --- |
| `/` | `index.html` |
| `/nibble/` | `nibble/index.html` |
| `/nibble/privacy/` | `nibble/privacy/index.html` |
| `/nibble/terms/` | `nibble/terms/index.html` |
| `/nibble/support/` | `nibble/support/index.html` |

## Repo structure

```
.
├── index.html          # Home / portfolio page (currently a placeholder)
├── style.css           # Single shared stylesheet for every page
├── fonts/              # Self-hosted Press Start 2P (woff2) + OFL license
├── CNAME               # Custom domain (nechalmaggon.com), required by GitHub Pages
├── .nojekyll           # Tells GitHub Pages to skip Jekyll processing
└── nibble/             # Project: Nibble Chrome extension
    ├── index.html      # Landing page
    ├── icon.png        # Favicon + project icon
    ├── cookie.png      # Mascot image
    ├── privacy/index.html
    ├── terms/index.html
    └── support/index.html
```

Hierarchy: the site root is the portfolio; each project lives in its own top-level folder (`/<project>/`) with its landing page at `<project>/index.html`. Project-specific sub-pages (privacy, terms, support, etc.) are nested one level deeper as `<project>/<page>/index.html`. Project-only assets (images, icons) sit next to the project's landing page. Assets shared by the whole site (`style.css`, `fonts/`) stay at the root.

## Conventions

- **Absolute paths.** Pages reference assets and links from the root (`/style.css`, `/nibble/icon.png`, `/nibble/privacy/`) so they work from any depth. Link to folders with a trailing slash.
- **Shared styles.** All pages link `/style.css`. Add new styles there rather than inline, and reuse the existing CSS variables in `:root`.
- **Page types.** Landing pages use a plain `<body>`. Text-heavy pages (privacy, terms, support) use `<body class="legal">` and start with a back link such as `<p><a href="/nibble/">← nibble</a></p>`.
- **Footer.** Project pages end with a `<footer>` linking back to `nechalmaggon.com` and to the project's privacy, terms and support pages.
- **Head boilerplate.** Each page needs `charset`, `viewport`, a `<title>`, a meta `description`, the favicon link and the stylesheet link. Copy it from an existing page.

## Adding a new project (e.g. `nechalmaggon.com/myapp`)

1. Create a folder at the root: `myapp/`.
2. Copy `nibble/index.html` to `myapp/index.html` and update the title, description, favicon path and content.
3. Put the project's images in `myapp/` (e.g. `myapp/icon.png`) and reference them as `/myapp/icon.png`.
4. If needed, add sub-pages by copying an existing one, e.g. `myapp/privacy/index.html`, `myapp/terms/index.html`, `myapp/support/index.html`. Update the back link and the footer.
5. Link the project from the home page (`index.html`).
6. Commit and push to `main`. The page is live at `nechalmaggon.com/myapp/` after GitHub Pages finishes deploying (usually within a minute or two).

## Adding a page to an existing project

Create `<project>/<page>/index.html` (copy a sibling such as `nibble/support/index.html`), then link to it from the project's footer and anywhere else relevant.

## Local preview

Because links are root-absolute, preview with a local server from the repo root rather than opening files directly:

```bash
python3 -m http.server 8000
```

Then visit http://localhost:8000/.

## Notes

- Don't delete `CNAME`; removing it disconnects the custom domain.
- Don't delete `.nojekyll`; it makes GitHub Pages serve files as-is.
- Open `TODO` comments in the HTML (e.g. the Chrome Web Store link and screenshots on the Nibble page) mark content still to be filled in.
