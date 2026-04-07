# MIP-04: Swap State Machine

## Status

- Status: Draft
- Implementation: Required
- Scope: swap execution events and append-only lifecycle
- Related:
  - [MIP-01-protocol-overview.md](./MIP-01-protocol-overview.md)
  - [MIP-03-escrow-descriptor.md](./MIP-03-escrow-descriptor.md)
  - [MIP-05-dispute-policy.md](./MIP-05-dispute-policy.md)

## Purpose

This document defines the event model and state machine for swaps.

## Core Model

A swap is represented by:

- one immutable root event that defines the requested trade
- a sequence of immutable transition events that advance the swap state
- optional replaceable snapshot events for fast lookup

The append-only transition log is the source of protocol history.
The snapshot is an optimization.

## Event Types

### Swap Request

- kind: `7300`
- immutable regular event

Required content:

- `version`
- `swap_id`
- `swap_type`
- `agent`
- `customer`
- `escrow_reference`
- `fiat`
- `bitcoin`
- `expiry`

### Transition

- kind: `7301`
- immutable regular event

Required content:

- `swap_id`
- `state`
- `prev_state`
- `actor_role`
- `reason`
- `created_at`

### Evidence

- kind: `7302`
- immutable regular event

Examples:

- fiat transfer reference
- bank confirmation
- payout proof
- escrow funding proof
- redacted external settlement proof

### Dispute

- kind: `7303`
- immutable regular event

Dispute grammar is part of the swap lifecycle, while dispute policy is defined in [MIP-05-dispute-policy.md](./MIP-05-dispute-policy.md).

### Note

- kind: `7304`
- immutable regular event

Optional human-readable operational note tied to a swap.

### Snapshot

- kind: `30362`
- addressable

Provides a replaceable materialized view of current state for fast lookup.

## State Machine Properties

- the request event is immutable
- every transition is append-only
- sequence coherence matters
- immutable history is authoritative over snapshots

## Participant Responsibilities

### Agent

- keep relay preferences available
- publish evidence or confirmations in a timely way
- reference usable escrow declarations

### Customer

- reference a valid current agent definition
- select a declared escrow descriptor
- publish required settlement instructions
- submit payment proof when required

### Escrow operator

- expose enough public information to be referenced in protocol flows
- publish or validate settlement transitions
- publish resolution transitions when acting as arbiter
