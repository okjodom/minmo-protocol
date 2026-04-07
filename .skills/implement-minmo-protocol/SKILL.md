---
name: implement-minmo-protocol
description: Use when building an independent implementation of the Minmo protocol from this repository's MIPs. Read the required MIPs first, implement the Nostr-native identity and swap model in dependency order, and keep operator overlays distinct from canonical protocol state.
---

# Implement Minmo Protocol

Use this skill when the task is to implement these specs in another repository or design an implementation plan from them.

## Terminology Guardrail

In these specs, `Agent` means a Minmo protocol participant that can publish capabilities and participate in swaps.

Do not confuse that with an `AI agent` or coding assistant working on a repository or implementation task.

## Start Here

Read [README.md](../../README.md), then read the MIPs in dependency order.

Implementation priority:

1. [MIP-01-protocol-overview.md](../../MIP-01-protocol-overview.md)
2. [MIP-02-agent-definition.md](../../MIP-02-agent-definition.md)
3. [MIP-03-escrow-descriptor.md](../../MIP-03-escrow-descriptor.md)
4. [MIP-04-swap-state-machine.md](../../MIP-04-swap-state-machine.md)
5. [MIP-05-dispute-policy.md](../../MIP-05-dispute-policy.md)
6. [MIP-06-wrapper-auth.md](../../MIP-06-wrapper-auth.md)
7. [MIP-07-automation-bridge.md](../../MIP-07-automation-bridge.md)
8. [MIP-08-operator-indexing.md](../../MIP-08-operator-indexing.md)
9. [MIP-09-reputation-attestations.md](../../MIP-09-reputation-attestations.md)

Treat `MIP-02` through `MIP-05` as the first complete interoperable baseline. Everything after that is an overlay or extension.

## Core Architectural Rules

- Nostr pubkey is the canonical identity.
- Minmo agent discovery and capability data are public Nostr events.
- Swaps are append-only Nostr state machines.
- Operator systems are overlays, not identity roots.
- Snapshot or index views are conveniences, not canonical history.

If your implementation needs a local account system, keep it subordinate to the canonical Nostr identity described in [MIP-06-wrapper-auth.md](../../MIP-06-wrapper-auth.md).

## Minimum Viable Independent Implementation

Support these capabilities first:

- publish and fetch agent definition events
- publish and fetch escrow descriptor events
- create swap request events
- append transition, evidence, dispute, and note events
- derive current swap state from the immutable event log
- apply dispute and timeout policy without hiding public state

Minimum event families from the current drafts:

- `30360`: agent definition
- `30361`: escrow descriptor
- `7300`: swap request
- `7301`: transition
- `7302`: evidence
- `7303`: dispute
- `7304`: note
- `30362`: snapshot
- `30363`: reputation attestation

These numbers are draft conventions, not final globally assigned protocol identifiers. Build your code so kind allocation can be reconfigured.

## Data Modeling Guidance

Model protocol facts separately from operator-local interpretation.

Keep separate layers for:

- canonical Nostr events
- derived current swap state
- operator-local indexing metadata
- private evidence or internal moderation data
- optional reputation or ranking overlays

Do not collapse public facts and private operator judgments into one state record.

## Implementation Order

1. Implement identity and relay handling needed to read and publish the required Nostr events.
2. Implement agent definition and escrow descriptor publication and validation.
3. Implement the swap root plus append-only transition log.
4. Implement state derivation from event history.
5. Implement dispute classes, timeout classes, and evidence references.
6. Add optional wrapper auth, automation, indexing, and reputation layers only after the baseline works.

## Validation Checklist

Before considering an implementation complete, verify:

- replaceable and addressable events follow Nostr semantics
- swap history can be rebuilt from immutable events alone
- snapshots can be discarded and recomputed
- dispute resolution leaves a public audit trail
- private raw documents stay off the public protocol surface
- operator ranking does not overwrite canonical public history

## Reading Hints

Read additional MIPs only when the task needs them:

- [MIP-06-wrapper-auth.md](../../MIP-06-wrapper-auth.md) for account/session wrappers
- [MIP-07-automation-bridge.md](../../MIP-07-automation-bridge.md) for adapters, callbacks, and idempotent automation
- [MIP-08-operator-indexing.md](../../MIP-08-operator-indexing.md) for search, freshness, and materialized views
- [MIP-09-reputation-attestations.md](../../MIP-09-reputation-attestations.md) for portable signed opinions

## Default Biases

Prefer:

- explicit public event publication over hidden internal updates
- deterministic replay from event history
- configurable policy layers around a stable core
- preserving draft uncertainty where the MIPs are still open

Avoid:

- treating operator APIs as canonical protocol state
- assuming one escrow mechanism or one fiat market
- hard-coding one product's database schema into the protocol model
- presenting draft conventions as globally final standards
