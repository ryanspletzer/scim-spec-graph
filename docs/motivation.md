# Motivation

## The Problem: Specification Sprawl

When learning about or implementing SCIM
(System for Cross-domain Identity Management),
you quickly encounter a common challenge: **specification sprawl**.

### The Tab Explosion

Here's what typically happens:

1. You start reading the
   [SCIM Protocol (RFC 7644)](https://www.rfc-editor.org/rfc/rfc7644)
   specification.
2. It constantly references the
   [SCIM Core Schema (RFC 7643)](https://www.rfc-editor.org/rfc/rfc7643),
   so you open that in a new tab.
3. Both lean on the concepts and requirements defined in
   [RFC 7642](https://www.rfc-editor.org/rfc/rfc7642),
   so that's another tab.
4. You want efficient paging for a large directory, so you reach for
   [Cursor-Based Pagination (RFC 9865)](https://www.rfc-editor.org/rfc/rfc9865),
   which updates both the schema and the protocol.
5. Before you know it, you have several tabs open and you've lost track of:
   - Which specifications you still need to read.
   - How they all relate to each other.
   - Which ones are foundational vs. optional extensions.
   - Where to start and in what order to read them.

### The Mental Load

Even experienced engineers struggle with:

- **Understanding dependencies**: Which specs build on which foundations?
- **Finding the right spec**: Need cursor pagination? Where does that fit in?
- **Avoiding missing pieces**: Did you consider every relevant spec for your
  use case?
- **Teaching others**: How do you explain this ecosystem to a teammate?

## The Solution: Visual Specification Mapping

This project exists to solve these problems by providing a **visual dependency
graph** that shows:

1. **All major specifications** in the SCIM ecosystem.
2. **Their relationships** — which specs depend on or reference others.
3. **Logical groupings** — conceptual foundation, core schema and protocol,
   and extensions.
4. **Direct links** — click any node to jump straight to the official
   specification.

## Who This Helps

### Developers

- **Learning**: Understand the identity-provisioning landscape before diving
  deep.
- **Implementation planning**: Identify which specifications you need for your
  use case.
- **Debugging**: When something goes wrong, trace through the relevant specs
  systematically.

### Identity Architects

- **Design decisions**: See the full picture when choosing which standards to
  support.
- **Gap analysis**: Ensure you haven't missed an important related spec.
- **Documentation**: Use the graph as a reference when documenting your
  provisioning architecture.

### Students and Educators

- **Teaching tool**: Show the relationships between specifications visually.
- **Study guide**: Know which specs to read and in what order.
- **Context building**: Understand how cross-domain identity provisioning fits
  together.

## How It Works

Instead of getting lost in a maze of specification tabs, you can:

1. **Start with the graph** to see the big picture.
2. **Identify your path** based on what you're trying to accomplish.
3. **Follow dependencies** to understand what foundational knowledge you need.
4. **Click through** to the official specs when you're ready to read the
   details.

## Example Use Cases

### "I need to implement a SCIM service provider"

Look at the graph and see that you'll need to understand:

- RFC 7642 — the concepts, use cases, and requirements.
- RFC 7643 — the User and Group schemas your resources must match.
- RFC 7644 — the RESTful protocol, filtering, and operations to expose.
- Possibly RFC 9865 — cursor-based pagination for large directories.

### "Why won't my big query page efficiently?"

The graph shows that RFC 9865 updates both the schema (RFC 7643) and the
protocol (RFC 7644) to add cursor-based pagination as an alternative to
index-based pagination — so both layers need support.

---

**Bottom line**: This project exists because understanding SCIM and its related
specifications shouldn't require a PhD in browser-tab management. Sometimes the
best way to understand complexity is to visualize it.
