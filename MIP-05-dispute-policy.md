# MIP-05: Dispute Policy

## Status

- Status: Draft
- Scope: operator-layer dispute and timeout policy for Nostr-native swaps
- Related:
  - [MIP-01-protocol-overview.md](./MIP-01-protocol-overview.md)
  - [MIP-04-swap-state-machine.md](./MIP-04-swap-state-machine.md)

## Purpose

This document defines how an operator should resolve disputes and timeouts for swaps that are modeled as Nostr-native state machines.

## Core Rule

- **the swap state machine is public**
- **the dispute process is operator-governed**

## Dispute Classes

- payment not received
- payment amount mismatch
- payout not sent
- payout amount mismatch
- escrow funding failure
- conflicting external confirmations
- fraud or impersonation risk
- timeout and abandonment

## Timeout Classes

- request expiry
- funding timeout
- payment proof timeout
- payout timeout
- resolution timeout

## Evidence Categories

- payment reference
- transfer receipt
- escrow funding proof
- payout proof
- operator note
- external confirmation reference
- redacted document hash

## Resolution Modes

An operator may resolve disputes by:

- confirming the customer claim
- confirming the agent claim
- splitting outcome where escrow policy allows it
- cancelling and refunding
- escalating to manual review

## Public-Protocol Boundary

### Public

- dispute opened
- dispute escalated
- dispute resolved
- public evidence references
- resolution actor and policy id

### Usually private

- raw screenshots
- internal notes
- private documents
- internal scoring logic
- third-party payloads that contain sensitive data
