# Project Structure

## Layout

```
cgp-documentation-technical-writing/
├── README.md                   ← Welcome page (what users see when they open the docs)
├── SUMMARY.md                  ← GitBook table of contents — the navigation the reader sees
├── AGENTS.md                   ← Project context for AI agents
├── CLAUDE.md                   ← @AGENTS.md (Claude-specific entry point)
├── .agents/
│   ├── INDEX.md                ← Index of rules and skills
│   ├── rules/                  ← Writing rules (this folder)
│   └── skills/                 ← Skills (e.g. /document-feature)
└── <capability>/               ← One folder per top-level capability with children
    ├── README.md               ← Capability overview page
    └── <child>.md              ← Child pages
```

## File Naming

- Use kebab-case filenames: `identity-providers.md`, `delivery-channels.md`.
- The current `todo-` prefix on filenames marks pages whose content has not been written yet. Once content is finalised, drop the prefix and update `SUMMARY.md` accordingly.
- Capabilities with children become a folder; the capability overview lives at `<folder>/README.md`.
- Capabilities without children are a single file at the root: `audit-trail.md`, `security.md`, etc.

## SUMMARY.md

`SUMMARY.md` is the **navigation the reader sees** in GitBook. Treat it as part of the user experience.

- **Update it whenever you add, move, or delete a page.**
- The order of entries in `SUMMARY.md` is the order users see in the sidebar — choose it deliberately, not alphabetically.
- Page titles in `SUMMARY.md` should match each page's H1 heading. The `[TODO]` prefix should remain only on pages that genuinely have no content yet.
- Indentation reflects hierarchy. Two spaces per level.

Example:

```markdown
* [Communication Center](communication-center/README.md)
  * [Communications](communication-center/communications.md)
  * [Notifications](communication-center/notifications.md)
  * [Delivery Channels](communication-center/delivery-channels/README.md)
    * [In-App Messages](communication-center/delivery-channels/in-app-messages.md)
    * [Emails](communication-center/delivery-channels/emails.md)
    * [SMS](communication-center/delivery-channels/sms.md)
```

## Frontmatter

Every page has YAML frontmatter — see [`page-format.md`](page-format.md) for the full spec. At minimum:

```yaml
---
description: One-sentence summary that appears under the page title.
---
```

## Linking Between Pages

- Use **relative paths** for links between pages in this repo.
- Always link the first mention of another capability ("see [Authentication](../authentication/README.md)").
- Do **not** link to the business-requirements or architecture repos from user-facing pages. Those repos are internal.
