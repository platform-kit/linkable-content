---

title: Blog
published: true
---

# Blog

The blog collection powers a full-featured article system with Markdown authoring, cover images, tags, RSS, and optional text-to-speech audio.

## Writing a post

Create a Markdown file in `content/blog/`:

```markdown
---
title: My First Post
date: "2025-06-15"
excerpt: A short summary for listing pages.
tags: ["announcement", "guide"]
coverImage: /content/uploads/hero.avif
published: true
---

# My First Post

Write your article content here using standard Markdown.

## Code blocks

Fenced code blocks are syntax-highlighted automatically:

\`\`\`js
console.log("Hello from PlatformKit!");
\`\`\`
```

## Frontmatter fields

| Field            | Type       | Required | Description                                 |
| ---------------- | ---------- | -------- | ------------------------------------------- |
| `title`          | `string`   | Yes      | Article title                               |
| `date`           | `string`   | Yes      | ISO date (`YYYY-MM-DD`)                     |
| `slug`           | `string`   | No       | URL slug (derived from filename if omitted) |
| `excerpt`        | `string`   | No       | Short summary for cards / RSS               |
| `tags`           | `string[]` | No       | Categorisation tags                         |
| `coverImage`     | `string`   | No       | URL to a cover image                        |
| `published`      | `boolean`  | No       | Set `false` to hide from the index          |
| `expirationDate` | `string`   | No       | ISO date after which the post is hidden     |
| `rss`            | `boolean`  | No       | Set `false` to exclude from the RSS feed    |
| `audio`          | `string`   | No       | Path to an audio file for in-post playback  |

## RSS feed

An RSS 2.0 feed is generated automatically at `public/content/rss.xml` during build. It includes all published posts unless individually excluded with `rss: false`.

## Open Graph pre-rendering

PlatformKit can generate per-post HTML shells at build time so that social media crawlers see proper OG tags (title, description, image) without JavaScript.

This is enabled via a build hook in the theme config and produces static `.html` files alongside the JSON output.

## Text-to-speech

The TTS build hook can automatically generate MP3 audio from post content. When audio is available, an inline audio player appears at the top of the article.

## CMS editing

In the CMS, click **Blog** → **New Post** to open the editor. The editor provides:

- A Markdown / rich-text writing area (powered by TipTap)
- Cover image upload
- Tag management
- Publish / schedule controls
- Live preview