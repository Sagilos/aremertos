---
id: POL_access-control
category: policies
title: Access Control Policy
obligation: MUST
requirement_references: [OIDC-PKCE]
internal_references: []
normative_vs_informative: normative
---

# Access control
To meet the security criteria demanded by EU cyber regulations, your specification must enforce these modern baseline rules:
- **RFC 8252: OAuth 2.0 for Native Apps** 
  - Clients handling web-views must open external browser contexts to isolate credentials safely.
- **RFC 9700: OAuth 2.0 Security Best Current Practice** 
  - Explicitly bans the legacy Implicit Flow & mandates exact-string matching for redirect URIs.
- **IETF Draft: OAuth 2.0 for Browser-Based Applications**
  - Formally details how browser apps must handle token storage & recommends evaluating a Backend-for-Frontend (BFF) pattern to isolate tokens from Cross-Site Scripting (XSS) risks inside the browser.

# AuthN : Authentification
AuthN (Authentication): Verifies who you are. It is the process of validating a user’s identity (e.g., via passwords, biometrics, or one-time codes). The primary output is typically an `ìd_token`.
## RFC to enforce
- **OpenID Connect Core 1.0**
  - Defines the payload of the ID Token and requires the implementation of the `/userinfo` endpoint.
- **OpenID Connect Discovery 1.0** 
  - Mandates `/.well-known/openid-configuration` endpoint so your application can fetch the identity provider’s signing keys (JWKS).
- **RFC 7515: JSON Web Signature (JWS)**
  - Dictates how ID Tokens are digitally signed so the browser can prove the token hasn't been altered by a third party.
- **RFC 7519: JSON Web Token (JWT)** 
  - Defines the exact claims structure that allows OIDC clients to parse and trust verified identities securely.

# AuthZ : Authorisations
AuthZ (Authorization): Verifies what you are allowed to do. It determines your access rights, roles, and permissions after your identity is proven. The primary output is an `access-token`.
## RFC to enforce
- **RFC 6749: The OAuth 2.0 Authorization Framework**
  - Outlines the fundamental token-based authorization workflows.
- **RFC 6750: OAuth 2.0 Bearer Token Usage**
  - Defines how to present the Access Token to your APIs using the HTTP Authorization: `Bearer <token>` header.
- **RFC 7636: Proof Key for Code Exchange (PKCE)**
  - Eliminates the need for a client secret by creating a dynamic cryptographic challenge `code_challenge` and verifier `code_verifier` for every login session.
- **RFC 7662: OAuth 2.0 Token Introspection**
  - Requires your internal backend APIs to be able to verify token validity, active status, and scopes in real-time against the Authorization Server.
- **RFC 9068: JWT Profile for OAuth 2.0 Access Tokens** 
  - Standardizes your `access_token` as JWTs covering by user permissions, roles, and scopes are structured uniformly for your API gateways to read.

### Contexte validation - Audience check
When your backend API receives an Access Token, it must check if the aud value exactly matches its own identifier.
If your API skips this check, it will mistakenly accept valid tokens meant for an entirely different application or client. A malicious or compromised client could take a token meant for a low-security public API and replay it against your high-security internal API.

### Capability validation - RBAC Mapping
While the aud check ensures the token was intended to be sent to your API, it does not grant permissions. That is the job of your internal RBAC.
Once the audience is verified, your API must inspect the authorization claims within the token to enforce access control:
- **Scopes (scp or scope)**
  - These define what the client application is allowed to do on behalf of the user (e.g., scope: `"read:profile"`).
- **Roles / Groups (roles, groups)**
  - These define what the actual user is allowed to do based on their corporate or system identity (e.g., roles: `["FinanceAdmin"]`).
- **Enforce a strict logical `AND` match**
  - Both requierments must be matched to comply, RFC9068 & RFC9700 & NIS2 & RGPD
