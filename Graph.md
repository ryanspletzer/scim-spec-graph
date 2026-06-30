# SCIM Specification Dependency Graph

This graph visualizes the relationships and dependencies between SCIM specifications.

```mermaid
graph TD
    %% Core SCIM Foundation
    RFC7642["<a href='https://www.rfc-editor.org/rfc/rfc7642'>RFC 7642</a><br/>SCIM: Definitions, Overview,<br/>Concepts, and Requirements"]
    
    %% SCIM Schema
    RFC7643["<a href='https://www.rfc-editor.org/rfc/rfc7643'>RFC 7643</a><br/>SCIM: Core Schema<br/>(User & Group Resources)"]
    
    %% SCIM Protocol
    RFC7644["<a href='https://www.rfc-editor.org/rfc/rfc7644'>RFC 7644</a><br/>SCIM: Protocol<br/>(RESTful HTTP API)"]
    
    %% Pagination Extension
    RFC9865["<a href='https://www.rfc-editor.org/rfc/rfc9865'>RFC 9865</a><br/>Cursor-Based Pagination<br/>of SCIM Resources"]
    
    %% Security Event Token Profile Extension
    RFC9967["<a href='https://www.rfc-editor.org/rfc/rfc9967'>RFC 9967</a><br/>SCIM Profile for<br/>Security Event Tokens (SETs)"]
    
    %% Agentic Identity Extension (Draft)
    SCIM_AgentSchema["<a href='https://datatracker.ietf.org/doc/html/draft-wahl-scim-agent-schema-01'>draft-wahl-scim-agent-schema-01</a><br/>SCIM: Agentic Identity Schema<br/>(Draft)"]
    
    %% Styling
    classDef foundation fill:#e1f5ff,stroke:#01579b,stroke-width:2px
    classDef core fill:#fff9c4,stroke:#f57f17,stroke-width:2px
    classDef extension fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    
    class RFC7642 foundation
    class RFC7643,RFC7644 core
    class RFC9865 extension
    class RFC9967 extension
    class SCIM_AgentSchema extension
    
    %% Dependencies
    %% Conceptual foundation (dotted): RFC 7642 is informative context, not a
    %% normative reference of the schema or protocol.
    RFC7642 -.->|"Concepts and<br/>requirements"| RFC7643
    RFC7642 -.->|"Concepts and<br/>requirements"| RFC7644
    %% Normative references (solid): edge points from the referenced spec to the
    %% spec that normatively references it.
    RFC7643 -->|"Schemas used by"| RFC7644
    RFC7644 -->|"Protocol cited by"| RFC7643
    RFC7643 -->|"Updates with<br/>pagination attributes"| RFC9865
    RFC7644 -->|"Updates with<br/>pagination support"| RFC9865
    RFC7643 -->|"Updates with<br/>SET schema attributes"| RFC9967
    RFC7644 -->|"Updates with<br/>async SET signaling"| RFC9967
    RFC7643 -->|"Extends with<br/>agent resource schema"| SCIM_AgentSchema
    RFC7644 -->|"Provisions agents<br/>via SCIM protocol"| SCIM_AgentSchema
```

## Legend

Node colors:

- **Blue (Foundation)**: Conceptual foundation - defines terminology, requirements, and use cases
- **Yellow (Core)**: Core technical specifications - schema and protocol definitions
- **Purple (Extension)**: Extensions and enhancements to core specifications

Edge styles:

- **Solid arrow** (`-->`): a **normative** reference - the target spec normatively references (builds upon) the source spec
- **Dotted arrow** (`-.->`): a **conceptual** link only - RFC 7642 is informative context that the schema and protocol satisfy, but neither normatively references it

## Relationships Explained

### RFC 7642 ⋯ RFC 7643 & RFC 7644 (conceptual only)

RFC 7642 is the conceptual foundation that establishes:

- What SCIM is and why it exists
- Key terminology and definitions
- Use cases and requirements
- Operational models (push/pull)

The schema (RFC 7643) and protocol (RFC 7644) satisfy these requirements,
so RFC 7642 is the natural starting point for a reader.
This link is **conceptual, not normative**, though:
neither RFC 7643 nor RFC 7644 lists RFC 7642 as a reference,
and RFC 7642 (an Informational document) cites them only informatively.
The graph therefore draws these two edges dotted.

### RFC 7643 ↔ RFC 7644 (mutual normative reference)

The schema and protocol reference each other normatively, so the graph draws
an edge in **both** directions:

- RFC 7644 normatively references RFC 7643 — the protocol defines how to
  manipulate resources whose shape the schema defines.
- RFC 7643 normatively references RFC 7644 — the core schema cites the
  protocol for how its resources are exchanged.
- You need both together: the schema says what resources look like, the
  protocol says how to create, read, update, and query them.

### RFC 7643 & RFC 7644 → RFC 9865

RFC 9865 extends both the schema and protocol:

- Adds new query parameters to the protocol
- Adds new attributes to resource representations in the schema
- Provides cursor-based pagination as an alternative to index-based pagination
- Maintains backward compatibility with existing implementations

### RFC 7643 & RFC 7644 → RFC 9967

RFC 9967 profiles SCIM resource changes as Security Event Tokens (SETs) and
formally `Updates` both the schema and protocol:

- Updates RFC 7643 with new `ServiceProviderConfig` attributes that advertise
  the SET profile
- Updates RFC 7644 with an optional asynchronous SCIM request capability
- Lets SCIM create/modify/delete/activate events be signaled between domains
- The underlying Security Event Token (SET) RFCs are intentionally out of
  scope for this graph

### RFC 7643 & RFC 7644 → SCIM Agentic Identity Schema (Draft)

The agentic identity schema draft (draft-wahl-scim-agent-schema) extends both
the schema and protocol to cover AI agent identities:

- Defines a new `AgenticIdentity` resource type on top of the core schema
- Adds agent-specific attributes (e.g. OAuth client identifiers, application
  IDs) for provisioning autonomous agents
- Reuses the existing SCIM protocol to provision, authenticate, and authorize
  agents
- Status: individual Internet-Draft (not yet WG-adopted); revision -01 is
  expired/archived, so treat it as exploratory rather than stable

## Reading Order

If you're new to SCIM, we recommend reading the specifications in this order:

1. **RFC 7642** - Start here to understand the overall concepts and goals
2. **RFC 7643** - Learn about the data structures and resource types
3. **RFC 7644** - Understand the API operations and protocol details
4. **RFC 9865** - Learn about advanced pagination techniques for large-scale deployments
5. **RFC 9967** - Learn how SCIM changes are signaled as Security Event Tokens (SETs)
6. **draft-wahl-scim-agent-schema** - Optional, exploratory: how SCIM is being extended to provision AI agent identities

## Implementation Checklist

When implementing SCIM, ensure you:

- [ ] Understand the use cases and requirements from RFC 7642
- [ ] Implement the User and Group schemas from RFC 7643
- [ ] Support core CRUD operations from RFC 7644
- [ ] Implement filtering and sorting capabilities from RFC 7644
- [ ] Consider cursor-based pagination from RFC 9865 for large datasets
- [ ] Support bulk operations if needed (RFC 7644)
- [ ] Implement proper error handling (RFC 7644)
- [ ] Adopt the Security Event Token profile (RFC 9967) if signaling SCIM changes between domains
- [ ] Track the agentic identity schema draft (draft-wahl-scim-agent-schema) if provisioning AI agent identities
