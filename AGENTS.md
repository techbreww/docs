# Documentation project instructions

## About this project

- This is the documentation site for [BrewBot Dashboard](https://brewbot.techbrew.dev), a Discord bot management platform
- Built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`
- Run `mint dev` to preview locally
- Run `mint broken-links` to check links

## Terminology

- Use "server" not "guild"
- Use "member" not "user" (when referring to Discord server members)
- Use "dashboard" not "portal"
- Use "bot" not "client"
- Use "premium" not "paid" or "pro"
- Use "free" not "basic" or "starter"

## Style preferences

- Use active voice and second person ("you")
- Keep sentences concise — one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references
- Use `<Note>` for supplementary info, `<Warning>` for destructive actions, `<Tip>` for best practices

## Content boundaries

- Do not document super-admin internals (internal tool, not user-facing)
- Do not include API keys, tokens, or secrets in examples
- Mark UI instructions with a TODO comment when screenshots are unavailable:
  ```mdx
  {/* TODO: Add screenshot of [feature] UI */}
  ```
- Features are split into free and premium tiers — always note which tier a feature belongs to
- The dashboard URL is `https://brewbot.techbrew.dev`
- The Discord support server is `https://discord.gg/WbMUYr7DCg`
