# Style guide

The conventions every page in this portfolio follows. Adding a new sample means following these rules.

## Files and folders

- Use lowercase, hyphen-separated names that match the page title, for example `healthmate-glucometer-quick-start.md`.
- Place each page under the folder for its document type: `api-docs/`, `guides/`, `release-notes/`, `case-studies/` or `articles-and-video/`.
- Give a multi-page set its own folder, with `index.md` as the entry page.
- Name release-note folders by product and version, with dots replaced by hyphens, for example `nexus-mft-4-2/`.
- Put images in `docs/assets/images/` and downloadable files in `docs/assets/downloads/`. Never store them next to pages.
- Add every new page to `nav` in `mkdocs.yml`. A page that isn't in the navigation is a page nobody finds.

## Front matter

Every page starts with three fields:

```yaml
---
title: Authentication and security        # navigation and browser tab
seo_title: "Nexus MFT API: Authentication | Satya Sai Pasupuleti"
description: "One sentence on what the reader will learn or do."   # search results and link previews
---
```

## Headings

- Use sentence case: "Generate an API key", not "Generate An API Key".
- Use one `#` heading per page, matching `title`.
- Start task headings with a verb: "Register a webhook", "Rotate your API keys".
- Write troubleshooting headings as the symptom the reader sees, quoting the exact error: `Transfer fails with a "Connection refused" error`.
- Don't skip heading levels.

## Writing

- Address the reader as "you", in the present tense and the active voice.
- Write one action per numbered step, with the expected result after it where the reader needs to confirm it.
- Format UI labels in bold (**Settings** > **Updates**). Format code, file names, commands and values as `code`.
- Put the condition before the instruction: "If you use OAuth2, register the new redirect URI."
- Write links that say where they go. Never use "click here".

## Admonitions

| Type | Use for |
|---|---|
| `!!! abstract` | The "About this sample" card at the top of each sample: audience, purpose, scope |
| `!!! note` | Context that helps but isn't needed to complete the task |
| `!!! warning` | Something that can cause errors, data loss or downtime if ignored |
| `!!! danger` | Safety risks to people (medical device content) |

Use them sparingly. If every paragraph is a note, nothing is.

## Before you commit

Run `mkdocs build --strict` and fix every warning. The same check runs on every pull request.
