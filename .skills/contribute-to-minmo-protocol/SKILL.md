---
name: contribute-to-minmo-protocol
description: Use when updating or adding Minmo protocol MIPs in this repository. Follow the repository's protocol-only writing rules, preserve atomic spec boundaries, keep implementation details out, and maintain consistency across the MIP series.
---

# Contribute To Minmo Protocol

Use this skill when the task is to edit this repository's protocol documents rather than build an application.

## Terminology Guardrail

In protocol text, `Agent` refers to the Minmo protocol participant defined by the MIP series.

When writing repository-facing or tooling-facing text, use explicit terms like `AI agent`, `coding assistant`, or `repository automation` instead of using `agent` by itself.

## Scope

This repository is for protocol documents only. Keep changes:

- protocol-focused
- atomic by component
- free of implementation-repo details
- free of application-specific database or migration logic

Do not add product plans, SDK instructions, deployment notes, or backend schema proposals unless the user explicitly asks for protocol text that requires them.

## Repository Shape

Read [README.md](../../README.md) first, then only the MIPs directly relevant to the task.

Current series and intent:

- `MIP-01`: architecture and shared conventions
- `MIP-02`: Minmo agent definition
- `MIP-03`: escrow descriptor
- `MIP-04`: swap state machine
- `MIP-05`: dispute policy
- `MIP-06`: wrapper auth
- `MIP-07`: automation bridge
- `MIP-08`: operator indexing
- `MIP-09`: reputation attestations

## Editing Rules

Preserve each MIP's basic structure unless the task clearly requires a structural change:

- title
- status
- purpose
- protocol-specific sections
- related links

When adding a new MIP:

1. Choose the next `MIP-XX` number.
2. Add a clear title with one narrow concern.
3. Mark implementation level consistently: `Informational`, `Required`, `Recommended`, or `Optional`.
4. Link dependencies and related MIPs explicitly.
5. Update [README.md](../../README.md) so the series ordering stays correct.

## Consistency Checks

Before finishing, verify:

- event kinds and tags do not conflict with existing draft allocations
- the privacy boundary matches `MIP-01`
- new normative statements do not silently contradict related MIPs
- required/recommended/optional language matches the intended implementation burden
- cross-links point to real files

If a change affects swap lifecycle semantics, also review:

- [MIP-04-swap-state-machine.md](../../MIP-04-swap-state-machine.md)
- [MIP-05-dispute-policy.md](../../MIP-05-dispute-policy.md)

If a change affects discovery or public declarations, also review:

- [MIP-02-agent-definition.md](../../MIP-02-agent-definition.md)
- [MIP-03-escrow-descriptor.md](../../MIP-03-escrow-descriptor.md)

## Writing Style

Prefer:

- short declarative sections
- explicit protocol boundaries
- stable terminology across files
- explicit `Minmo agent` phrasing on first mention when ambiguity is possible
- open questions only when the design is genuinely unresolved

Avoid:

- speculative product UX
- hidden assumptions about one operator or app
- implementation pseudocode unless the user asks for it
- duplicating the same rules across multiple MIPs without a reason

## Change Strategy

When the requested change spans multiple documents:

1. Update the most canonical MIP first.
2. Propagate only the minimum supporting edits to related MIPs.
3. Keep the source of truth obvious.

If a proposal is still immature, prefer adding a short `Open Question` or draft convention note instead of pretending the design is final.
