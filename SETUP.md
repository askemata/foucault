# Local Setup & Development

## Quick Start (No Installation Required)

Docsify requires no build step. Simply open `index.html` in your browser:

```bash
# Navigate to the project directory
cd /path/to/foucault-bibliography

# Open in your default browser
open index.html
# Or on Linux:
xdg-open index.html
```

The site will render with full search and all features.

## Local Server (Recommended)

For better development experience with file watching, use Docsify CLI:

```bash
# Install Node.js if not already installed
# Then install Docsify CLI globally:
npm install -g docsify-cli

# In the project directory, start a dev server:
docsify serve .
```

This will:
- Start a local server at `http://localhost:3000`
- Auto-reload when files change
- Show build errors in the console

## Project Structure

```
/
├── index.html              # Main entry point (Docsify config)
├── README.md               # Homepage content
├── _sidebar.md             # Navigation menu
├── keywords.md             # Keyword index
├── ABOUT.md                # About & contribution guidelines
├── CLAUDE.md               # AI assistant instructions
├── SETUP.md                # This file
│
├── content/                # Content directory
│   ├── histoire_de_la_folie.md
│   ├── les_mots_et_les_choses.md
│   ├── naissance_de_la_clinique.md
│   ├── l_archeologie_du_savoir.md
│   ├── surveiller_et_punir.md
│   ├── histoire_sexualite_vol1.md
│   └── [add more .md files here]
│
├── .github/
│   └── workflows/
│       └── deploy.yml      # GitHub Actions deployment config
│
├── .nojekyll               # Disables Jekyll for GitHub Pages
├── .gitignore              # Git ignore rules
├── package.json            # Node.js metadata (optional)
└── [other config files]
```

## Creating New Entries

1. **Create a new markdown file** in `/content/` with a descriptive slug:
   ```bash
   content/new_work_title.md
   ```

2. **Use this template:**
   ```markdown
   ---
   title: "Full Title of Work"
   author: "Author Name"
   type: primary | secondary
   date: "YYYY" or "YYYY-MM-DD"
   url: "https://example.com"
   ---

   # [Title]

   **Referência ABNT completa:**
   [Full citation with URL]

   ## Resumo
   [4 paragraphs of 3-5 sentences each]

   **Palavras-chave:** #keyword1 #keyword2 ... #foucault-primaria
   ```

3. **Update `_sidebar.md`** to add a link to your new entry
4. **Update `keywords.md`** to link any new keywords

5. **Test locally** before committing:
   ```bash
   # Start dev server
   docsify serve .
   
   # Open http://localhost:3000
   # Verify link works and content displays correctly
   ```

## Editing & Styling

### YAML Frontmatter
Each content file uses YAML frontmatter (between `---` delimiters):
- `title` — display title of the work
- `author` — author/creator name
- `type` — `primary` (Foucault's own works) or `secondary` (about Foucault)
- `date` — publication year or full date
- `url` — URL to the work (library, publisher, etc.)

The frontmatter is automatically:
- Injected into page `<head>` as Highwire meta tags (for Zotero)
- Used to generate RIS export button
- Removed from display (only body content shows)

### Markdown Formatting

All standard Markdown is supported:
```markdown
# Heading 1
## Heading 2
### Heading 3

**Bold text**
*Italic text*
[Link text](http://example.com)

- Bullet list
- Another item

1. Numbered list
2. Second item

> Blockquote

`inline code`

```code block```
```

### Keywords/Tags

Use hashtags in the "Palavras-chave" section:
```markdown
**Palavras-chave:** #foucault-primaria #knowledge #power #discipline
```

Make sure keywords:
1. Are defined in `/keywords.md`
2. Link back to relevant content
3. Use kebab-case (hyphens, no spaces)

## Deployment

### GitHub Pages (Automatic)

1. Push to GitHub (main or master branch)
2. GitHub Actions automatically deploys to GitHub Pages
3. Site becomes available at: `https://username.github.io/repo-name`

Check `.github/workflows/deploy.yml` for configuration details.

### Manual Deployment

To deploy to any static hosting (Netlify, Vercel, etc.):
1. Copy all files to the hosting service
2. Set root directory to `/`
3. No build step required

## Troubleshooting

### Search not working
- Ensure `_sidebar.md` links are correct
- Check browser console (F12) for errors
- Verify markdown file paths

### Sidebar not showing
- Verify `_sidebar.md` exists and is properly formatted
- Check `index.html` has `loadSidebar: true` in config

### Export button not working
- Ensure frontmatter is valid YAML
- Check browser console for JavaScript errors
- Verify `date` field follows YYYY or YYYY-MM-DD format

### Zotero import failing
- Verify Highwire meta tags in page source (browser Dev Tools)
- Check that `citation_title` and `citation_author` are populated
- Ensure `url` field in frontmatter is valid HTTP/HTTPS URL

## Tips & Best Practices

1. **Use docsify serve locally** — auto-reload makes editing faster
2. **Test before pushing** — verify links work and formatting displays correctly
3. **Keep summaries focused** — 4 paragraphs is a good length for accessibility
4. **Use existing keywords when possible** — adds to keyword index connections
5. **Date consistency** — use YYYY for year-only, YYYY-MM-DD for specific dates
6. **Link checks** — verify URLs are accessible and reference stable locations
7. **Mobile preview** — use browser dev tools to test responsive layout

## Additional Resources

- **Docsify Documentation:** https://docsify.js.org/
- **Markdown Guide:** https://www.markdownguide.org/
- **GitHub Pages Documentation:** https://docs.github.com/en/pages
- **Zotero API:** https://www.zotero.org/support/dev/web_api/v3/basics

---

Questions or issues? See `ABOUT.md` for contribution guidelines.
