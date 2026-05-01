---
description: How users and external systems authenticate to the platform.
layout:
  width: wide
---

# Authentication

The platform has no public access. Every portal screen and every API request must come from an authenticated user — there are no anonymous pages and no public endpoints. Authentication is what proves who is making a request.

You'll meet authentication in two places:

- **In a portal,** when you open a portal URL and the platform asks you to sign in.
- **In an API integration,** when an external system calls the platform's API and must include credentials with every request.

This chapter covers both, plus what happens after sign-in (sessions) and how you can use the platform to sign users in to your own applications.

## Key concepts

- **User.** The account that represents a person, or a system, on the platform. Created by an administrator and identified by a username and email. See [Users](../users.md).
- **Credentials.** The proof you provide to sign in. Most often a password; can also be an [API key](api-keys.md), or trust delegated to an external [identity provider](identity-providers.md).
- **Identity provider.** The service that verifies your credentials. By default, the platform verifies username and password itself. Administrators can configure additional identity providers — for example, your organisation's existing corporate sign-in — so users can sign in with accounts they already have. See [Identity Providers](identity-providers.md).
- **Session.** The active period after you sign in to a portal, during which you can keep using the platform without signing in again.
- **API key.** A key issued to a user that an external system can use to authenticate to the API as that user. API keys are managed on each user's detail page in [Identity and Access](../README.md). See [API keys](api-keys.md).
- **Single sign-on (SSO).** Signing in once and being recognised across multiple systems that trust the same identity provider. The platform supports SSO across all of its portals, and can act as the identity provider for your own external applications. See [SSO for external applications](sso-for-external-applications.md).

## Signing in to a portal

Each portal has its own URL. When you open the URL, the platform sends you to the sign-in page, where you can either:

- enter your **username (or email) and password**, or
- choose an **identity provider** if your administrator has configured one.

Once you sign in successfully, the platform takes you back to the page you originally requested.

{% hint style="info" %}
**Suspended accounts.** If you fail to sign in **five times in a row** with username and password, your account is **suspended for 30 minutes** to protect against guessing attacks. You can try again after the 30 minutes are up.

**Deactivated accounts.** If your account has been **deactivated** by an administrator, you can't sign in until they reactivate it. Being deactivated is separate from being suspended — deactivation is a deliberate admin action, not something that happens automatically.

**Pending activation.** A newly-created account is in **Pending** status until you verify your email and set a password. You can't sign in until activation is complete. See [Activate your account](activate-account.md).
{% endhint %}

For step-by-step instructions, see:

- [Sign in](sign-in.md) — every-day sign-in flow.
- [Activate your account](activate-account.md) — first time, setting your initial password.
- [Reset your password](reset-password.md) — when you've forgotten it.

## Authenticating to the API

The API doesn't keep a server-side session for callers — every request must carry credentials. To call the API as a user, an external system uses an **API key** issued to that user, sent as a header on each request.

Every API request must also include an **`X-Tenant` header**. This header identifies your platform instance and is issued to your organisation when the platform is set up. Requests without it are rejected.

API keys are created and revoked on the user's detail page in **Identity and Access**. See [API keys](api-keys.md).

## Sessions

After you sign in to a portal, your session stays active as long as you're using the platform. Two limits apply:

- **Idle timeout.** If you don't do anything in the platform for **30 minutes**, your session ends and you'll need to sign in again.
- **Maximum lifetime.** Even with continued use, your session expires after **30 days**, after which you'll be asked to sign in again.

Opening a new tab or switching between portals doesn't require a new sign-in — the platform remembers you across tabs and across portals during an active session. There's no limit on the number of active sessions per user.

Every session is tied to a specific user account on the platform. Whether you sign in with a password or through an identity provider, the platform always has a record of you as a user — and that record is what the session represents. A session can't exist without a corresponding user.

See [Sessions](sessions.md).

## Using the platform to sign users in to your own applications

If your organisation builds its own applications and you want users to sign in with the same accounts they use on the platform, you can configure the platform as the identity provider for those applications. The platform handles sign-in; your application receives the verified user.

See [SSO for external applications](sso-for-external-applications.md).

## More in this chapter

- [Identity Providers](identity-providers.md) — built-in and external providers, and how to add one.
- [Password policy](password-policy.md) — the rules new and changed passwords must meet.

## Related pages

- [Users](../users.md) — managing the people who can sign in.
- [Security](../../todo-security.md) — the platform's overall security model.
