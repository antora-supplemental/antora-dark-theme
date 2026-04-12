# Antora Dark Theme

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Antora 3.x](https://img.shields.io/badge/antora-3.x-purple.svg)](https://antora.org)

Dark mode supplemental UI for [Antora](https://antora.org) documentation sites.

## Quick start

### Which installation path should I use?

- **If your project already uses Node/npm/pnpm** (common for Antora sites) — use **Method 1** (npm). To add your own supplemental files on top of this theme, use **Method 2** (valid Antora patterns only—see below).
- **If you want no JavaScript install step** (minimal CI, or a repo without Node) — use **Method 3** (pre-built `ui-bundle.zip`): one URL in the playbook, no `node_modules`.

### Method 1: npm dependency (recommended for Node-based projects)

```bash
# npm
npm install --save-dev antora-dark-theme

# pnpm
pnpm add -D antora-dark-theme

# yarn
yarn add -D antora-dark-theme

# bun
bun add -d antora-dark-theme
```

Then reference the supplemental UI from `node_modules` in `antora-playbook.yml` (or your playbook file):

```yaml
ui:
  bundle:
    url: https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/HEAD/raw/build/ui-bundle.zip?job=bundle-stable
    snapshot: true
  supplemental_files: ./node_modules/antora-dark-theme/supplemental-ui
```

### Method 2: Project overrides (valid Antora options)

Antora’s `ui.supplemental_files` accepts **either** a single directory path **or** an array of [virtual files](https://docs.antora.org/antora/latest/playbook/ui-supplemental-files) (`path` + `contents`). A YAML list of multiple **directories** is not supported—the array form is only for virtual entries.

**Merged directory (recommended when you use npm and need custom partials/CSS):** Copy `node_modules/antora-dark-theme/supplemental-ui` into your repo (for example `supplemental-ui/`), merge your changes on top, then point the playbook at that **one** folder:

```yaml
ui:
  bundle:
    url: https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/HEAD/raw/build/ui-bundle.zip?job=bundle-stable
    snapshot: true
  supplemental_files: ./supplemental-ui
```

**Pre-built theme bundle + virtual files:** Use the release `ui-bundle.zip` (default UI + dark theme already combined) and add only extra assets with a virtual `supplemental_files` array:

```yaml
ui:
  bundle:
    url: https://github.com/antora-supplemental/antora-dark-theme/releases/latest/download/ui-bundle.zip
    snapshot: true
  supplemental_files:
    - path: ui.yml
      contents: |
        static_files:
          - favicon.ico
    - path: favicon.ico
      contents: ./branding/favicon.ico
```

**Virtual override of a single UI file:** Each entry must use `path` and `contents` (inline or path to a file). If you replace a partial such as `partials/head-meta.hbs`, your file must still load this theme’s CSS and scripts (start from the theme’s partial), or use a merged directory instead.

```yaml
ui:
  bundle:
    url: https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/HEAD/raw/build/ui-bundle.zip?job=bundle-stable
    snapshot: true
  supplemental_files:
    - path: partials/head-meta.hbs
      contents: ./my-supplemental-ui/partials/head-meta.hbs
```

### Method 3: Pre-built UI bundle (no JavaScript toolchain)

```yaml
ui:
  bundle:
    url: https://github.com/antora-supplemental/antora-dark-theme/releases/latest/download/ui-bundle.zip
    snapshot: true
```

### Method 4: Copy `supplemental-ui` into your repo (vendor the theme)

Vendor or fork the theme assets by copying the `supplemental-ui` folder into your project, then:

```yaml
ui:
  bundle:
    url: https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/HEAD/raw/build/ui-bundle.zip?job=bundle-stable
    snapshot: true
  supplemental_files: ./supplemental-ui
```

## Features

- Dark mode toggle button (sun/moon icons)
- System preference detection
- Persistent preference via localStorage
- No flash of unstyled content (FOUC)
- Works with Antora Default UI — no fork required

## Documentation

Full documentation and live demo: [antora-supplemental.github.io/antora-dark-theme](https://antora-supplemental.github.io/antora-dark-theme)

For the full AsciiDoc guide (same content, more detail), see [README.adoc](https://github.com/antora-supplemental/antora-dark-theme/blob/main/README.adoc).

## License

[MIT](LICENSE)
