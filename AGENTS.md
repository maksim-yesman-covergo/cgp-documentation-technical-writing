# CGP Technical Writing — User-Facing Documentation

## Project Overview

This repository is the source of truth for **user-facing documentation of the CoverGo Platform (CGP)**, published via GitBook. Audience is the people who **use and configure** the platform — administrators, business users, and power users — not the engineers who build it.

All content lives in Markdown files at the repository root, organised one chapter per top-level capability. The chapters and their hierarchy are reflected in [`SUMMARY.md`](SUMMARY.md).

## Sister Repositories

This repo is one of three under `cgp-documentation/documentation/`:

| Repo | Purpose | Audience |
| --- | --- | --- |
| `cgp-documentation-business-requirements` | Business requirement briefs, WBS, requirements | Internal — product, BAs, engineers |
| `cgp-documentation-architecture` | Solution architecture, services, APIs, data models | Internal — engineers, architects |
| **`cgp-documentation-technical-writing`** *(this repo)* | **End-user product documentation** | **External — tenant admins & users** |

When you need authoritative information about a feature (what it does, how it's configured, what fields it has), the **business-requirements** repo is the source you should consult. Architecture is rarely relevant for user-facing docs and should not bleed into them.

## Agent Guidelines

All rules and skills live in `.agents/`.

**Before any work, read [`.agents/INDEX.md`](.agents/INDEX.md) to load the relevant guidelines into context.**

Most importantly:

- [`.agents/rules/system-context.md`](.agents/rules/system-context.md) — what CGP is and the capabilities you'll document.
- [`.agents/rules/audience.md`](.agents/rules/audience.md) — who reads these pages and how to write for them.
- [`.agents/rules/constraints.md`](.agents/rules/constraints.md) — what to keep out of these pages (multi-tenancy, infrastructure, unsupported capabilities).
- [`.agents/rules/page-format.md`](.agents/rules/page-format.md) — frontmatter, GitBook syntax, page anatomy.
- [`.agents/rules/style.md`](.agents/rules/style.md) — voice, tone, terminology.
- [`.agents/rules/project-structure.md`](.agents/rules/project-structure.md) — file layout and `SUMMARY.md`.

## Hard Rules

- **Domain-agnostic framing.** CGP is a configurable building-block platform. Do **not** position it as an insurance product or use insurance-specific examples (quote, policy, claim, underwriting, premium). Use generic examples (eligibility, validation, routing, pricing).
- **No multi-tenancy concepts.** Never mention "tenants", "Control Tower", "tenant admin portal", or the SaaS infrastructure. From the reader's perspective there is just **the platform**.
- **UI-first, API-fallback.** Documentation is primarily a guide to using the platform's UI — screenshots, step-by-step, no code. **Exception:** if a capability has no UI yet (it's only reachable via API), link to its public API spec and describe how the reader can use it. See [`.agents/rules/constraints.md`](.agents/rules/constraints.md) for what's allowed when an API fallback is used.
- **Document only what's supported.** If a capability isn't shipped (e.g. multi-factor authentication is not currently supported), do not document it — even if it appears in business requirements.
- **One H1 per page** that matches the page filename's intent. Page title and H1 must agree.
- **Update `SUMMARY.md` whenever you add, move, or remove a page.**
- **Read 2–3 sibling pages of the same kind before creating a new one** to match established structure.
- **Never invent feature details.** If something isn't in the business-requirements repo or confirmed by the user, ask before writing it.
