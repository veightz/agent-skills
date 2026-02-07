# Claude Compatibility Guide

This repository's `SKILL.md` format is designed for Codex.  
For Claude, use this file as the task contract and run the same scripts/resources.

## Scope

Use this workflow when the user asks to import a web article into Obsidian and wants:
- original source URL recorded
- collected date recorded
- source/author metadata (if available)
- key images localized into `attachments/` when possible

## Inputs

- Required: article URL
- Optional:
  - target note filename
  - target note directory
  - image mode: `key-only` (default) or `full`

## Output Requirements

Create/update one Obsidian Markdown note that includes:
- source URL
- collected date (absolute date)
- source name and author (if found)
- structured summary (conclusion, key points, next steps)
- image archive section (local path list + failed external links)

## Suggested Prompt for Claude

Use this prompt in Claude projects/chats:

```text
Import this article into my Obsidian vault and structure it as an analysis note.
Requirements:
1) Keep original URL and collected date.
2) Extract source and author when available.
3) Localize key images into attachments/ when possible, then reference local paths.
4) If an image cannot be downloaded, keep external URL and mark it as pending archival.
5) Provide conclusion, key points, and actionable next steps.
URL: <ARTICLE_URL>
```

## Shared Script (with uv)

From installed skill directory:

```bash
cd ~/.codex/skills/obsidian-article-import
uv run python scripts/download_images.py --help
```

Example:

```bash
uv run python scripts/download_images.py \
  --urls-file /tmp/img_urls.txt \
  --out-dir attachments \
  --prefix article-2026-02-07
```

## Notes

- Claude can reuse `scripts/` and `references/`.
- Codex auto-trigger behavior from `SKILL.md` does not apply to Claude.
