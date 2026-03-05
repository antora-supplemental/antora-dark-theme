# Antora Dark Theme

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Antora 3.x](https://img.shields.io/badge/antora-3.x-purple.svg)](https://antora.org)

Dark mode supplemental UI for [Antora](https://antora.org) documentation sites.

## Install

```bash
pnpm add -D github:antora-supplemental/antora-dark-theme
```

Then configure your `antora-playbook.yml`:

```yaml
ui:
  bundle:
    url: https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/HEAD/raw/build/ui-bundle.zip?job=bundle-stable
    snapshot: true
  supplemental_files: ./node_modules/antora-dark-theme/supplemental-ui
```

## Features

- Dark mode toggle button (sun/moon icons)
- System preference detection
- Persistent preference via localStorage
- No flash of unstyled content (FOUC)
- Works with Antora Default UI — no fork required

## Documentation

Full documentation and live demo: **https://devcentr.github.io/antora-dark-theme**

## License

[MIT](LICENSE)


