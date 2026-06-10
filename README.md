# Garden Wiki

A knowledge base for home gardeners, built from the **Cannabis Cultivation and Science Podcast** and structured using the [LLM-wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f). Organized in two halves — **Science** (the why) and **Practice** (the how) — with cannabis-specific guidance woven throughout.

🌱 **Read it here: https://bartlett-will.github.io/garden-wiki**

## How it works

- **`raw/transcripts/`** — immutable podcast transcripts (the source layer).
- **`content/`** — the wiki itself: LLM-generated, interlinked Obsidian-flavored markdown across `science/`, `practice/`, `people/`, and `episodes/`. Maintained by an LLM; you read it.
- **`CLAUDE.md`** — the schema: conventions and workflows for ingesting episodes and maintaining the wiki.

The site is published with [Quartz v5](https://quartz.jzhao.xyz/) and deployed to GitHub Pages automatically on every push to `v5`.

## Built with Quartz

This site runs on [Quartz](https://quartz.jzhao.xyz/), a tool for publishing [digital gardens](https://jzhao.xyz/posts/networked-thought) and notes as a website for free.
