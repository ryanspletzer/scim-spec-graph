---
name: add-spec
description: >-
  Add a new specification (RFC or IETF draft) to the SCIM dependency graph.
  Use whenever the user wants to add or update a spec in Graph.md — handles the
  four-place sync (node, class, edges, README) and verifies references against
  the source document.
---

# Add a spec to the graph

`Graph.md` is the source of truth; `README.md` mirrors it. A spec lives in
**four** places that must stay in sync. Do all four for every spec.

## 1. Research the spec (do not guess)

Delegate to the `spec-researcher` subagent (or fetch the rfc-editor.org /
datatracker page yourself) to obtain:

- canonical **title**,
- latest **revision** number (for drafts),
- canonical **URL**,
- the **normative references** (and `Updates` relationships) to specs already
  in the graph.

Edges must reflect what the document actually references — confirm against the
spec text, not memory.

## 2. Pick id, label, class, and grouping

- RFCs: id `RFC<number>`, label
  `"<a href='<url>'>RFC <number></a><br/><Title>"`.
- Drafts: descriptive PascalCase id (e.g. `SCIM_Events`); label ends in
  `(Draft)` if unfinished.
- Choose the `classDef` category that fits: `foundation` (concepts and
  requirements), `core` (schema and protocol), or `extension` (everything
  built on top).

If the spec already exists, this may be an **update** (e.g. bump a draft to a
newer revision) — edit in place instead of adding a duplicate node.

## 3. Edit `Graph.md` (Mermaid block)

1. **Node** — add the `RFC<number>["..."]` line under the matching `%% ...`
   comment.
2. **Class** — add `class RFC<number> <category>` in the styling section.
3. **Edges** — add `Dep -->|"<label>"| RFC<number>` lines under the
   `%% Dependencies` block, one per normative dependency that exists in the
   graph.

Also update the prose sections (Legend, Relationships Explained, Reading
Order, Implementation Checklist) if the new spec changes them.

## 4. Edit `README.md`

Add a bullet under the matching `### ...` category heading
(`Core SCIM Suite` or `Extensions`) describing the spec in one sentence,
consistent with the existing entries.

## 5. Verify

- Every node has exactly one `class` assignment.
- No edge references an undefined node id.
- Run the markdown linter (`mdlinter` skill or `markdownlint-cli2`) and fix.
