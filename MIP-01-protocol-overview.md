# MIP-01: Protocol Overview

## Status

- Status: Draft
- Implementation: Informational
- Scope: overall architecture and shared conventions for the protocol family
- Depends on:
  - NIP-01
  - NIP-19
  - NIP-24
  - NIP-42
  - NIP-46
  - NIP-65
  - NIP-89
  - NIP-98
- Related:
  - [MIP-02-agent-definition.md](./MIP-02-agent-definition.md)
  - [MIP-03-escrow-descriptor.md](./MIP-03-escrow-descriptor.md)
  - [MIP-04-swap-state-machine.md](./MIP-04-swap-state-machine.md)
  - [MIP-05-dispute-policy.md](./MIP-05-dispute-policy.md)
  - [MIP-06-wrapper-auth.md](./MIP-06-wrapper-auth.md)
  - [MIP-07-automation-bridge.md](./MIP-07-automation-bridge.md)
  - [MIP-08-operator-indexing.md](./MIP-08-operator-indexing.md)
  - [MIP-09-reputation-attestations.md](./MIP-09-reputation-attestations.md)

## Purpose

This document defines the architecture and shared conventions for the Minmo Nostr protocol family.

## Core Goals

1. Agents are discovered and identified by Nostr identity.
2. Agent capabilities are published as Nostr events.
3. Swaps are modeled as Nostr-native state machines.
4. Operators are optional overlays rather than identity roots.

## Principals

- **Agent**
  - a Nostr identity that publishes capability data and participates in swaps

- **Customer**
  - a Nostr identity that requests an onramp or offramp

- **Escrow provider**
  - a declared settlement mechanism and operator used by the swap

- **Operator**
  - an optional implementation layer that indexes, filters, validates, or presents protocol interactions

## Protocol Layers

1. **Identity and discovery**
   - Nostr profile metadata
   - relay list metadata
   - agent definition

2. **Execution and state**
   - swap request
   - transition log
   - evidence
   - dispute lifecycle

3. **Operator overlays**
   - wrapper auth
   - indexing
   - automation bridge
   - reputation attestations

## Canonical Nostr Rules Versus Protocol Conventions

### Canonical Nostr rules

The following come from Nostr itself:

- events are signed by a pubkey and identified by event id
- kind `0` is user metadata
- kind `10002` is relay list metadata
- kinds `30000-39999` are addressable events keyed by `kind`, `pubkey`, and `d`
- kind `27235` is NIP-98 HTTP auth
- kind `31990` is an app handler announcement

### Protocol conventions

Everything else in this protocol family is layered on top of Nostr, including:

- agent definition events
- escrow descriptor events
- swap state events
- dispute semantics
- operator attestations and overlays

## Event Kind Allocation

The concrete kinds used in this protocol family are draft conventions. They are not assigned by any NIP.

These numbers should not be treated as globally stable protocol identifiers yet.

Recommended allocation strategy:

- use them only as draft conventions during design and controlled deployments
- prefer experimental kind ranges for early real-world rollout to reduce collision risk
- coordinate longer-term kind assignments with the Nostr community before claiming stable public protocol numbers

For early deployment, implementations should strongly prefer:

- experimental regular-event ranges such as `20000-29999` for non-final immutable event kinds
- operator-controlled addressable conventions until the event family is ready for wider coordination

## Shared Privacy Boundary

### Public by default

- agent identity
- public capabilities
- escrow declarations
- swap root event existence
- state transitions
- public dispute outcomes

### Often private or minimized

- exact balances
- sensitive KYC data
- raw documents or screenshots
- provider secrets
- internal moderation notes
- private scoring logic

## Open Questions

- whether swap snapshots should be operator-authored, participant-authored, or both
- whether encrypted payload references should be standardized for evidence
- how key rotation should be represented for long-lived agents
- whether escrow descriptors need subtype-specific schemas
- whether agent acceptance should be explicit for all swaps or optionally implicit for automated agents
