---
title: Themes
published: true
---

# Themes

Themes control the visual layout, navigation, and component structure of your site. Each theme lives in its own directory under `src/themes/`.

## Theme directory structure

```
src/themes/bento/
├── Root.vue                # Main layout entry point
├── platformkit.config.ts   # Theme-level configuration
├── routes-manifest.ts      # Route definitions
├── package.json            # Theme-specific dependencies (optional)
├── TabNav.vue              # Tab navigation bar
├── DocsSection.vue         # Docs viewer
├── BlogSection.vue         # Blog list + detail
├── GallerySection.vue      # Gallery masonry grid
└── ...
```

## Creating a new theme

1. **Create the directory** — e.g. `src/themes/minimal/`
2. **Add `Root.vue`** — this is the entry point the framework renders.
3. **Add `platformkit.config.ts`** — declare which content collections, schemas, and build hooks your theme uses.
4. **Add `routes-manifest.ts`** — export an array of Vue Router route objects.
5. **Set the theme** — in `src/overrides/platformkit.config.ts`, set `theme: "minimal"`.

## Theme-specific dependencies

If your theme needs extra npm packages, create a `package.json` in the theme directory:

```json
{
  "name": "@themes/bento",
  "private": true,
  "dependencies": {
    "grid-layout-plus": "^1.1.1"
  }
}
```

Dependencies are installed automatically before `dev` and `build` by `scripts/install-layout-deps.mjs`. **Do not add theme deps to the root `package.json`.**

## CSS variables

Themes expose a set of CSS custom properties for colour, typography, and layout. Users can override these through the CMS theme editor.

### Core colour variables

| Variable | Description |
|----------|-------------|
| `--color-brand` | Primary brand colour |
| `--color-accent` | Accent / highlight colour |
| `--color-ink` | Main text colour |
| `--color-ink-soft` | Muted text colour |
| `--bg` | Page background |
| `--glass` / `--glass2` | Semi-transparent surfaces |
| `--card-bg` | Card background |
| `--card-border` | Card border colour |
| `--color-border` | General border colour |

### Bento-specific layout variables

| Variable | Default | Description |
|----------|---------|-------------|
| `--bento-grid-width` | `960px` | Max grid width |
| `--bento-gap` | `16px` | Gap between grid cells |
| `--bento-card-radius` | `20px` | Card border radius |
| `--bento-hover-scale` | `1.02` | Card hover zoom |

## Theme presets

Define light, dark, or custom presets by mapping preset names to CSS variable values. Users pick a preset in the CMS, or the theme can auto-switch based on `prefers-color-scheme`.

> **Tip:** Use CSS custom properties for all colours and spacing to make your theme easy to customise without code changes.