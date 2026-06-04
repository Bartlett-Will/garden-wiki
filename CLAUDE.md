# Garden Wiki — Schema

A growing knowledge base built from podcast transcripts (primarily the Cannabis Cultivation and Science Podcast), structured using the LLM-wiki pattern. The wiki serves home gardeners — from complete beginners to those ready to go deep into the science. Cannabis is woven throughout as one important application, not a standalone section.

## Architecture

### Three layers

1. **Raw sources** (`raw/`) — immutable podcast transcripts and any future documents. The LLM reads from these but never modifies them.
2. **The wiki** (`wiki/`) — LLM-generated and LLM-maintained Obsidian-compatible markdown. The LLM owns this layer entirely.
3. **This schema** (`CLAUDE.md`) — conventions, structure, and workflows. Co-evolved by the human and LLM.

### Wiki structure

```
wiki/
├── index.md              # Content catalog — every page listed with summary
├── log.md                # Chronological record of ingests, queries, lint passes
├── science/              # THE WHY — concepts, biology, chemistry, physics
├── practice/             # THE HOW — techniques, methods, applied guidance
├── people/               # Guest experts — credentials, contributions, links
└── episodes/             # Episode summaries — one per source episode
```

**Science pages** explain the underlying principles: what silicon does in a plant cell, how the rhizophagy cycle works, why soil pH matters. Written so a beginner can follow but not afraid to go deep into the mechanisms.

**Practice pages** explain what to do: how to run a soil test, how to apply silicon, how to set up a lean workflow. Cross-linked heavily to the science pages that explain *why* each practice works.

**People pages** capture guest expert credentials, key contributions, and which episodes/concepts they appear in. Enables tracing claims back to authoritative sources.

**Episode pages** summarize each podcast episode with key takeaways, concepts covered, and links to the wiki pages that were created or updated from that episode.

### Cannabis integration

Cannabis-specific guidance is **woven into** relevant pages, not siloed. Use a consistent callout format:

```markdown
> [!cannabis] Cannabis Application
> Silicon supplementation is particularly valuable for cannabis because...
```

This keeps the wiki useful for all gardeners while highlighting cannabis-relevant details for those who need them.

## Page conventions

### Frontmatter

Every wiki page has YAML frontmatter:

```yaml
---
title: Silicon in Plants
aliases: [silica, silicon nutrition, plant silicon]
tags: [science, mineral-nutrition, plant-health]
sources: [ep-156]
created: 2026-06-04
updated: 2026-06-04
---
```

- `title`: human-readable page title
- `aliases`: alternative names for Obsidian search and linking
- `tags`: categorization. Use lowercase, hyphenated. Common prefixes: `science`, `practice`, `person`, `episode`
- `sources`: list of episode IDs (e.g., `ep-156`) that contribute to this page
- `created` / `updated`: ISO dates

### Cross-references

Use Obsidian `[[wikilinks]]` for all internal references:
- `[[silicon-in-plants]]` — link to a page
- `[[silicon-in-plants|silicon]]` — link with display text
- `[[dr-wendy-zellner]]` — link to a person page
- `[[ep-156-silicon-in-plant-health]]` — link to an episode page

### Page structure

Each page follows this skeleton:

```markdown
---
(frontmatter)
---

# Title

> **Quick take:** One-sentence summary a beginner can understand.

(Body — accessible opening paragraph, then progressively deeper sections)

> [!cannabis] Cannabis Application
> (Cannabis-specific notes, if relevant)

## Key Takeaways
- Bullet points of the most important ideas

## Sources
- [[ep-156-silicon-in-plant-health]] — Dr. Wendy Zellner on silicon's role in plant defense

## Related
- [[soil-food-web]] — how silicon interacts with microbial systems
- [[plant-stress-responses]] — broader context for abiotic stress resistance
```

### Naming conventions

- File names: lowercase, hyphenated, descriptive (`silicon-in-plants.md`, `lean-farming.md`)
- Episode files: `ep-{number}-{short-title}.md` (e.g., `ep-156-silicon-in-plant-health.md`)
- People files: name slug (`dr-wendy-zellner.md`, `ben-hartman.md`)

## Operations

### Ingest (conversational)

When processing one episode at a time with the human:

1. Read the transcript from `raw/transcripts/`
2. Discuss key takeaways with the human — what to emphasize, what surprised them
3. Create or update wiki pages:
   - Create the episode summary page in `wiki/episodes/`
   - Create or update people pages in `wiki/people/`
   - Create or update science pages in `wiki/science/`
   - Create or update practice pages in `wiki/practice/`
4. Update `wiki/index.md` with new/changed pages
5. Append an entry to `wiki/log.md`

### Ingest (batch)

When processing multiple episodes at once:

1. Read all transcripts from `raw/transcripts/`
2. For each episode, extract: key concepts, people, practical techniques, cannabis-specific notes
3. Create all new pages and update existing ones
4. Resolve cross-references across the batch (concepts that appear in multiple episodes)
5. Update `wiki/index.md` comprehensively
6. Append entries to `wiki/log.md` for each episode processed

### Query

When answering questions against the wiki:

1. Read `wiki/index.md` to find relevant pages
2. Read the relevant pages
3. Synthesize an answer with `[[citations]]` to wiki pages
4. If the answer is valuable and reusable, file it as a new wiki page (with human approval)

### Lint

Periodically health-check the wiki:

- **Contradictions**: claims on one page that conflict with another
- **Stale content**: claims that newer episodes have updated or corrected
- **Orphan pages**: pages with no inbound `[[links]]`
- **Missing pages**: `[[links]]` that point to pages that don't exist yet
- **Gaps**: important concepts mentioned but lacking their own page
- **Cross-reference quality**: pages that should link to each other but don't

## Tone and voice

- **Beginner-friendly first**: assume the reader might not know what a root hair is or why soil pH matters. Define terms on first use.
- **Then go deep**: after the accessible intro, don't shy away from the cellular biology, the chemistry, the research. The science is the point.
- **Practical**: always connect the science to what a gardener can actually do.
- **Honest about uncertainty**: when the podcast host or guests note that something is debated, still being researched, or often misunderstood — capture that nuance.
- **No hype**: avoid "miracle," "game-changer," "silver bullet" language (unless quoting a source, with context).

## Raw source reference

Transcripts live in `raw/transcripts/` and follow the naming pattern from the original podcast archive:
```
{episode-number}-{truncated-title}.txt
```

The Cannabis Cultivation and Science Podcast is hosted by Tad Hussey of KISS Organics. Episodes are conversations with expert guests spanning soil science, plant physiology, microbiology, farming systems, and cultivation practices. Cannabis is the primary crop context but the science applies broadly to all gardening and agriculture.
