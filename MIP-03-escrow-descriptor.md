# MIP-03: Escrow Descriptor

## Status

- Status: Draft
- Scope: public escrow declaration for swap compatibility and execution assumptions
- Related:
  - [MIP-01-protocol-overview.md](./MIP-01-protocol-overview.md)
  - [MIP-02-agent-definition.md](./MIP-02-agent-definition.md)
  - [MIP-04-swap-state-machine.md](./MIP-04-swap-state-machine.md)

## Purpose

This document defines the public escrow descriptor event referenced by agent definitions and swaps.

## Event Type

- kind: `30361`
- addressable
- `d` tag: stable identifier for one escrow configuration

## Function

The escrow descriptor tells counterparties and operators:

- what escrow mechanism is used
- on which network
- what the funding and release rules are
- how the escrow instance is referenced
- what timeout and dispute assumptions apply

## Minimum Content

`content` is JSON and MUST be versioned.

Minimum expected fields:

- `version`
- `escrow_type`
- `network`
- `funding_rules`
- `release_rules`
- `dispute_rules`
- `reference_format`
- `updated_at`

## Selection Rules

Every agent profile should declare:

- at least one usable escrow configuration
- one default escrow configuration

That declared escrow must be usable without out-of-band negotiation at swap time.

## Open Question

Different escrow mechanisms may eventually need subtype-specific schemas rather than one generic descriptor shape.
