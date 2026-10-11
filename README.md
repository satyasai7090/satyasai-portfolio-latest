# Satya Sai Pasupuleti: technical writing portfolio

Source for **[satyasaiwork.online](https://satyasaiwork.online/)**, the portfolio of a senior technical writer and information architect.

The site itself is a documentation project. Every page is written in Markdown, organized by document type, versioned in Git, checked by a strict build on every change, and published automatically. That is the same docs-as-code workflow I use for product documentation.

## What's inside

| Section | Document type | Audience |
|---|---|---|
| [Case study](docs/case-studies/) | Problem, insight, solution and result for a publishing pipeline I built | Hiring managers, documentation leads |
| [API docs](docs/api-docs/) | REST API reference: endpoints, authentication, webhooks | Developers and integration engineers |
| [Guides](docs/guides/) | User guides, quick starts and a symptom-based knowledge base | End users, administrators, support engineers |
| [Release notes](docs/release-notes/) | Versioned release notes with upgrade steps and known issues | Administrators and enterprise customers |
| [Articles and video](docs/articles-and-video/) | A published article and a narrated product walkthrough | Writers, prospective users |

The products in the samples (Nexus MFT, CloudSuite CRM, HealthMate, PennyWise) are fictional. The writing is mine.

## How the content is organized

```text
docs/
├── index.md                      Home page
├── about.md                      About, experience and tools
├── case-studies/                 One page per case study
├── api-docs/
│   └── nexus-mft/                One folder per API: reference, authentication, webhooks
├── guides/
│   ├── *.md                      Single-page guides (summary page + downloadable PDF)
│   └── nexus-mft-knowledge-base/ Multi-article knowledge base
├── release-notes/
│   ├── cloudsuite-crm-3-12/      One folder per product version
│   └── nexus-mft-4-2/            overview → what's new → upgrade → known issues
├── articles-and-video/
└── assets/
    ├── images/                   Covers and case-study screenshots
    ├── downloads/                PDF versions of print-first guides
    ├── stylesheets/
    └── fonts/                    Self-hosted, SIL Open Font License
overrides/                        Theme templates (home page layout, page metadata)
mkdocs.yml                        Site settings and navigation
```

The principles behind the structure:

- **Organized by document type, not by product.** Readers arrive looking for an API reference or a set of release notes, so the top level matches the job the reader is doing.
- **One topic per page.** Multi-page sets (API, knowledge base, release notes) live in their own folder, with `index.md` as the entry point and pages in reading order.
- **Predictable names.** Lowercase, hyphen-separated file and folder names that match the page title, so every URL is readable and stable.
- **Assets separated from content.** Images, PDFs, styles and fonts sit under `assets/`, so content folders hold only pages.
- **Navigation defined in one place.** The order readers see is set in `mkdocs.yml`, not by file names.

Writing and formatting rules are in [STYLE_GUIDE.md](STYLE_GUIDE.md).

## Build and preview

Requires Python 3.10 or later.

```bash
pip install -r requirements.txt
mkdocs serve            # live preview at http://127.0.0.1:8000
mkdocs build --strict   # production build; fails on broken links or missing pages
```

## Publishing

- Every push to `main` is built by Netlify, which runs the command in `netlify.toml` and publishes the `site/` folder.
- Pull requests are checked by a GitHub Actions workflow (`.github/workflows/build.yml`), which runs the same strict build, so a broken link never reaches the live site.

## Built with

[MkDocs](https://www.mkdocs.org/) and [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/), with a custom theme. Hosted on [Netlify](https://www.netlify.com/).

© 2026 Satya Sai Pasupuleti
