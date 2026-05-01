# Page Format

## Frontmatter

Every page begins with YAML frontmatter. Required fields:

```yaml
---
description: >-
  One sentence describing what this page is about. Appears under the page
  title in GitBook and in search results.
---
```

Optional fields used on the welcome page or feature overviews:

```yaml
---
description: ...
icon: hand-wave            # GitBook icon name (welcome / overview pages only)
layout:
  width: wide              # default for all pages in this repo
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---
```

`layout.width: wide` is the **default for every page in this repo** — content reads better at wide width when there are screenshots, tables, or step-by-step lists. Always include it. For most feature pages, the minimum frontmatter is therefore:

```yaml
---
description: ...
layout:
  width: wide
---
```

## Standard Page Anatomy

Every feature page follows the same five-section shape. Once a reader has read one page, they know how to read the rest.

```markdown
---
description: ...
---

# <Feature name>

<One-paragraph overview: what this feature is and why a reader would care.>

## Key concepts

<Defines the 2–5 terms the reader needs to follow the rest of the page.>

## How to <do task 1>

<Step-by-step instructions. Numbered list. Screenshots where helpful.>

## How to <do task 2>

<Step-by-step instructions.>

## Reference

<Field definitions, permission requirements, configuration options.>

## Troubleshooting

<Common questions and their answers, in Q&A or expandable form.>
```

Not every page needs every section. Drop the ones that don't apply (e.g. a concept-only page can skip Reference).

## GitBook Syntax

The platform renders standard CommonMark plus a few GitBook-specific blocks. Use them.

### Hints

```markdown
{% hint style="info" %}
Tips and helpful context.
{% endhint %}

{% hint style="warning" %}
Watch out — this changes live behaviour.
{% endhint %}

{% hint style="success" %}
Best practice we've seen work well.
{% endhint %}

{% hint style="danger" %}
Destructive or irreversible action.
{% endhint %}
```

Use sparingly. A page covered in hints stops being useful — readers learn to skip them.

### Expandables

For optional detail or troubleshooting Q&A:

```markdown
<details>

<summary><strong>Short summary</strong> — clarifying tail</summary>

Details that are useful but not on the critical path for first-time readers.

</details>
```

### Tabs

For showing the same task in different contexts (e.g. "From the menu" vs "From the keyboard shortcut"):

```markdown
{% tabs %}
{% tab title="Option A" %}
Content for option A.
{% endtab %}

{% tab title="Option B" %}
Content for option B.
{% endtab %}
{% endtabs %}
```

### Tables

Use minimal-width markdown tables; they render the same and pass linters reliably:

```markdown
| Column | What it does |
| --- | --- |
| **Field name** | Description. |
```

## Voice and Formatting

See [`style.md`](style.md) for voice, tone, and terminology rules.

## Screenshots and Images

- Place images under `.gitbook/assets/<capability>/` to keep them organised.
- Use descriptive filenames: `users-create-form.png`, not `screenshot-2026-05-01.png`.
- Always include alt text: `![Create user form with required fields highlighted](../.gitbook/assets/identity-and-access/users-create-form.png)`.
- Annotate screenshots when steps reference specific UI elements (numbered callouts work well).
- Keep screenshots up to date — a stale screenshot is worse than none.

## API Reference Fallback

Default to UI-driven, screenshot-based pages. **Only when a capability has no UI** is it acceptable to instruct the reader via the API — see [`constraints.md`](constraints.md) for the carve-out.

When you do, follow this shape inside the standard page anatomy:

```markdown
{% hint style="info" %}
This capability does not yet have a UI. Use the API as described below. Once the UI ships, this page will be updated.
{% endhint %}

## How to <task>

1. Open the [<API name> reference](<link to Stoplight / Swagger>).
2. Call the `<HTTP verb> <endpoint>` operation with:
   - `<field>` — what to put here, in plain language.
   - `<field>` — …

Example request body:

`​`​`json
{
  "field": "value"
}
`​`​`

You'll get back …
```

Keep examples **small and focused** on what the reader needs to copy. Don't paste the full API spec — link to it.

## What to Avoid

- **No H1 below the top-level page title.** Use H2 (`##`) for sections.
- **No code blocks of API requests / JSON / YAML** unless this is an API-fallback page (see above).
- **No "Last updated" footer** — GitBook handles that. Do not add it manually.
