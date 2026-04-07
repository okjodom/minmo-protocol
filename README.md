# Minmo Protocol MIPs

This repository contains the `MIP` series: `Minmo Implementation Possibility` documents for the Minmo protocol family.

## Design Direction

- Nostr pubkey is the canonical agent identity
- agent capabilities and discovery metadata are published on Nostr
- swaps are modeled as Nostr-native state machines
- operators may provide business, compliance, indexing, and UX overlays without becoming the identity root

The practical inversion is:

- from `application account owns agent`
- to `Nostr identity is agent, application accounts wrap it`

## MIP Series

The MIPs are ordered by dependency and implementation priority.

- [MIP-01-protocol-overview.md](./MIP-01-protocol-overview.md)
  - overall architecture, shared conventions, privacy boundary, and open questions

- [MIP-02-agent-definition.md](./MIP-02-agent-definition.md)
  - public agent capability and discovery record

- [MIP-03-escrow-descriptor.md](./MIP-03-escrow-descriptor.md)
  - public escrow declaration referenced by agents and swaps

- [MIP-04-swap-state-machine.md](./MIP-04-swap-state-machine.md)
  - request, transition, evidence, dispute, note, and snapshot event lifecycle

- [MIP-05-dispute-policy.md](./MIP-05-dispute-policy.md)
  - dispute classes, timeout classes, evidence boundary, and resolution modes

- [MIP-06-wrapper-auth.md](./MIP-06-wrapper-auth.md)
  - local account wrappers, recovery, sessions, and API key ownership over canonical Nostr identity

- [MIP-07-automation-bridge.md](./MIP-07-automation-bridge.md)
  - validated translation of off-protocol automation inputs into public protocol evidence or transitions

- [MIP-08-operator-indexing.md](./MIP-08-operator-indexing.md)
  - relay ingestion, filtering, freshness, snapshots, and ranking overlays

- [MIP-09-reputation-attestations.md](./MIP-09-reputation-attestations.md)
  - optional signed operator opinions about trust and performance

## Repository Rule

Files in this repository should remain:

- protocol-focused
- atomic by component
- free of implementation-repo details
- free of application-specific database or migration logic
