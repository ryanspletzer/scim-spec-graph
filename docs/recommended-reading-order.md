# Recommended Reading Order for SCIM Specifications

Learning the SCIM (System for Cross-domain Identity Management) ecosystem is
far less daunting than other identity stacks — there are only a handful of core
specifications — but reading them in the right order still saves time.
This guide provides a recommended reading order based on practical learning
experience, starting with concepts and progressively moving into schema,
protocol, and extensions.

## Learning Philosophy

The approach recommended here is to **start with the concepts**
(RFC 7642), then learn **what the data looks like** (the schema, RFC 7643),
then **how to move it over the wire** (the protocol, RFC 7644),
and finally layer on **extensions** such as cursor-based pagination
(RFC 9865) once the foundations are solid.

## Phase 1: Concepts and Requirements

### 1. RFC 7642 — Definitions, Overview, Concepts, and Requirements

**Why start here:** It establishes the vocabulary and the "why" behind SCIM
before you hit any JSON or HTTP detail.

**What to focus on:**

- What SCIM is and the problem it solves.
- Key terminology (service provider, client, resources).
- Use cases and operational models (push/pull).
- The requirements that the schema and protocol satisfy.

**Don't worry about:** Wire-level detail — that comes next.

## Phase 2: The Data Model

### 2. RFC 7643 — Core Schema

**Why now:** With the concepts in hand, learn how SCIM represents identities.

**What to focus on:**

- The User and Group resource types and their attributes.
- Common attributes, multi-valued attributes, and the `meta` attribute.
- Schema extensions (e.g. the Enterprise User extension).
- The platform-neutral, JSON-based data model.

## Phase 3: The Protocol

### 3. RFC 7644 — Protocol

**Why now:** Now that you know what resources look like, learn how to create,
read, update, delete, and query them.

**What to focus on:**

- The RESTful resource endpoints and CRUD operations.
- `PATCH` semantics for partial updates.
- Filtering, sorting, and (index-based) pagination.
- Bulk operations and error handling.

## Phase 4: Extensions

### 4. RFC 9865 — Cursor-Based Pagination of SCIM Resources

**Why now:** With schema and protocol understood, add modern pagination for
large-scale deployments.

**What to focus on:**

- Why cursor-based pagination beats index-based paging at scale.
- The new query parameters it adds to the protocol.
- The attributes it adds to resource representations.
- Backward compatibility with existing implementations.

## Tips for Success

1. **Read concepts first:** RFC 7642 makes the later specs click into place.
2. **Keep schema and protocol side by side:** RFC 7644 constantly references
   RFC 7643.
3. **Use the specification graph:** The [main graph](../Graph.md) shows the
   dependencies between specs.
4. **Implement as you learn:** A minimal service provider solidifies the model
   fast.
5. **Treat specs as reference, not tutorials:** Skim first, deep-dive when
   implementing a specific feature.

## Conclusion

Learning SCIM is a short journey compared with most identity stacks.
Start with the concepts (RFC 7642),
learn the data model (RFC 7643),
master the protocol (RFC 7644),
then adopt extensions like cursor-based pagination (RFC 9865) as your scale
demands.

Happy learning!
