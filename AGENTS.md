# AGENTS.md — coreagent-config

## Purpose and current phase

This is the public server-side identity and connection counterpart to `homeagent-config` and `edgeagent-config`. Keep the structure small enough for a personal/SOHO installation or a small server operator, without requiring a particular cloud.

**Documentation phase. GLG explicitly said on 2026-10-21 that this round produces no code.** Do not create a runtime scaffold, sample service, dependency manifest, deployment configuration or test implementation without a new request. A proposed verification is not permission to implement it.

Read `README.md` first. It owns the public scope and connection shape; this file owns agent operating boundaries. Keep them consistent rather than duplicating a detailed design here.

## Responsibility boundaries

- **Core:** server-side authentication, registration, ownership/authorization, connection/reconnection and credential revocation, plus eventual reproducible server packaging. These are intended responsibilities, not implemented capabilities.
- **Home:** hub BSP/vendor base, radio/protocol services, and packaging the connection client and hub services across boot, network/time readiness, provisioning, updates and recovery. It does not become a second authority for server accounts or ownership.
- **Edge:** small-node state, self-description and message contracts. Its own repository documents are authoritative; Home/Core agreement does not constitute Edge maintainer approval.
- Business logic and a general account platform are not the starting point. Do not grow them as prerequisites for connectivity.

Each maintainer edits their own repository. Route cross-repository checkpoints and contract changes through the coordinator GLG appoints; this repository's maintainer is not automatically the initiative coordinator. Contact or open siblings only within GLG's authorization.

## Contract discipline

- A NodeCard is self-description, not authentication evidence.
- An authenticated Hub does not independently authenticate every downstream Edge.
- Edge-to-Hub-to-Core is a possible topology, not a mandatory route. Direct Edge connections remain undecided.
- Explicitly distinguish an authenticated principal, a node identifier, ownership and permission to a target. Do not silently treat them as equivalent.
- Initial credential issuance, registration/claim authority, ownership transfer/release, revocation scope and transport remain open. Do not turn a candidate into a decision by writing deployment instructions for it.
- No broker, certificate tooling, protocol or cloud stack has been selected. Earlier research suggestions are candidates only.

The first joint verification described in `README.md` is **proposed and unexecuted**: one fake Hub, authentication/authorization and permitted exchange, disconnect/reconnect, then revocation blocking both continued session use and reconnects; also deny unregistered and unauthorized principals. It would establish only the Hub–server boundary, not downstream Edge authentication. Settle credential and authorization rules before implementing that check.

## Public boundary and evidence

This repository is a fresh public space, not a migration of an earlier private repository. Do not copy private history, vendor/company material, credentials, device keys or business logic into it. Consult only sources appropriate for public documentation; do not use private material as a template to sanitize later.

When exchanging claims with peers, attach their evidence state: directly read source and location, measured command/result, or a named inherited source not yet verified. Keep design proposals separate from observed behavior. Never describe README agreement, a fake peer or a passing format check as live device/security proof.

Useful public sources:

- [Home README](https://github.com/junghan0611/homeagent-config/blob/main/README.md) — current hub scope and Home/Core boundary.
- [Home issue #8](https://github.com/junghan0611/homeagent-config/issues/8) — hub product-packaging discussion; read the latest thread before relying on its scope.
- [Edge README](https://github.com/junghan0611/edgeagent-config/blob/main/README.md) and its linked contracts — node self-description and message boundaries.

## Change and verification gates

Make small documentation edits and run `git diff --check`; inspect the diff for unsupported claims and private information. Do not touch sibling work or unrelated dirty files.

README coordination does not authorize implementation, board modification, commit or push. Follow the commit skill if GLG requests a commit; push requires GLG's explicit request. No release or technology adoption is implied by this document.
