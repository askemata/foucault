# About This Bibliography

## Project Overview

Michel Foucault's Bibliography is a digital, open-access collection of primary works by Michel Foucault and carefully selected secondary literature about his thought. The project aims to facilitate scholarly research and teaching by providing:

- Complete bibliographic information with multiple citation formats
- Summaries and keyword indexing for quick orientation
- Direct export to citation management software (Zotero, Mendeley, etc.)
- Full-text search across all descriptions and metadata

## Why This Project?

Foucault's work spans five decades and multiple languages (primarily French, with significant publication in English and other languages). His thought evolves significantly across his career—from early work on madness and medicine through archaeology and genealogy to late work on ethics and governmentality. Students and researchers benefit from a curated, organized introduction to this corpus.

This bibliography prioritizes accessibility without sacrificing rigor: each entry provides scholarly context while remaining approachable to newcomers.

## Technical Architecture

- **Static site generator:** [Docsify](https://docsify.js.org) — renders Markdown in real-time without build step
- **Hosting:** [GitHub Pages](https://pages.github.com) — free, version-controlled, deployable via GitHub Actions
- **Export formats:**
  - Highwire Press meta tags (for Zotero browser import)
  - RIS files (compatible with Zotero, Mendeley, EndNote, etc.)
- **Theming:** Responsive, light/dark mode aware CSS with Sphinx/Read the Docs aesthetic

## Adding New Entries

To add a new work to the bibliography:

1. Create a new file in `/content/` named `slug-of-title.md`
2. Use this template:

```markdown
---
title: "Full Title of Work"
author: "Author Name"
type: primary | secondary
date: "YYYY" or "YYYY-MM-DD"
url: "https://..."
---

# [Title]

**Referência ABNT completa:**
[Full citation]

## Resumo
[4 paragraphs]

**Palavras-chave:** #keyword1 #keyword2 ... #foucault-primaria
```

3. Update `_sidebar.md` to include a link to the new file
4. Update `keywords.md` to add any new keywords with back-links
5. Commit and push; GitHub Actions will deploy automatically

## Citation Metadata

Each entry includes structured metadata via two methods:

### 1. Highwire Press Meta Tags
Automatically injected into the page `<head>` when viewing an entry. Enables direct import into Zotero via browser button:
- `citation_title`
- `citation_author`
- `citation_publication_date`
- `citation_public_url`

### 2. RIS Export Button
"Export to Zotero" button on each page generates and downloads a `.ris` file compatible with:
- Zotero
- Mendeley
- EndNote
- BibDesk
- Citavi
- And most other reference managers

## Contributing

### Content Guidelines

- **Primary works:** Foucault's own publications, lectures, and interviews
- **Secondary literature:** Scholarly monographs, articles, dissertations, and edited collections analyzing Foucault
- **Summaries:** Clear, accurate, 4-paragraph format suitable for first-time readers and specialists alike
- **Keywords:** Use existing keywords when possible; create new ones sparingly and descriptively
- **Accuracy:** Double-check bibliographic information, dates, and citation formatting

### Code Contributions

Issues, pull requests, and suggestions are welcome. Please:

1. Test changes locally (site requires no build: simply open `index.html` in a browser)
2. Validate YAML frontmatter syntax in new `.md` files
3. Ensure keywords are linked in `keywords.md`
4. Update `_sidebar.md` for navigation

## License & Attribution

[To be determined by project maintainer]

## Credits

This project was built with:
- [Docsify](https://docsify.js.org) — lightweight documentation site generator
- [GitHub Pages](https://pages.github.com) — static site hosting
- [GitHub Actions](https://github.com/features/actions) — continuous deployment

---

Questions or suggestions? Open an issue or contact the project maintainer.
