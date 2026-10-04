# BrewBot documentation

User documentation for [BrewBot](https://brewbot.gg), built with Mintlify. Pages are MDX; `docs.json` defines navigation. Follow [AGENTS.md](AGENTS.md) for terminology and content boundaries.

## Preview and validate

From this repository:

```bash
npx mint dev
npx mint broken-links
npx mint validate
```

## Keep features current

Compare documentation against the BrewBot app's dashboard navigation, feature pages, API validation, subscription guards, and bot handlers. Verify user-visible behavior rather than treating every database field or navigation description as a completed feature.

The [feature audit](FEATURE_AUDIT.md) maps the October 2026 review to source files and records unresolved implementation gaps. New pages need a navigation entry and a tier/access statement. Preserve existing page URLs when possible.

Use root-relative links without file extensions inside published pages. Add screenshot TODOs when UI screenshots are not available. Do not document internal administration or publish secrets.

## Publishing

Review changes before pushing to the repository's connected deployment branch. Mintlify deployment settings determine when changes go live.
