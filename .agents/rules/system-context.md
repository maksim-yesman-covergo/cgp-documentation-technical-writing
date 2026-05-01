# System Context

## What CGP is

The **CoverGo Platform (CGP)** is a configurable, modular platform that provides the building blocks every business application needs — identity, data, rules, workflows, communications, documents, and more — that customers compose to build the solution their business needs.

CGP is **domain-agnostic**: it ships the basic capabilities, and customers configure them for whatever domain they're working in. Any domain-specific framing (insurance, finance, healthcare) belongs to the customer, not to CGP itself, and **must not appear** in user-facing documentation.

## Capabilities Documented Here

The repo currently documents these top-level capabilities (see [`SUMMARY.md`](../../SUMMARY.md) for the live structure):

| Capability | What it covers |
| --- | --- |
| **Authentication** | Sign-in, identity providers, sessions |
| **Identity & Access** | Users, roles, user groups, authorisation resources |
| **Security** | Platform-wide security model and practices |
| **Party** | Person/organisation records and party-role definitions |
| **Dynamic Data Model** | Configuring entities, attributes, relationships; managing content |
| **Reference Data** | Code lists, lookup tables, currencies |
| **Rules** | Rule definitions, configuration, evaluation |
| **Workflow** | Process configuration and execution |
| **Portals** | Which portals exist and what they're for |
| **UI Plugins** | Extending portal screens with custom UI |
| **Communication Center** | Notifications across in-app, email, and SMS channels |
| **Documents** | Document definitions and composition |
| **Publish** | Promoting configuration changes safely |
| **Audit Trail** | Who did what and when |

Each capability page (and its children) follows the page anatomy in [`page-format.md`](page-format.md).

## Where to Find Authoritative Info

If you need to know what a capability actually does, in detail, consult the business-requirements repo first:

```
../cgp-documentation-business-requirements/spaces/business/CoverGo-Platform/
├── Requirement-Briefs/   ← capability-level briefs (start here)
├── Requirements/         ← detailed functional requirements
└── Glossary.md           ← canonical terminology
```

The architecture repo (`cgp-documentation-architecture/`) is rarely useful for user-facing docs — it describes services, APIs, and infrastructure, none of which the reader sees or cares about.

## What's Visible to the Reader

The reader sees **the platform** — they sign in to a portal, they configure things, they get notifications, they see audit history. They do **not** see:

- Multiple tenants, the Control Tower, or that CGP is multi-tenant SaaS.
- Services, APIs, Kafka, databases, Kubernetes, or any infrastructure.
- Internal CoverGo team structure, release processes, or deployment topology.

These exclusions are listed in detail in [`constraints.md`](constraints.md).

## Currently Unsupported

Some things appear in business requirements but are **not yet shipped**, and must not be documented as if they exist:

- **Multi-factor authentication (MFA).** Not supported. Do not document it.

If you discover during writing that something else is also unsupported, ask the user before publishing.
