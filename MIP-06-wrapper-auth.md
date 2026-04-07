# MIP-06: Wrapper Auth

## Status

- Status: Draft
- Implementation: Recommended
- Scope: operator-layer authentication and account wrapper model over canonical Nostr identity
- Related:
  - [MIP-01-protocol-overview.md](./MIP-01-protocol-overview.md)

## Purpose

This document defines how an operator may provide local account and authentication wrappers over a canonical Nostr identity.

## Core Rule

- **Nostr identity is the canonical principal**
- **local account is a wrapper**

## Non-Goals

- standardizing auth across all Nostr applications
- making API keys portable outside one operator domain
- replacing Nostr identity with local account identity

## Core Principles

1. one canonical identity
2. one wrapper account binds to one canonical identity
3. email/password is not identity
4. recovery restores wrapper access, not identity ownership
5. API keys inherit from a linked principal

## Account Classes

- Nostr-only account
- linked wrapper account
- legacy local account pending link during migration

## Linking Flows

### Nostr-first account creation

1. User signs an operator challenge with Nostr.
2. Operator verifies the proof.
3. Operator creates or finds the canonical Nostr identity.
4. Operator creates a wrapper account or uses wrapperless mode.
5. User may later set email/password.

### Add wrapper auth to existing Nostr account

1. User signs in with Nostr.
2. User adds email.
3. User verifies email.
4. User sets password.
5. Wrapper auth becomes enabled.

### Link legacy local account to Nostr

1. User authenticates with existing local credentials.
2. User completes a Nostr challenge-sign flow.
3. Operator creates or finds the canonical Nostr identity.
4. Operator updates the wrapper account to point to that identity.
5. The user becomes Nostr-primary from that point forward.

## Recovery Model

Recommended recovery levels:

- wrapper recovery
- controlled relink
- recovery lock

Recovery should restore local access without casually redefining the canonical identity.

## Session Issuance

Operators may issue local sessions after proving Nostr control or after successful wrapper login.

Recommended claims:

- `sub_local`
- `canonical_pubkey`
- `npub`
- `auth_method`
- `session_level`
- `issued_at`
- `expires_at`

## API Key Interaction

API keys remain operator-local credentials.
They are not protocol identity.

Core rules:

- an API key MUST resolve to a canonical owner chain
- the canonical owner chain MUST terminate in a Nostr identity for agent-capable usage
- revocation, rotation, and scoping remain operator-local
