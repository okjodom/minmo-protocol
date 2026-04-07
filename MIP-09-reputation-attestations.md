# MIP-09: Reputation Attestations

## Status

- Status: Draft
- Scope: optional operator-signed attestations about agent performance and trust signals
- Related:
  - [MIP-01-protocol-overview.md](./MIP-01-protocol-overview.md)
  - [MIP-08-operator-indexing.md](./MIP-08-operator-indexing.md)

## Purpose

This document defines a clean optional model for portable reputation and performance signals without undermining Nostr-native decentralization.

## Core Position

Internal metrics should be treated as replaceable implementation detail.

The durable design should separate three things:

- **protocol facts**
  - public Nostr events such as swap requests, transitions, disputes, and resolutions

- **operator-derived metrics**
  - counts, rates, confidence scores, and heuristics computed by an operator

- **portable attestations**
  - optional signed public statements by an operator about what they observed or inferred

## Core Principles

1. attestations are opinionated observations
2. facts before scores
3. attributable issuer
4. time-bounded meaning
5. plurality over centrality

## Attestation Event Model

Suggested event type:

- kind: `30363`
- addressable
- `d` tag: stable identifier such as `agent-reputation:<agent-pubkey>` or `agent-reputation:<agent-pubkey>:<policy-id>`

## What Can Be Attested

Recommended portable attestation classes:

- completion rate bands or exact values
- dispute rate bands or exact values
- activity recency
- volume bands
- operator approval status
- moderation status
- trust or service tier

## What Should Not Be Protocolized As Reputation

The following should generally stay private or local:

- raw fraud scores
- detailed support case notes
- private user complaints
- KYC or compliance records
- internal risk models
- proprietary pricing preferences

## Relation To Ranking

- ranking is how an operator orders results in its own product
- attestation is what an operator is willing to sign publicly

An operator may use many private signals for ranking while publishing only a smaller portable subset as attestations.
