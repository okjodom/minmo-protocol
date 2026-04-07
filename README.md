# Minmo Protocol MIPs

Minmo is a Nostr-native protocol family for agent identity, capability discovery, escrow declaration, and swap lifecycle coordination.

This repository is the canonical landing page for the Minmo protocol and contains the `MIP` series: `Minmo Implementation Possibility` documents that define the protocol family.

## Terminology Note

In this repository, `Agent` refers to a Minmo protocol participant that publishes capabilities and can conduct swaps.

References to automation working on this repository are written explicitly as `AI agent`, `coding assistant`, or `repository automation` to avoid confusion with the protocol term.

## MIP Series

The MIPs are ordered by dependency and implementation priority.

Read `MIP-01` through `MIP-05` first for the minimum interoperable protocol core.

- [MIP-01-protocol-overview.md](./MIP-01-protocol-overview.md)
  - Implementation: `Informational`
  - overall architecture, shared conventions, privacy boundary, and open questions

- [MIP-02-agent-definition.md](./MIP-02-agent-definition.md)
  - Implementation: `Required`
  - public agent capability and discovery record

- [MIP-03-escrow-descriptor.md](./MIP-03-escrow-descriptor.md)
  - Implementation: `Required`
  - public escrow declaration referenced by agents and swaps

- [MIP-04-swap-state-machine.md](./MIP-04-swap-state-machine.md)
  - Implementation: `Required`
  - request, transition, evidence, dispute, note, and snapshot event lifecycle

- [MIP-05-dispute-policy.md](./MIP-05-dispute-policy.md)
  - Implementation: `Required`
  - dispute classes, timeout classes, evidence boundary, and resolution modes

- [MIP-06-wrapper-auth.md](./MIP-06-wrapper-auth.md)
  - Implementation: `Recommended`
  - local account wrappers, recovery, sessions, and API key ownership over canonical Nostr identity

- [MIP-07-automation-bridge.md](./MIP-07-automation-bridge.md)
  - Implementation: `Recommended`
  - validated translation of off-protocol automation inputs into public protocol evidence or transitions

- [MIP-08-operator-indexing.md](./MIP-08-operator-indexing.md)
  - Implementation: `Recommended`
  - relay ingestion, filtering, freshness, snapshots, and ranking overlays

- [MIP-09-reputation-attestations.md](./MIP-09-reputation-attestations.md)
  - Implementation: `Optional`
  - optional signed operator opinions about trust and performance

## Design Direction

Minmo is designed around a small set of protocol positions:

- Nostr pubkey is the canonical agent identity
- agent capabilities and discovery metadata are published on Nostr
- swaps are modeled as Nostr-native state machines
- operators may provide business, compliance, indexing, automation, and UX overlays without becoming the identity root

The practical inversion is:

- from `application account owns agent`
- to `Nostr identity is agent, application accounts wrap it`

## Implementation Baseline

The first interoperable implementation baseline is:

- [MIP-02-agent-definition.md](./MIP-02-agent-definition.md)
- [MIP-03-escrow-descriptor.md](./MIP-03-escrow-descriptor.md)
- [MIP-04-swap-state-machine.md](./MIP-04-swap-state-machine.md)
- [MIP-05-dispute-policy.md](./MIP-05-dispute-policy.md)

These define the public discovery model, escrow declaration model, swap event lifecycle, and dispute boundary needed for a usable Minmo-compatible implementation.

The remaining MIPs extend that core with operator-layer wrappers, automation, indexing, and portable reputation.

## Contribution

This repository is for protocol specification work, not application implementation.

Changes in this repository should remain:

- protocol-focused
- atomic by component
- free of implementation-repo details
- free of application-specific database or migration logic

When contributing:

1. Read this `README` first.
2. Read only the MIPs directly relevant to the requested change.
3. Keep one MIP as the primary source of truth for each rule.
4. Update related MIPs only where consistency requires it.
5. Update this `README` when adding a new MIP or local repository skill.

If a design is still unresolved, prefer documenting a draft convention or open question rather than implying false finality.

## Local Skills

This repository includes local skills for AI agents and coding assistants under [`.skills/`](/home/okj/minmoto/protocol/.skills).

Current skills:

- [`.skills/contribute-to-minmo-protocol/SKILL.md`](/home/okj/minmoto/protocol/.skills/contribute-to-minmo-protocol/SKILL.md)
  - use when editing or extending the MIP documents in this repository
- [`.skills/implement-minmo-protocol/SKILL.md`](/home/okj/minmoto/protocol/.skills/implement-minmo-protocol/SKILL.md)
  - use when implementing these specs independently in another repository or when producing an implementation plan

AI agent guidance:

- start with this `README`
- load the relevant local skill when the task is contribution or implementation
- read the smallest relevant subset of MIPs needed for the task
- preserve the distinction between canonical public protocol state and operator-layer overlays
- avoid introducing product-specific assumptions into protocol text

The repository is intentionally small. Humans and agents should preserve that property by avoiding auxiliary process documents unless explicitly needed.
