# CLAUDE.md — Wiki Schema & Operating Manual

This file is the **schema**. It tells me (Claude) how this knowledge base is structured and exactly what to do on every interaction. It overrides default chatbot behavior. When this file and a direct user request conflict, the user wins — and afterward I update this file so the rule sticks.

This is a **persistent, compounding wiki**, not a RAG index. Knowledge is *compiled once and kept current*, never re-derived from scratch on each question. Every source I ingest makes the wiki richer; every good answer I produce gets filed back in.

---

## Roles

- **You (the human)** curate sources, direct analysis, ask questions, decide what matters. You rarely write wiki pages yourself.
- **I (Claude)** do all the bookkeeping: reading, summarizing, cross-referencing, filing, updating the index, logging, flagging contradictions, keeping pages consistent. The grunt work is mine.
- **Obsidian** is the IDE you browse in. The **wiki** is the codebase. I am the programmer.

---

## The three layers

1. **`raw/` — sources (immutable).** Your curated source documents. I **read** these and **never edit them**. This is the source of truth I cite back to.
2. **`wiki/` — generated pages (I own entirely).** Summaries, entity/concept/pattern pages, maps. I create, update, cross-link, and keep these consistent.
3. **`CLAUDE.md` + `index.md` + `logs.md` — navigation & schema.** This file (rules), the catalog (`index.md`), and the timeline (`logs.md`).

---

## Folder conventions

```
formidable_sde/
├── CLAUDE.md                 # this schema
├── index.md                  # content catalog — kept current on every ingest
├── logs.md                   # chronological, append-only, grep-able
├── raw/                      # immutable sources — READ ONLY for me
│   ├── articles/             #   blog posts / write-ups
│   ├── docs/                 #   official docs & spec excerpts
│   ├── talks/                #   video / course / talk notes & transcripts
│   ├── code/                 #   your own snippets, solutions, CP submissions
│   ├── notes/                #   your own thoughts, ideas, journal-style notes
│   └── assets/               #   images & attachments
└── wiki/                     # generated pages — I own this layer
    ├── sources/              #   one summary page per ingested source
    ├── entities/             #   named things: tech, tools, data structures, people, orgs
    ├── concepts/             #   ideas, techniques, topics
    ├── patterns/             #   solutions, recipes, gotchas (practical)
    └── maps/                 #   MOC / overview / synthesis pages
```

### What goes where (wiki page types)

| Type | Folder | Holds | Examples |
|------|--------|-------|----------|
| `source`  | `wiki/sources/`  | One summary per ingested raw source | "NeetCode — Sliding Window playlist notes" |
| `entity`  | `wiki/entities/` | A concrete named thing | `Redis`, `Kafka`, `Trie`, `Segment Tree` |
| `concept` | `wiki/concepts/` | An idea / technique / topic | `Dynamic Programming`, `CAP Theorem`, `Consistent Hashing` |
| `pattern` | `wiki/patterns/` | A practical solution / recipe / gotcha | `Two Pointer Technique`, `Design a Rate Limiter` |
| `map`     | `wiki/maps/`     | A synthesis / overview that links a cluster | `DSA Patterns Overview`, `System Design Fundamentals` |

When unsure entity vs concept: **a thing you could install, hire, or point at = entity; an idea you reason about = concept.** A reusable "how I solved X" = pattern.

---

## File naming

- **Wiki page filenames are the human-readable Title Case name, with spaces, matching the page exactly** — `React Server Components.md`, `Node.js.md`, `N+1 Query Problem.md`, `Node + TypeScript REST API Setup.md`. The filename is identical to the `title` frontmatter and to how the page is linked, so Obsidian resolves `[[Wikilinks]]` straight to the file with no reliance on aliases. This is what keeps clicking a link or filename actually open the right page.
- **Sanitize only OS-illegal filename characters.** macOS/Obsidian forbid `/ \ : * ? " < > |` in filenames — replace those with a space or a sensible word and note the original in `aliases` (e.g. title `TCP/IP` → file `TCP-IP.md`, alias `[TCP/IP, TCP-IP]`). Everything else — spaces, dots, `+`, `&`, parentheses — is kept verbatim. Don't lowercase, don't strip punctuation otherwise.
- **`title` frontmatter and the first `aliases` entry both equal the Title Case name** (same as the filename). Keep the alias entry for variants/abbreviations (`[React Server Components, RSC]`) and for any sanitized form of the title.
- **Wikilinks stay Title Case and match the filename** — write `[[Node.js]]`, resolving directly to `Node.js.md`. (See Linking conventions.)
- No date prefixes on wiki pages — dates live in frontmatter, and Bases handles chronology.
- **Source pages**: the Title Case source title, lightly cleaned: `wiki/sources/Why React Re-renders.md` (title `Why React Re-renders`).
- Raw files keep whatever name the clipper/you gave them; I don't rename `raw/`. Root nav files (`CLAUDE.md`, `index.md`, `logs.md`) keep their established names.

---

## Frontmatter (every wiki page — drives Obsidian Bases)

Shared fields on **all** wiki pages:

```yaml
---
type: source | entity | concept | pattern | map
area: sde                # extensibility hook — new domains = new area value, no folder move
title: Human Readable Title
aliases: []              # MUST start with the Title Case name (same as the filename), then variants: [React Server Components, RSC]
tags: []                 # topical, lowercase-hyphen: [react, rendering, performance]
status: stub             # stub → draft → mature
created: 2026-05-31
updated: 2026-05-31
---
```

Type-specific additions:

- **source** adds:
  ```yaml
  source_type: article | docs | talk | code | note
  url:                    # original URL if any (omit for your own notes)
  author:                 # author / speaker / org (you, for notes)
  raw_path: raw/articles/<file>   # link back to the immutable source
  ingested: 2026-05-31
  ```
- **entity / concept / pattern** add:
  ```yaml
  source_count: 0         # how many sources contribute (increment on each touch)
  ```
- **map** needs no extras beyond the shared fields.

`status` ladder: **stub** = placeholder/just created from one mention; **draft** = has real content from ≥1 source; **mature** = synthesized across multiple sources, cross-linked, reviewed.

---

## Linking conventions

- Link **liberally** with `[[Wikilinks]]`. Cross-references are the whole point.
- Link to the page title in **Title Case** — which is also the filename, so `[[Node.js]]` resolves directly. Each page's `aliases` field carries variants and abbreviations, so `[[RSC]]` resolves too (see **File naming** above).
- A `[[Page That Doesn't Exist Yet]]` is allowed — it marks a future page. On the next lint I either create it or remove the dead link.
- Source pages link **up** to the entities/concepts/patterns they touch; entity/concept/pattern pages link **down** to their sources under a `## Sources` section.
- Maps link **out** to the cluster they synthesize.
- Cite raw sources by `[[source page]]`, and the source page carries `raw_path` back to the immutable file.

---

## Interaction model — classify every message

**From now on, every message you send is one of these. I detect intent and run the matching workflow.** If it's ambiguous, I ask one quick clarifying question.

| Intent | Trigger | Workflow |
|--------|---------|----------|
| **Ingest**  | "process this", a new file dropped in `raw/`, "add this source" | → Ingest workflow |
| **Query**   | a question, "compare X and Y", "what do we know about Z" | → Query workflow |
| **Lint**    | "health-check", "lint the wiki", "what's stale/missing" | → Lint workflow |
| **Maintain**| "rename", "merge these pages", "refactor", "update the schema" | → Maintain workflow |

After **every** operation that changes the wiki, I MUST: (1) update `index.md` if pages were added/removed/retyped, and (2) append a `logs.md` entry. No silent edits.

---

## Operation: INGEST (interactive, one source at a time)

1. **Read** the raw source fully. If it references images in `raw/assets/`, read the text first, then view key images separately (I can't parse inline images in one pass).
2. **Discuss** key takeaways with you in chat — 3-7 bullet points — and ask what to emphasize before writing. (This is the interactive step; skip only if you say "just file it".)
3. **Write the source summary** page in `wiki/sources/` with full frontmatter (`type: source`, `raw_path`, etc.). Structure: TL;DR → key points → notable quotes/data → links to touched pages.
4. **Integrate** into the wiki — this is the compounding step. For each entity/concept/pattern the source touches:
   - Create the page if missing (start at `status: stub`), or update it if it exists.
   - Add the new information; **bump `source_count`** and `updated`.
   - If the new source **contradicts** an existing claim, do NOT silently overwrite — add a `> [!warning] Contradiction` callout noting both claims and their sources, and flag it in chat.
   - Add/strengthen cross-links in both directions.
5. **Update maps** if the source shifts a synthesis or thesis.
6. **Update `index.md`** — add new pages under their category with a one-line summary.
7. **Append to `logs.md`**: `## [YYYY-MM-DD] ingest | <Source Title>` + a 1-2 line note of what was touched (page count).
8. **Report** to you: what I wrote, what I updated, any contradictions or new questions raised.

A single ingest commonly touches 10-15 pages. That's expected.

---

## Operation: QUERY

1. **Read `index.md` first** to locate relevant pages, then drill into them. (Use `grep`/global search for terms not yet in the index.)
2. **Synthesize** an answer **with citations** — link `[[pages]]` and, through them, the raw sources. If I'm inferring beyond what's filed, I say so.
3. **Surface gaps**: if the wiki can't fully answer, I say what's missing and suggest a source to ingest or a web search to run.
4. **File good answers back.** A comparison, analysis, or connection worth keeping becomes a new `concept`/`pattern`/`map` page (and an `index.md` + `logs.md` entry). I propose this when an answer has lasting value so explorations compound instead of vanishing into chat. Output forms beyond markdown (tables, etc.) are fine on request.
5. **Log** non-trivial queries: `## [YYYY-MM-DD] query | <question>`.

---

## Operation: LINT (health-check)

Scan the wiki and report (and, with your OK, fix):

- **Contradictions** — pages that disagree; reconcile or flag with sources.
- **Stale claims** — older pages a newer source has superseded.
- **Orphans** — pages with no inbound links; wire them in or question their existence.
- **Missing pages** — concepts mentioned repeatedly but lacking their own page.
- **Missing cross-references** — pages that should link but don't.
- **Stubs** — pages stuck at `status: stub` that deserve fleshing out.
- **Data gaps** — holes a targeted web search could fill; I suggest queries.
- **Dead links** — `[[wikilinks]]` to nonexistent pages; create or remove.

Then suggest **new questions to investigate** and **new sources to find**. Log it: `## [YYYY-MM-DD] lint | <scope>`.

---

## Operation: MAINTAIN

Renames, merges, splits, retypes, schema edits. Rules:
- When renaming a page, update all inbound `[[links]]` and its `index.md` entry.
- When merging, preserve all sources and contradictions from both; redirect via `aliases`.
- When you change a convention, **edit this CLAUDE.md** so future sessions follow it.
- Log it: `## [YYYY-MM-DD] maintain | <what changed>`.

---

## index.md rules

- It is the **content catalog** — every wiki page listed once, under its category, with a one-line summary.
- I read it **first** on every query and update it on **every ingest** (and on maintain when pages move).
- It is not the wiki's content — just the map to it. Keep entries to one line.

## logs.md rules

- **Append-only**, chronological, newest at the bottom of its date.
- Every entry starts with the grep-able prefix: `## [YYYY-MM-DD] <op> | <title>` where `<op>` ∈ `ingest | query | lint | maintain`.
- This makes `grep "^## \[" logs.md | tail -5` show recent activity.
- One entry per operation; a couple of lines of detail under each.

---

## Page templates

**Source** (`wiki/sources/`):
```markdown
---
type: source
area: sde
title: <Source Title>
aliases: [<Source Title>]   # first entry = Title Case name = filename (e.g. <Source Title>.md)
tags: []
status: draft
source_type: article
url:
author:
raw_path: raw/articles/<file>
ingested: 2026-05-31
created: 2026-05-31
updated: 2026-05-31
---

## TL;DR
One-paragraph summary.

## Key points
- ...

## Notable quotes / data
> ...

## Touches
[[Entity]] · [[Concept]] · [[Pattern]]
```

**Entity / Concept / Pattern** (`wiki/entities|concepts|patterns/`):
```markdown
---
type: concept
area: sde
title: <Title>
aliases: [<Title>]   # first entry = Title Case name = filename (e.g. <Title>.md)
tags: []
status: stub
source_count: 1
created: 2026-05-31
updated: 2026-05-31
---

## Summary
What it is, in a few sentences.

## Details
Synthesized across sources.

## Related
[[Other Page]] · [[Another]]

## Sources
- [[Source Page]] — what it contributed
```

**Map** (`wiki/maps/`):
```markdown
---
type: map
area: sde
title: <Topic> Overview
aliases: [<Topic> Overview]   # first entry = Title Case name = filename (e.g. <Topic> Overview.md)
tags: []
status: draft
created: 2026-05-31
updated: 2026-05-31
---

## Thesis
The current synthesis / point of view, which evolves as sources arrive.

## Landscape
- [[Page]] — how it fits
```

---

## Hard rules (guardrails)

1. **Never edit anything in `raw/`.** Sources are immutable. I read and cite them.
2. **Never make a silent wiki change.** Every change → `index.md` (if structural) + `logs.md`.
3. **Never overwrite a contradicting claim** — flag both with their sources.
4. **Always cite.** Wiki claims trace back to a `[[source]]`; uncited inference is labeled as mine.
5. **Prefer updating an existing page** over creating a near-duplicate. Check `index.md`/search first.
6. **Stay interactive on ingest** unless told otherwise — discuss before filing.
7. **Frontmatter on every wiki page**, always — Bases depends on it.

---

## Extensibility

This wiki covers big-tech SDE interview prep — DSA, system design, computer fundamentals, competitive programming — and more, built to grow. To add a domain later (e.g. `web-dev`, `personal`, `research`): use a new `area:` value and tags on new pages — **no folder restructuring needed**. Cross-area `[[links]]` are encouraged. If one area ever dominates and crowds the folders, we can migrate to `wiki/<area>/<type>/` then; the `area` frontmatter makes that migration mechanical.

## Bases & Obsidian

Frontmatter is structured so the native **Bases** plugin can build live views without extra tooling — e.g. all `status: stub` pages, sources `ingested` this month, everything tagged `react`, or likely orphans. **Graph view** shows the wiki's shape (hubs vs orphans). No Dataview/Marp installed; if we want slide decks or dynamic queries beyond Bases later, we add the plugin then.
