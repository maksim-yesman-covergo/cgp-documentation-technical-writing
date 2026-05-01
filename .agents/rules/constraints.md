# Constraints — What to Keep Out

User-facing documentation has a deliberately narrow scope. The list below is the set of topics, concepts, and framings that **must not appear** in pages in this repo, even though they appear elsewhere in the CGP documentation universe.

## 1. No Domain-Specific (Insurance) Framing

CGP is currently positioned as a domain-agnostic platform that provides basic capabilities. Customers bring their own domain.

**Do not write:**
- "Quote", "policy", "claim", "underwriting", "premium", "endorsement", "policyholder", "broker"
- "Insurance" except as one possible example among others
- Insurance-specific scenarios as the primary example

**Do write:**
- Generic, recognisable examples: eligibility checks, validation, approval workflows, pricing tiers, status changes, customer onboarding, document generation
- "Records", "items", "entities" instead of insurance nouns
- "Your business", "your organisation" instead of "your insurance business"

If the source brief uses insurance language, translate it to neutral language when bringing it into a user-facing page.

## 2. No Multi-Tenancy Concepts

The reader sees one platform. They are not aware that other organisations are using the same software.

**Do not mention:**
- "Tenant", "tenancy", "multi-tenant", "tenant admin", "tenant user"
- "Control Tower" (CoverGo's internal management portal)
- "CoverGo users" / internal CoverGo staff
- That the platform is SaaS, hosted, or shared

**Do say:**
- "The platform" / "your platform"
- "Administrators" / "users in your organisation"
- "Sign in" without referring to which portal it routes to

### Exception — technical identifiers the reader has to type

Some technical identifiers — HTTP headers, query parameters, configuration keys — contain the word "tenant" because that's their literal name in the platform. The reader has to type these names exactly for a request to succeed. In that narrow case:

- **Use the literal name** so the reader's request actually works. For example, an API request must include the `X-Tenant` header.
- **Frame what it represents in neutral terms** — "an identifier for your platform instance", "issued to your organisation when the platform is set up". Do **not** explain that the platform is multi-tenant or that other organisations are using the same software.
- **Apply this carve-out only on pages that document the API directly.** UI-driven pages should not need to surface these identifiers — the portal sends them on the reader's behalf.

## 3. UI-First, API-Fallback

These docs are primarily a guide to using the platform's UI. Default to screenshots and step-by-step instructions; keep implementation detail out.

**Do not mention** (in the default UI-driven case):
- Services, microservices, request/response models, endpoints
- Kafka, message queues, events, streaming
- Postgres, DynamoDB, databases, schemas, tables
- Kubernetes, AWS, load balancers, gateways, deployment topology
- Keycloak (the identity provider implementation)
- Internal architecture, services structure, or how the platform is built

If the underlying behaviour matters, describe it in terms of **what the user sees** in the UI.

### Exception — when a feature has no UI

Some capabilities are usable today but **don't yet have a UI** (or have only partial UI coverage). In that case it is **acceptable and expected** to:

- Link to the **public API spec** (e.g. the Stoplight or Swagger page for the relevant API).
- Tell the reader, in plain language, **how to use the capability via the API** — what to call, with what inputs, to achieve the goal.
- Show **small, focused request/response examples** when they meaningfully help the reader complete the task.

Even in this case:

- Frame the page around the **reader's goal**, not the API surface ("How to send a notification" → here's the endpoint, not "POST /notifications" → here's what it does).
- Mention the API only to the extent the reader needs to use it. Do **not** describe internal services, message buses, or storage.
- When a UI for the same capability ships later, plan to replace the API instructions with UI instructions and demote the API reference to a "Reference" subsection or remove it entirely.
- If only **part** of the feature lacks a UI, document the UI parts the UI way and use the API fallback only for the gaps. Be explicit about which is which.

When in doubt about whether to use an API fallback, ask the user.

## 4. Document Only Supported Capabilities

If a capability isn't shipped, don't write about it — even if a brief describes it as planned.

**Currently unsupported:**
- **Multi-factor authentication (MFA).** Not supported. No mention of OTP, authenticator apps, SMS codes for sign-in, etc.

If you discover something else is unsupported during writing, **stop and ask the user**. Do not silently include or exclude it.

## 5. No Marketing Copy

This is reference documentation, not a product brochure.

**Avoid:**
- Superlatives ("powerful", "seamless", "world-class", "industry-leading")
- Vague benefits without backing detail ("enhances productivity", "drives engagement")
- Forward-looking statements ("we plan to", "soon you'll be able to") unless explicitly approved

**Prefer:** plain, accurate description of what the feature is and does.

## 6. No Internal Process

The reader doesn't need to know how CoverGo builds, releases, or supports the platform.

**Do not include:**
- Sprint plans, roadmaps, release schedules
- Internal team names ("the Communication Center team")
- Names of CoverGo employees
- Internal Jira/Confluence/Slack links

If a page needs a "What's new" section, that's a separate, deliberate page — not inline asides.
