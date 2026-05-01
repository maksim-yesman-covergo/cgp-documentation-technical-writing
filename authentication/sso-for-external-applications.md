---
description: >-
  Use the platform as the identity provider for your own applications, so
  users sign in once with their platform account and are recognised across
  every system.
layout:
  width: wide
---

# SSO for external applications

If your organisation builds its own applications and you want users to sign in with the same accounts they use on the platform, you can use the platform as the **identity provider** for those applications. Users sign in on the platform once; your application receives the verified user identity without managing passwords of its own.

There's no per-application registration step today — any application that knows the platform's OIDC issuer URL can run the flow and receive a verified user. You provide the redirect URI on each request.

This page covers:

- **The flow** — how the platform and your application talk to each other.
- **What to configure** in your application's OIDC client.
- **Skipping the platform's sign-in screen** with `kc_idp_hint`.
- **What your users see** during sign-in.

## How the flow works

The platform uses the standard [OpenID Connect (OIDC) Authorization Code Flow](https://openid.net/specs/openid-connect-core-1_0.html). At a high level:

1. A user opens your application.
2. The application checks whether the user is already authenticated. If not, it redirects them to the platform's authorisation endpoint.
3. The platform shows its standard [sign-in screen](sign-in.md). The user signs in with their platform account — username and password, or any [identity provider](identity-providers.md) configured on the platform.
4. The platform redirects the user back to your application's redirect URI with a one-time **authorisation code** in the URL.
5. Your application's backend exchanges the code for an **ID token** (proving who the user is) and an **access token** (letting the application call the platform's API on the user's behalf).
6. The user is now signed in to your application.

If the user already has an active session on the platform, step 3 is silent — they aren't asked to sign in again, just redirected straight back to your application. See [Sessions](sessions.md).

## How to integrate your application

Use any standard OIDC client library on the application's side. Configure it with the values below.

### OIDC discovery URL

The platform exposes an OIDC discovery document your library can use to learn the authorisation, token, JWKS, and userinfo endpoints automatically:

```
https://<host>/realms/cgp_<your-platform-id>/.well-known/openid-configuration
```

- `<host>` — the platform's identity host, environment-specific.
- `<your-platform-id>` — the same identifier you use as the value of the [`X-Tenant` header](api-keys.md#headers-on-each-request) when calling the API.

The issuer URL itself (without `/.well-known/openid-configuration`) is what some libraries ask for instead of the discovery URL.

### Client values

| Value | What to use |
| --- | --- |
| **Client ID** | The literal string `public`. The platform uses a single shared public client for external applications today. |
| **Client secret** | Not required. The platform uses **public-client** OIDC — your library should be configured for a public client, not a confidential one. |
| **Redirect URI** | Any URL on your application that should receive the redirect after sign-in. You provide this on each request; it isn't pre-registered. |
| **Scopes** | At minimum `openid`. Add `profile` and `email` if your application needs the user's basic profile information. |

Once configured, the library handles the authorisation code flow for you — redirecting the user to the platform, receiving the callback, exchanging the code for tokens, and validating the tokens against the JWKS published in the discovery document.

After sign-in, the access token can be used to call the platform's API as the user — send it as `Authorization: Bearer <access_token>`, plus the platform identifier on every request (the `X-Tenant` header for server-side calls, or `?X-Tenant=<your-platform-id>` as a query parameter on browser-driven GETs where setting custom headers isn't practical). See [API keys](api-keys.md#how-to-use-an-api-key-in-a-request) for the request shape.

### Skipping the sign-in screen with `kc_idp_hint`

If your application already knows which identity provider the user wants to sign in with, you can pass `kc_idp_hint=<provider-id>` as a query parameter on the authorisation request. The platform skips its own sign-in screen and sends the user straight to that identity provider.

This is useful when:

- Your application asks the user to choose a sign-in option in its own UI.
- You're embedding the flow in a context where you don't want to show two layers of sign-in chrome.

The provider ID matches the identifier of the [identity provider](identity-providers.md) configured on the platform.

If `kc_idp_hint` is omitted or names a provider that isn't configured, the platform falls back to its standard sign-in screen.

## What your users see

The platform shows users the **same sign-in screen** for external applications as for its own portals — there's no separate look-and-feel. See [Sign in](sign-in.md).

If the user is already signed in to the platform, they aren't asked to sign in again. Sessions cover external applications too — sign in once and the user is recognised across every system that trusts the same OIDC issuer. See [Sessions](sessions.md).

## Reference

### Discovery URL

```
https://<host>/realms/cgp_<your-platform-id>/.well-known/openid-configuration
```

### Authorisation request — recognised query parameters

| Parameter | Value |
| --- | --- |
| `client_id` | `public` |
| `redirect_uri` | The URL on your application that should receive the redirect. |
| `response_type` | `code` |
| `scope` | At minimum `openid`. Optionally add `profile`, `email`. |
| `state` | An opaque value your application generates and verifies on the callback. Standard CSRF protection. |
| `kc_idp_hint` *(optional)* | The identifier of an identity provider configured on the platform. Skips the sign-in screen and routes the user straight to that provider. |

### Token endpoint

Resolved from the discovery document. Exchange the authorisation code with `grant_type=authorization_code`, `code=<the_code>`, and `redirect_uri=<same_url_used_initially>`. No client secret is sent.

## Troubleshooting

<details>

<summary><strong>The authorisation code is rejected when we try to exchange it.</strong></summary>

A few things to check:

- The code can only be exchanged **once**. If your code retries the exchange after a failure, the second attempt will fail.
- Authorisation codes are short-lived — exchange them immediately after receiving them.
- The `redirect_uri` sent on the token request must match exactly what you sent on the authorisation request — same scheme, host, port, path, and trailing slash (or lack of one).

</details>

<details>

<summary><strong>Users are redirected to the platform but never come back to our application.</strong></summary>

Usually a problem on the application side — the redirect URI you sent isn't reachable, or your application isn't handling the callback correctly. Open the platform's redirect URL in a browser directly and check what your application returns when it receives an `?code=...` parameter.

</details>

<details>

<summary><strong>An ID token signature failed verification.</strong></summary>

Your OIDC client library should fetch the platform's public signing keys from the JWKS endpoint advertised by the discovery document — and re-fetch them periodically, in case keys have rotated. If you're caching keys for too long, signature verification will fail when keys rotate. Use a library that handles JWKS rotation automatically rather than caching keys yourself.

</details>

<details>

<summary><strong>We pass <code>kc_idp_hint</code> but users still see the platform's sign-in screen.</strong></summary>

Either the value doesn't match an identity provider configured on the platform, or the provider isn't enabled. Check the configured providers and confirm the identifier you're passing. See [Identity Providers](identity-providers.md).

</details>
