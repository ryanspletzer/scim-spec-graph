# SCIM Specification Graph

This repo is a curated dependency graph of the SCIM
(System for Cross-domain Identity Management) specifications and their
references.
It is documentation only — there is no build, no tests, and no application code.

## Layout

- `Graph.md` — the canonical artifact: a single Mermaid `graph TD` diagram of
  every tracked spec and its dependency edges, plus prose explaining the
  relationships and a recommended reading order.
- `README.md` — prose overview plus a categorized list of every spec that
  mirrors the nodes in `Graph.md`.
- `docs/motivation.md` — why this project exists.
- `docs/recommended-reading-order.md` — a curated learning path
  (intentionally a subset, not an exhaustive list).

## CLAUDE.md / AGENTS.md symlink pattern

`AGENTS.md` is the canonical instructions file.
`CLAUDE.md` is a symlink to it so Claude Code picks it up automatically while
other AGENTS.md-aware tools read the same content — one file to maintain.
Edit `AGENTS.md`; never replace the symlink with a divergent copy.

## Graph conventions

`Graph.md` is the source of truth. Each spec appears in **four** places that
must stay in sync:

1. **Node definition** — an `RFC<number>` node whose label embeds an
   `<a href>` link and a `<br/>`-separated title, in the Mermaid block,
   grouped under the matching `%% ...` comment.
2. **Class assignment** — a `class RFC<number> <category>` entry, where the
   category is one of the `classDef`s (`foundation`, `core`, `extension`).
3. **Dependency edges** (`A -->|"<label>"| B`, meaning "B builds upon /
   references A") under the `%% Dependencies` block.
4. **README** bullet under the matching `### ...` heading
   (`Core SCIM Suite`, `Extensions`).

Keep the prose sections in `Graph.md` (Legend, Relationships Explained,
Reading Order, Implementation Checklist) consistent with any node you add.

Node id conventions:

- Published RFCs: `RFC<number>` (e.g. `RFC9865`), label
  `"<a href='...'>RFC <number></a><br/><Title>"`.
- IETF drafts: descriptive PascalCase id (e.g. `SCIM_Events`), label ending
  in `(Draft)` for unfinished work.

URL conventions:

- RFCs → `https://www.rfc-editor.org/rfc/rfc<number>`.
- IETF drafts → pin to the **latest revision** you verified, e.g.
  `https://datatracker.ietf.org/doc/html/draft-ietf-scim-...-NN`.
  Prefer the adopted WG (`draft-ietf-scim-...`) document over a superseded
  individual draft.

After editing, sanity-check that every node has exactly one `class`
assignment and that no edge references an undefined node id.

## Adding a spec

Use the `add-spec` skill — it walks the four-place update plus reference
verification. The `spec-researcher` subagent fetches a spec's canonical title,
latest revision, and normative references so edges are wired correctly.
Always verify dependency edges against the actual specification text rather
than guessing.

## Markdown conventions

- All Markdown must pass `markdownlint-cli2`; fix issues, don't ask.
  Config lives in `.markdownlint.yaml`.
- Follow semantic line breaks in prose: start each sentence on a new line and
  break after major clauses. These breaks affect source/diffs only, never
  rendered output, and never break inside a hyphenated word.
- Do not reflow `Graph.md`'s Mermaid block to satisfy prose rules.
