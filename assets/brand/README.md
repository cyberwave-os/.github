# Cyberwave Brand Assets

This directory is the canonical source for Cyberwave branding used across GitHub repositories.

## Logo Assets

- `cyberwave-logo-black.svg` — cyan mark with a dark wordmark for light backgrounds
- `cyberwave-logo-white.svg` — cyan mark with a white wordmark for dark backgrounds
- `cyberwave-icon.svg` — standalone cyan Cyberwave mark
- `cyberwave-physical-ai-badge.svg` — custom Shields-style badge with the Cyberwave mark

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

## Custom Cyberwave Badge

[![Cyberwave Physical AI](./cyberwave-physical-ai-badge.svg)](https://cyberwave.com)

The recommended badge is generated in the Shields.io style and stored in this repository. This keeps the README URL short and avoids embedding the full Base64-encoded logo in every repository.

Use this Markdown for a clickable custom badge:

```markdown
[![Cyberwave Physical AI](https://raw.githubusercontent.com/cyberwave-os/.github/main/assets/brand/cyberwave-physical-ai-badge.svg)](https://cyberwave.com)
```

Or use it without a link:

```markdown
![Cyberwave Physical AI](https://raw.githubusercontent.com/cyberwave-os/.github/main/assets/brand/cyberwave-physical-ai-badge.svg)
```

### Generate It with Shields.io

[Shields.io supports custom logos](https://shields.io/docs/logos#custom-logos) by accepting a Base64-encoded SVG in the `logo` query parameter. It does not load a custom logo directly from a GitHub URL.

Use the standalone Cyberwave icon to regenerate the stored badge:

```bash
logo_base64=$(base64 < assets/brand/cyberwave-icon.svg | tr -d '\n')

curl --get \
  --data-urlencode "logo=data:image/svg+xml;base64,$logo_base64" \
  "https://img.shields.io/badge/Cyberwave-Physical_AI-black" \
  --output assets/brand/cyberwave-physical-ai-badge.svg
```

The resulting Shields URL is long because it contains the complete icon. Commit the generated SVG and reference its raw GitHub URL instead of copying that long URL into every README.

### Standard Shields.io Badge

If the Cyberwave icon is not required, use the shorter dynamic Shields.io badge:

```markdown
[![Cyberwave](https://img.shields.io/badge/Cyberwave-Physical_AI-black)](https://cyberwave.com)
```

The underscore in `Physical_AI` renders as a space.

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
