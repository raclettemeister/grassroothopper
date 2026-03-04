# AGENTS.md

## Cursor Cloud specific instructions

### Overview

This is a documentation + static website repo. There is **no backend, no database, no build step, no package manager, and no test suite**. The only runnable artifact is `website/index.html` — a single-file vanilla HTML/CSS/JS pitch deck deployed to GitHub Pages.

### Running the website locally

```
python3 -m http.server 8080 --directory website
```

Then open `http://localhost:8080/` in a browser. No build or install step is needed.

### Lint / Test / Build

- **Lint:** No linter is configured. HTML validation can be done manually or with an external tool if needed.
- **Tests:** No automated tests exist.
- **Build:** No build step. The site is static HTML served directly.

### Deployment

Pushes to `main` auto-deploy the `website/` directory to GitHub Pages via `.github/workflows/pages.yml`.

### Key files

- `SPEC.md` — source of truth for vision, principles, features, strategy
- `website/index.html` — the entire website in one file
- `.cursor/rules/` — project context and constraints for AI-assisted development
