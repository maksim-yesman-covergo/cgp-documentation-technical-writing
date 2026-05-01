---
name: document-feature
description: Drive an interview-style flow with the user to gather everything needed to document a feature, then produce a draft user-facing page that matches repo conventions.
argument-hint: "[feature-name-or-path]"
---

# Document Feature

This skill walks the user through everything needed to document a feature in user-facing terms, then produces a draft page that matches the conventions in this repo.

It is **interview-driven**: never invent feature behaviour. If the user can't answer a question, mark the gap with `[TODO]` in the draft and surface the unresolved questions at the end. Do not guess.

**Argument:** `$ARGUMENTS` may contain a feature name (e.g. `roles`) or a target page path (e.g. `identity-and-access/roles.md`). It is optional — if omitted, ask the user which feature they want to document.

## Phase 0 — Load Context

Before asking the user anything:

1. Read [`.agents/rules/system-context.md`](../../rules/system-context.md), [`audience.md`](../../rules/audience.md), and [`constraints.md`](../../rules/constraints.md). These constrain everything you write.
2. Read [`.agents/rules/page-format.md`](../../rules/page-format.md) and [`style.md`](../../rules/style.md) for the page anatomy and voice.
3. Read the current [`SUMMARY.md`](../../../SUMMARY.md) to see where the feature fits in the navigation.
4. Read **2–3 sibling pages** (peers under the same parent capability, or the closest existing feature pages if there are none yet) so the draft matches local conventions.
5. If a corresponding requirement brief exists in the business-requirements repo, skim it for ground truth on what the feature does:
   ```
   ../cgp-documentation-business-requirements/spaces/business/CoverGo-Platform/Requirement-Briefs/
   ```
   The brief is reference material only — do not copy its language, framing, or insurance examples into the user page.

## Phase 1 — Locate the Feature

Confirm where the page belongs:

1. Resolve the feature to a path under the repo root (e.g. `identity-and-access/roles.md`).
2. Confirm with the user whether the page should be:
   - **a new page** (most common — create it)
   - **an edit to an existing draft** (it has `[TODO]` content already)
   - **a child of an existing capability** (verify the parent folder structure)
3. If the location requires creating a new folder or restructuring `SUMMARY.md`, flag this to the user before continuing.

## Phase 2 — Interview the User

Ask the questions below, **one cluster at a time**, in this order. After each cluster, summarise what you've heard back to the user before moving on. If the user says "skip", "don't know", or "later" — record that as a gap and continue.

### A. Headline

1. **What is this feature, in one sentence?** The reader should know what it is and why they'd care after this sentence alone.
2. **Who is the primary reader of this page?** Administrator, business user, or power user? (See [`audience.md`](../../rules/audience.md).)
3. **What's the one job this page should help the reader do?** ("Create a role and assign it to a user", "send a notification to a group", etc.)

### B. Core Idea & Concepts

1. **What are the 2–5 terms the reader needs to know to follow this page?** For each: a one-line definition.
2. **Are there related features the reader should know about?** (Pages to link from "Key concepts" or "Reference".)
3. **Are there any prerequisites?** Permissions the reader needs, configuration that must already exist, capabilities that must be enabled.

### C. How-to Coverage

1. **What are the most common things a reader needs to do with this feature?** Aim for 3–5 tasks. Phrase each as a goal, not a button name. ("Create a role" not "Click Save".)
2. **For each task: what are the steps, in order?** Capture every step that involves a UI action. If the user doesn't know all the steps, ask which task is highest priority and record the rest as `[TODO]`.
3. **Are any tasks reserved for administrators only?** This affects where the task sits and whether to flag the permission requirement.

### D. UI vs API

1. **Does this feature have a UI today?** Three possible answers:
    - **Yes, fully** — write a UI-driven page (steps + screenshots).
    - **No, API only** — write an API-fallback page. Ask: what's the link to the public API spec (Stoplight / Swagger)? Which operations does the reader need to call to accomplish the tasks listed in cluster C?
    - **Partial** — for each task in cluster C, mark whether it's UI-driven or API-fallback. The page will mix both, with a clear visual divider.
2. **For UI-driven tasks: do you have screenshots?** Ask the user to paste image paths or attach them. For each, capture: which task it illustrates and what to call out (highlights, fields, buttons).
3. **If no screenshots yet** — note placeholders (`[TODO: screenshot of …]`) so the page is structured correctly and screenshots can be filled in later.
4. **For API-fallback tasks: do you have a small, focused example** (request body, key parameters) that helps the reader complete the task? Capture it. Do **not** paste full API specs — link to them.

### E. Reference

1. **What fields, options, or settings does this feature expose?** For each: name (matching UI label), what it does, whether it's required, default value, and any constraints.
2. **What permissions or roles control access to this feature?** (Both viewing and editing.)
3. **Are there limits or quotas?** Maximum count, length, frequency, etc.

### F. Troubleshooting

1. **What's the question support hears most often about this feature?**
2. **What can go wrong, and how does the reader fix it?**
3. **Are there known limitations?** Things the feature deliberately doesn't do.

### G. Constraints Check

1. **Is this feature fully shipped today?** If parts of it are not yet supported, capture exactly what's in vs out. Unsupported parts must not appear in the page (see [`constraints.md`](../../rules/constraints.md), specifically: MFA is currently not supported).
2. **Any insurance-specific or multi-tenant framing in the source material that needs translating?** Flag it now so it doesn't slip into the draft.

## Phase 3 — Confirm Before Drafting

Before writing the page:

1. Show the user a short outline (page title, the 5 standard sections, list of how-to titles, list of reference fields).
2. Ask: "Before I draft the full page, anything to add or change?"
3. Wait for confirmation.

## Phase 4 — Draft the Page

Write the draft following [`page-format.md`](../../rules/page-format.md):

```markdown
---
description: <one-sentence description from question A.1>
layout:
  width: wide
---

# <Feature name>

<Overview paragraph: the headline answer plus a sentence on who it's for and the core job it helps with.>

## Key concepts

<2–5 bolded terms, each followed by a one-line definition. Pull from question B.1.>

{% hint style="info" %}
<Optional: prerequisites or "before you start" note from B.3.>
{% endhint %}

## How to <task 1>

1. Step one.
2. Step two.
3. Step three.

![<alt text>](../.gitbook/assets/<capability>/<image>.png)

## How to <task 2>

…

## Reference

| Field | Description | Required | Default |
| --- | --- | --- | --- |
| **<Field name>** | … | Yes | — |

### Permissions

<Who can view, who can edit. Pull from E.2.>

### Limits

<Any limits or quotas. Pull from E.3.>

## Troubleshooting

<details>

<summary><strong><Question></strong></summary>

<Answer.>

</details>
```

While drafting:

- **Apply the constraints in [`constraints.md`](../../rules/constraints.md) actively.** Translate any insurance-specific language to neutral examples. Strip any multi-tenant framing. Omit unsupported behaviour.
- **Match sibling page tone.** Voice, heading style, table format.
- **Mark gaps explicitly.** Anything the user couldn't answer becomes `[TODO: <what's missing>]` so it's visible.

## Phase 5 — Wrap Up

After producing the draft:

1. Save the file at the resolved path.
2. Update `SUMMARY.md`:
   - If the page is new, add the entry in the right place and order.
   - If the page replaces a `[TODO]` entry, drop the `[TODO]` prefix from the title.
3. Report to the user:
   - The path of the page you wrote.
   - The list of unresolved `[TODO]` markers in the draft, by section.
   - Any constraint translations you made (e.g. "Translated 'policy lifecycle' to 'record lifecycle' in the overview").
   - The next concrete step (typically: get screenshots, or fill the highest-priority `[TODO]`).

## Important

- **Never invent.** If you don't have an answer, mark `[TODO]` and ask.
- **Never copy from briefs verbatim.** Briefs are written for an internal audience and use insurance framing. User pages are not.
- **One question cluster at a time.** Don't dump all 21 questions on the user — they will not answer well.
- **Read sibling pages first.** Page consistency matters more than your stylistic instincts.
- **Stop and ask** if you find yourself uncertain about scope, structure, or whether a behaviour is supported.
