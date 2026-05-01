# Audience

These pages are written for the people who **use and configure** the platform — not the engineers who build it.

## Reader Personas

| Persona | What they want |
| --- | --- |
| **Administrator** | Configure the platform: create users, assign roles, set up rules, publish changes, troubleshoot. |
| **Business user** | Get day-to-day work done: handle records, run processes, send communications, find information. |
| **Power user** | Push the platform further: design complex rule sets, orchestrate workflows, tailor the UI. |

All three are **non-technical by default**. They may be comfortable with concepts like "if/then logic" or "field types", but they will not read code, JSON, or API specs. If a topic genuinely requires a code-shaped example, keep it tiny and explain every part.

## How That Shapes Writing

- **Lead with the task, not the system.** The reader is here to do something. Open every how-to with the goal in plain language ("To create a user…"), not with internals ("The `User` entity is created via…").
- **Speak directly to the reader** with "you". Avoid "the user" when you mean the reader.
- **Examples should be neutral and recognisable.** Eligibility checks, validation, routing, pricing tiers, status changes. **No insurance-specific examples** (no quote/policy/claim/underwriting/premium) — see [`constraints.md`](constraints.md).
- **Define a term once.** Use the [glossary in business-requirements](../../../cgp-documentation-business-requirements/spaces/business/CoverGo-Platform/Glossary.md) as a reference. If a term needs to be explained again, link back to its first definition.
- **Show, then explain.** A screenshot or short example beats a paragraph. Pair every screenshot with the steps the reader is meant to take.
- **Don't over-warn.** Use the warning hint sparingly — only for actions that change live behaviour or are hard to undo. Routine configuration changes don't need a warning on every step.

## What the Reader Does NOT Want

- A description of how the platform works internally.
- The history of why a feature was built.
- Forward-looking statements ("in a future release we will…") unless absolutely necessary.
- Marketing copy.
- Long paragraphs of prose where a list, table, or screenshot would do.
