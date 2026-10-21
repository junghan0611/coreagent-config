# coreagent-config

Minimal server-side identity and connection core, paired with [homeagent-config](https://github.com/junghan0611/homeagent-config) and [edgeagent-config](https://github.com/junghan0611/edgeagent-config).

## Purpose

Keep the connection structure small: authenticate a device, establish what it may access, and maintain its connection. The intended deployment can be a personal/SOHO installation or a small server business; no particular cloud is required.

**Status: scope and documentation only.** No server implementation, deployment package, or technology stack has been selected here.

## Repository boundaries

| Repository | Intended responsibility |
|---|---|
| **coreagent-config** | Server-side authentication, registration, ownership and authorization; connection, reconnection and credential revocation; reproducible server packaging. |
| **homeagent-config** | Hub boot, network/time readiness, device provisioning, radio/protocol services and the server connection client, packaged across updates and recovery. Server-side account and ownership authority stays with coreagent. |
| **edgeagent-config** | Small-node hardware-independent state, self-description and message contracts, as defined by that repository's own documents. This coordination does not change its contracts. |

These are responsibility boundaries, not claims of implemented features. Business logic and a general account platform are not the starting point.

## Connection shape

A Hub may connect to the server on behalf of a local installation. Whether an Edge connects directly, through a Hub, or both remains open. An authenticated Hub does not by itself prove the independent identity of every downstream Edge.

A NodeCard is self-description, not authentication evidence. Binding a node identifier to an authenticated principal must be explicit.

Before implementation, settle who issues initial credentials, who may claim/transfer/release a device, and what revocation blocks for existing sessions and subsequent connections.

## Proposed first joint check

On a host, use one fake Hub to observe authentication → registration/authorization → permitted message exchange → disconnection/reconnection → credential revocation. Check that unregistered principals and principals without permission to the target are denied access, and that a revoked principal cannot keep using its session or reconnect.

This is a proposed verification slice, not a passing result or an implementation commitment. It covers Hub-to-server connectivity only, not downstream Edge authentication.
