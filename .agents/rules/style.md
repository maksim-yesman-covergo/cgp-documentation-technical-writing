# Style

## Voice

- **Direct.** Address the reader as "you". Avoid "the user" / "users will" when you mean the reader.
- **Plain.** Prefer the simpler word: *use* over *utilise*, *show* over *display*, *change* over *modify*.
- **Active.** "Click **Save**" beats "The **Save** button should be clicked".
- **Confident, not boastful.** State what is true. Skip superlatives ("powerful", "seamless", "world-class").
- **Neutral examples.** Eligibility, validation, routing, status changes, customer onboarding. **No insurance examples** — see [`constraints.md`](constraints.md).

## Tense and Person

- **Present tense** for what the platform does: "The rule **evaluates** every record."
- **Imperative** for steps: "**Open** the Users page. **Click** Add user."
- **Second person** ("you") for the reader.
- Avoid first person ("we") except in the welcome page or genuine editorial asides.

## Page Titles and Headings

- Page title (H1) is **the noun the reader is looking for**: "Users", "Roles", "Notifications" — not "Working with users" or "User management overview".
- Section headings (H2) describe what the section is about: `## Key concepts`, `## How to invite a user`, `## Reference`.
- Use **sentence case** for headings: "How to invite a user", not "How To Invite A User".
- Don't repeat the page title in section headings.

## Terminology

These are the canonical terms used in user-facing docs. Use them consistently.

| Use | Don't use |
| --- | --- |
| sign in, sign out | log in / log on / login |
| email | e-mail |
| user, administrator | tenant user, tenant admin (see [`constraints.md`](constraints.md)) |
| the platform | the system, the application, the SaaS |
| record / item | tuple, row, document (unless specifically a Document) |
| select, choose | pick, hit, smash |
| menu, button, field, panel | UI control terms — match what the screen literally shows |
| identity provider, single sign-on | IdP, SSO (spell out at first mention; abbreviate after) |

When the platform's UI uses a specific label, **match the label exactly** — capitalisation, spacing, punctuation. If the screen says "Sign in", write "Sign in" (not "Sign In" or "sign-in").

## UI References

- **Bold** for things the reader interacts with: "click **Save**", "open the **Users** page".
- `Monospace` for system identifiers, field names in data, code-shaped values: `record_id`, `pending`.
- *Italics* sparingly, for emphasis only.

## Lists

- Use a numbered list for **sequential steps** (must be done in order).
- Use a bullet list for **collections** (order doesn't matter).
- Don't mix the two — pick one per list.
- Each list item should start with a capital letter and end with a full stop, unless it's a single noun phrase.

## Punctuation and Formatting

- Use **em dash (—)** for asides, not double hyphens (--) or parenthetical phrases that could just be commas.
- Oxford comma: yes.
- One space after a full stop, not two.
- No trailing whitespace.
- Wrap lines around 100 characters where it makes the diff readable, but don't break tables, links, or hint blocks.

## Linking

- Link the **first mention** of any other capability or concept on the page.
- Link text is the **target page name** in plain reading order: "see [Roles](../identity-and-access/roles.md)" — not "click [here](...)".
- Don't link the same page twice in the same section.

## Numbers, Dates, Times

- Numbers under 10: spell out ("three users"). 10 and above: digits ("12 users").
- Dates: `1 May 2026` or `2026-05-01`. Never `5/1/26` or `05/01/2026`.
- Times: 24-hour with timezone (`14:30 UTC`) when precision matters.

## When in Doubt

Read 2–3 sibling pages and match their tone. If those pages disagree, the most recently edited one wins.
