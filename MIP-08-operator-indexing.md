# MIP-08: Operator Indexing

## Status

- Status: Draft
- Scope: operator-layer indexing, filtering, ranking, and snapshot behavior for Nostr-native protocol data
- Related:
  - [MIP-01-protocol-overview.md](./MIP-01-protocol-overview.md)
  - [MIP-04-swap-state-machine.md](./MIP-04-swap-state-machine.md)

## Purpose

This document defines how an operator should index, filter, rank, and expose protocol data that is published on Nostr.

## Core Position

An operator should act as a discovery and operating index, not as a second protocol.

That means:

- canonical public identity still comes from Nostr events
- canonical public swap history still comes from the Nostr event log
- operators may aggregate, rank, cache, filter, and annotate
- operators must not silently replace public state with operator-internal state

## Core Principles

1. indexing is interpretation, not authorship
2. freshness must be explicit
3. ranking is operator policy
4. snapshots are convenience only
5. relay fragmentation is expected

## Operator Index Model

An operator index should maintain at least four materialized views:

- agent discovery index
- swap timeline index
- snapshot cache
- ranking and policy overlay

## Ingestion Strategy

Operators SHOULD:

- subscribe to declared participant relays
- ingest public protocol events into a durable index
- backfill missing event chains when partial context appears later
- periodically reconcile index state against relay reads

## Freshness Model

Every indexed record should carry freshness metadata.

Recommended fields:

- `indexed_at`
- `observed_at`
- `latest_event_created_at`
- `latest_event_id`
- `relay_sources`
- `freshness_state`

Suggested `freshness_state` values:

- `fresh`
- `lagging`
- `stale`
- `partial`
- `unknown`

## Relay Conflict Resolution

Recommended rules:

1. immutable event ids win over derived cache state
2. for replaceable events, choose the newest valid event by Nostr semantics
3. when sequence coherence fails, downgrade confidence rather than inventing state
4. preserve conflicting observations in operator audit data
5. surface partial or stale status instead of pretending completeness

## Ranking Model

Ranking is an operator overlay over public discovery data.

Operators may rank using:

- completion rate
- dispute rate
- recent activity
- response speed
- declared liquidity confidence
- operator trust or moderation status
- business-specific priorities

Rankings should be presented as operator policy, not canonical protocol truth.
