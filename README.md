# SCIM Spec Graph

A graph of the SCIM (System for Cross-domain Identity Management) specifications and their references.

## Overview

This repository provides a visual representation of how various SCIM specifications relate to and depend on each other. Understanding these relationships is essential for developers implementing identity management systems and integrations.

SCIM is a standardized approach for automating the exchange of user identity information between identity domains and service providers. The specifications covered here form the core of modern cloud-based identity management.

## Specifications Covered

### Core SCIM Suite

- **[RFC 7642](https://www.rfc-editor.org/rfc/rfc7642)**: System for Cross-domain Identity Management: Definitions, Overview, Concepts, and Requirements
  - Provides the foundational definitions, high-level overview, and essential concepts for SCIM
  - Explains rationale, system concepts, data models, flows, scenarios, use cases, and requirements

- **[RFC 7643](https://www.rfc-editor.org/rfc/rfc7643)**: System for Cross-domain Identity Management: Core Schema
  - Defines SCIM resource types (User, Group) and their attributes
  - Specifies JSON-based schemas for representing users, groups, and extensions
  - Provides a platform-neutral data model suitable for cloud providers

- **[RFC 7644](https://www.rfc-editor.org/rfc/rfc7644)**: System for Cross-domain Identity Management: Protocol
  - Formalizes the RESTful protocol for SCIM
  - Details HTTP operations (CRUD) and patterns for managing SCIM resources
  - Specifies endpoints, request/response formats, filtering, pagination, and bulk operations

### Extensions

- **[RFC 9865](https://www.rfc-editor.org/rfc/rfc9865)**: Cursor-Based Pagination of SCIM Resources
  - Extends RFC 7643 and RFC 7644
  - Defines cursor-based pagination for SCIM queries and results
  - Improves performance and efficiency for large-scale scenarios

## The Graph

See [Graph.md](Graph.md) for the visual representation of how these specifications relate to each other.

## Why This Matters

When implementing SCIM in your applications:

- Understanding RFC 7642 helps you grasp the overall concepts and requirements
- RFC 7643 tells you how to structure your user and group data
- RFC 7644 shows you how to build the API endpoints and operations
- RFC 9865 provides modern pagination capabilities for scalability

The relationships between these specifications matter because:

- You can't implement the protocol (RFC 7644) without understanding the schema (RFC 7643)
- Both protocol and schema are based on the concepts in RFC 7642
- RFC 9865 builds on top of both schema and protocol to add advanced features

## License

This project is released under the [Unlicense](LICENSE), placing it in the public domain.
