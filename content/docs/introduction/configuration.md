---

title: Configuration
published: true
---

# Configuration

PlatformKit uses a **three-level configuration** system. Each level is a `platformkit.config.ts` file that exports a `PlatformKitConfig` object. Levels are deep-merged at build time with last-wins semantics.

## Config levels

| Level      | File                                      | Priority    |
| ---------- | ----------------------------------------- | ----------- |
| **System** | `platformkit.config.ts` (root)            | Lowest      |
| **Theme**  | `src/themes/<name>/platformkit.config.ts` | Medium      |
| **User**   | `src/overrides/platformkit.config.ts`     | **Highest** |

You almost never need to touch the system or theme configs. Put your overrides in `src/overrides/platformkit.config.ts`.

## Minimal example

```ts
import type { PlatformKitConfig } from "../../lib/config";

const config: PlatformKitConfig = {
  theme: "bento",
  contentCollections: {
    blog: {
      directory: "content/blog",
      format: "markdown",
      sortField: "date",
      sortOrder: "desc",
    },
  },
};

export default config;
```

## Key config options

### `theme`

The name of the active theme directory under `src/themes/`.

### `contentCollections`

A map of collection key → config. Each collection specifies:

| Option          | Type          | Description                                                      |
| --------------- | ------------- | ---------------------------------------------------------------- |
| `directory`     | `string`      | Path to the content source files                                 |
| `format`        | `"markdown" \ | "yaml" \                                                         | "json"` | File format |
| `sortField`     | `string`      | Field used to sort items                                         |
| `sortOrder`     | `"asc" \      | "desc"`                                                          | Sort direction |
| `recursive`     | `boolean`     | Enable nested subdirectory scanning (with `_meta.json` ordering) |
| `slugField`     | `string`      | Which field to derive the URL slug from                          |
| `fieldDefaults` | `Record`      | Default values for missing fields                                |
| `fieldRenames`  | `Record`      | Declarative field rename map                                     |
| `indexFilter`   | `function`    | Filter items out of the public index                             |

### `contentSchemas`

Defines the CMS editor UI for each collection using FormKit schemas. Controls what fields appear in the editor drawers.

### `buildHooks`

An array of build hook objects that run during the Vite build. Used for RSS feed generation, OG pre-rendering, TTS audio, image optimisation, and more.

### `pwa`

PWA manifest settings — `name`, `shortName`, `themeColor`, `backgroundColor`.

## Deep merge behaviour

- **Objects** are merged recursively (property by property).
- **`buildHooks` arrays** are concatenated across levels.
- **Scalar values** use last-wins (higher priority level overrides lower).

This means you can override a single field in the user config without duplicating the entire theme config.
