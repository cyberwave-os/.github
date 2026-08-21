# Cyberwave Brand Assets

This directory is the canonical source for Cyberwave branding used across GitHub repositories.

## Logo Assets

- `cyberwave-logo-black.svg` — cyan mark with a dark wordmark for light backgrounds
- `cyberwave-logo-white.svg` — cyan mark with a white wordmark for dark backgrounds

For a theme-aware logo in another Cyberwave repository, copy this markup into its `README.md`:

```html
<p align="center">
  <a href="https://cyberwave.com">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/cyberwave-os/.github/main/assets/brand/cyberwave-logo-white.svg">
      <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/cyberwave-os/.github/main/assets/brand/cyberwave-logo-black.svg">
      <img src="https://raw.githubusercontent.com/cyberwave-os/.github/main/assets/brand/cyberwave-logo-black.svg" alt="Cyberwave" width="240">
    </picture>
  </a>
</p>
```

## Shields.io Badge

[![Cyberwave](https://img.shields.io/badge/Cyberwave-Physical_AI-black)](https://cyberwave.com)

Use this Markdown for a clickable Cyberwave badge:

```markdown
[![Cyberwave](https://img.shields.io/badge/Cyberwave-Physical_AI-black)](https://cyberwave.com)
```

Or use the badge without a link:

```markdown
![Cyberwave](https://img.shields.io/badge/Cyberwave-Physical_AI-black)
```

Shields.io generates the badge dynamically, so no badge image needs to be downloaded or committed. The underscore in `Physical_AI` renders as a space.

### Add the Badge to a Repository

1. Add one of the snippets above to the repository's `README.md`.
2. Preview the README and verify that the badge links to `https://cyberwave.com`.
3. Commit the README change on a branch and open a pull request:

```bash
git switch -c docs/add-cyberwave-badge
git add -- README.md
git commit -m "docs: add Cyberwave badge"
git push -u origin docs/add-cyberwave-badge
gh pr create --base main --head docs/add-cyberwave-badge --draft
```

To customize the badge, use the [Shields.io badge builder](https://shields.io/badges/static-badge) and keep `Cyberwave` as the label.
