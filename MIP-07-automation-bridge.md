# MIP-07: Automation Bridge

## Status

- Status: Draft
- Scope: operator-layer automation bridge for Nostr-native swaps
- Related:
  - [MIP-01-protocol-overview.md](./MIP-01-protocol-overview.md)
  - [MIP-05-dispute-policy.md](./MIP-05-dispute-policy.md)

## Purpose

This document defines how off-protocol automation systems should affect swaps that are modeled as Nostr-native state machines.

## Design Direction

The bridge should be treated as an automation plane, not merely a webhook subsystem.

That automation plane may include:

- gateway callbacks
- polling workers
- operator consoles
- messaging bots
- reconciliation workers
- provider-specific settlement adapters

## Core Principles

1. automation is not identity
2. no invisible state changes
3. proof chain over trust shortcuts
4. idempotency is mandatory

## Authority Model

Recommended publication models:

- agent-delegated automation
- operator bridge publication
- advisory evidence only

The safest initial model is operator bridge publication.

## Bridge Modes

- observation mode
- evidence mode
- transition mode

## Bridge Input Model

Every adapter input should normalize into a common envelope containing:

- `bridge_input_id`
- `adapter_type`
- `source_type`
- `received_at`
- `raw_payload_hash`
- `external_event_id`
- `external_transaction_id`
- `claimed_action`
- `swap_reference_candidates`
- `signature_valid`
- `idempotency_key`

## Processing Pipeline

1. receive
2. authenticate source
3. normalize
4. match to swap
5. check idempotency
6. evaluate policy
7. publish evidence or transition if allowed
8. persist audit trail

## Transition Eligibility Rules

A bridge input should only cause a public transition if:

- the input source authenticated successfully
- swap matching is unambiguous
- the action is valid for the current swap state
- no higher-priority contradictory state already exists
- the action is allowed by the active bridge policy
