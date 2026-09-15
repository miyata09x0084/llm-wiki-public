# LLM Wiki

A personal knowledge base built on [Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

**The LLM writes the wiki; the human only supplies sources and asks questions.**
Obsidian is the IDE, the LLM is the programmer, and the wiki is the codebase.

## Usage

### 1. Add sources

Drop articles, papers, notes, transcripts, etc. into `raw/` (Markdown preferred).

- [Obsidian Web Clipper](https://obsidian.md/clipper) makes it easy to save web articles as Markdown straight into `raw/`
- Put images in `raw/assets/` (already configured as Obsidian's attachment folder)

### 2. Ingest

Open this directory in Claude Code and run:

```
/ingest
```

Or just say "I put X in raw/, please ingest it."
The LLM summarizes the source → updates related pages → updates the index and log.

### 3. Ask questions

Just ask:

- "Summarize everything we have on X so far"
- "Compare A and B"

Good answers are saved to `wiki/answers/`, so knowledge compounds over time.

### 4. Periodic maintenance

```
/lint
```

Checks for contradictions, orphan pages, and information gaps.

## Browsing in Obsidian

Open this folder (`llm-wiki/`) as a vault.

- **Graph view** shows the overall shape of the wiki, hub pages, and orphan pages
- Assign a hotkey to Settings → Hotkeys → "Download attachments for current file" to save all images from a clipped article locally in one go

## Structure

| Path | Role | Written by |
|---|---|---|
| `raw/` | Immutable sources | Human |
| `wiki/` | Generated pages (index / log / sources / entities / concepts / topics / answers) | LLM |
| `CLAUDE.md` | Schema (operating rules for the LLM) | Both (updated by agreement) |

## Example: how knowledge about "Iekei ramen" grows

A single web research note (Iekei ramen shops in Nagoya) is broken down into pages with different roles and accumulates over time.

```
raw/Web research + Google Maps check: Iekei ramen in Nagoya.md   ← source placed by the human (immutable)
 │
 ├─ /ingest ────────────────────────────────────────
 │   ├─ wiki/sources/  summary of the research (one source = one page)
 │   ├─ wiki/concepts/ Iekei ramen — timeless knowledge (lineage taxonomy: direct-line, Ichi-kei, chain-style, ...)
 │   └─ wiki/topics/   Iekei ramen in Nagoya — evolving page (pilgrimage list, updated after every visit)
 │
 └─ Question: "What's the nutritional value of the soup?" ──────
     └─ wiki/answers/  Nagoya Iekei's clear soup and its nutrition (estimated comparison) — the answer becomes an asset too
```

- **Separating concepts (timeless) from topics (evolving)** keeps the lineage knowledge clean no matter how many tasting notes pile up
- Ask "Which Iekei shop do you recommend in Nagoya?" later, and the LLM answers by citing these pages.
  An answer that would have vanished in a chat log stays in `answers/`, and knowledge compounds

---

> This repository is a sanitized mirror of a private repository.
> `raw/` (original sources) and some non-public pages are not included.
