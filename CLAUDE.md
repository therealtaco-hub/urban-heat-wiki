# LLM Wiki Schema — Urban Heat Mapping

This file governs all behavior of the LLM wiki agent for this vault. Read it at the start of every session. All conventions defined here are authoritative.

---

## Role

You are the wiki agent for this Urban Heat Mapping knowledge base. Your job is to write and maintain all wiki files. The human curates sources, asks questions, and directs analysis. You do the filing, cross-referencing, summarizing, and maintenance. Never ask the human to do what you can do yourself.

---

## Directory Structure

```
/                          ← vault root
├── CLAUDE.md              ← this schema (agent instructions)
├── index.md               ← content catalog (LLM-maintained)
├── log.md                 ← append-only activity log (LLM-maintained)
│
├── raw/                   ← immutable source documents (human-curated)
│   ├── assets/            ← locally downloaded images from clipped articles
│   └── *.md               ← clipped articles, papers, reports, data notes
│
└── wiki/                  ← LLM-generated knowledge base
    ├── overview.md        ← high-level synthesis, evolving thesis
    ├── entities/          ← cities, regions, researchers, orgs, datasets, tools
    ├── concepts/          ← UHI mechanisms, mitigation strategies, metrics, methods
    └── sources/           ← one summary page per source in raw/
```

**Rules:**
- `raw/` is read-only. Never modify files there.
- `wiki/` is fully LLM-owned. Create, update, delete pages freely.
- Every file in `wiki/` must be reachable via a link from `index.md`.
- Page filenames: lowercase, hyphens for spaces. E.g. `urban-heat-island.md`, `london.md`.

---

## Page Conventions

### Frontmatter (YAML, required on all wiki pages)

```yaml
---
title: "Page Title"
type: concept | entity | source | overview
tags: [tag1, tag2]
sources: 0          # number of raw sources this page draws from
updated: YYYY-MM-DD
---
```

### Page types and their structure

**concept** — a mechanism, phenomenon, method, metric, or strategy
```
# Title
One-paragraph plain-English summary.

## Key Facts
- Bullet list of the most important, citable claims.

## Mechanisms / How It Works
## Evidence and Data
## Debates and Uncertainties
## Related Concepts
## Relevant Entities
## Sources
```

**entity** — a city, region, researcher, organization, dataset, or tool
```
# Title
One-line description.

## Overview
## Key Data / Stats
## Role in Urban Heat Research
## Connections
## Sources
```

**source** — summary of one raw document
```
# Source: [Short Title]
- **Type:** paper | article | report | dataset | book chapter
- **Author(s):**
- **Date:**
- **Raw file:** [[raw/filename]]

## Summary
2–4 paragraph synthesis.

## Key Claims
- Numbered list of claims that will propagate to other wiki pages.

## Data and Figures
Notable quantitative findings.

## Contradictions / Gaps
## Wiki Pages Updated
```

**overview** — the single `wiki/overview.md`, the evolving thesis
```
# Urban Heat Mapping — Overview
*Last updated: YYYY-MM-DD | Sources ingested: N*

## Current Synthesis
## Key Open Questions
## Strongest Evidence So Far
## Active Debates
## Next Sources to Find
```

---

## Workflows

### INGEST — adding a new source

When the human says "ingest [file]" or drops a source:

1. Read the raw source file.
2. Discuss key takeaways with the human (2–4 bullet points, ask if emphasis is right).
3. Create `wiki/sources/[slug].md` with the source summary page.
4. Identify all entity and concept pages this source touches.
   - Update existing pages: add claims, update data, flag contradictions.
   - Create new pages if an important entity or concept lacks one.
5. Update `wiki/overview.md`: revise synthesis, open questions, evidence strength.
6. Update `index.md`: add the new source page, update any entity/concept entries.
7. Append to `log.md`: `## [YYYY-MM-DD] ingest | [Source Title]`
8. Report back: list every wiki file created or updated, with a one-line note on what changed.

A single source should typically touch 5–15 wiki pages.

### QUERY — answering a question

When the human asks a question:

1. Read `index.md` to identify relevant pages.
2. Read those pages.
3. Synthesize an answer with inline wiki citations `[[page-name]]`.
4. Ask: "Should I file this answer as a wiki page?" If yes, save to `wiki/` under the appropriate type.
5. If the answer reveals a gap (missing page, stale claim, contradiction), flag it and offer to fix.

### LINT — wiki health check

When the human says "lint" or "health check":

1. Read all wiki pages via index.
2. Check for:
   - Contradictions between pages
   - Stale claims superseded by newer sources
   - Orphan pages (not linked from anywhere)
   - Important concepts mentioned but lacking their own page
   - Missing cross-references between related pages
   - Data gaps that could be filled by a web search
3. Produce a prioritized punch list of issues.
4. Ask which to fix now.

### UPDATE — revising wiki content

When the human asks to revise, correct, or expand a page:

1. Read the current page.
2. Make the change.
3. Update `updated:` frontmatter date.
4. Note the change in `log.md`.

---

## Cross-Referencing Rules

- Use `[[wiki/entities/city-name]]` style wikilinks throughout.
- Every concept page must link to at least one entity page where that concept is observed.
- Every entity page must link to all relevant concept pages.
- Every source page must list all wiki pages it contributed to under "## Wiki Pages Updated".
- When a new source contradicts an existing claim, mark the existing claim with `> [!warning] Contradicted by [[wiki/sources/new-source]]` and update the relevant section.

---

## Domain Vocabulary

Key terms to always create dedicated concept pages for if they appear:

- Urban Heat Island (UHI)
- Land Surface Temperature (LST)
- Air Temperature vs. Surface Temperature
- Albedo / Surface Reflectance
- Impervious Surface Coverage
- Green Infrastructure (parks, street trees, green roofs)
- Cool Roofs / Pavements
- Nocturnal Heat Retention
- UHI Intensity
- Remote Sensing (Landsat, MODIS, Sentinel)
- NDVI (Normalized Difference Vegetation Index)
- Thermal Infrared (TIR) Imagery
- Heat-Related Mortality / Morbidity
- Climate Equity / Environmental Justice
- Urban Morphology
- Canyon Effect

Key entity types for this domain:
- **Cities** — case study cities, ranked by UHI intensity when known
- **Researchers / Groups** — key authors, labs, institutions
- **Datasets** — Landsat, MODIS, ERA5, city-specific sensor networks
- **Tools / Models** — WRF, ENVI-met, SUHI models, GIS tools
- **Organizations** — C40, IPCC, EPA, local urban planning bodies

---

## Index and Log Conventions

**index.md** sections (in order):
1. Overview
2. Sources (one line per `wiki/sources/*.md`)
3. Concepts (one line per `wiki/concepts/*.md`)
4. Entities / Cities (one line per `wiki/entities/*.md`)
5. Other

Each line format: `- [[wiki/path/page]] — one-sentence description (N sources)`

**log.md** entry format:
```
## [YYYY-MM-DD] TYPE | Title
- Brief note on what was done.
- Files created or modified.
```
Types: `ingest`, `query`, `lint`, `update`, `setup`

---

## Behavioral Rules

- Never truncate or summarize wiki page updates — write the full content.
- Always update `index.md` and `log.md` as part of any workflow that changes wiki files.
- If unsure whether to create a new page or expand an existing one: create a new page and cross-link.
- Do not invent claims not supported by the sources. Mark speculative synthesis clearly with `> [!note] Synthesis — not yet sourced`.
- When the human adds a source without instruction, default to starting the INGEST workflow.
- At session start, read `index.md` and `log.md` to orient yourself before doing anything else.
