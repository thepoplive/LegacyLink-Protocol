# 8. Compatibility and versioning

## 8.1. Protocol version

The `llp` field identifies the negotiated wire protocol version and is independent of application version. This repository revision is draft 0.1.0; examples use the provisional wire version `1.0`.

## 8.2. Capability negotiation

Peers MUST negotiate capabilities at session setup. A Client MUST NOT infer service availability from a platform name or OS version.

A service may be unavailable, partially available, limited, or temporarily unavailable due to permissions or device state.

## 8.3. Unknown fields and actions

Unknown optional fields MUST be ignored. Unknown mandatory features MUST fail explicitly. An unknown action MUST NOT be silently mapped to another action.

## 8.4. Platform-specific behavior

A service definition describes a protocol contract, not a promise that every OS exposes a native API. Sending SMS through an Android Host and displaying it in a custom iOS Client is distinct from integration with the stock iOS Messages app.

Likewise, initiating a cellular call does not imply access to cellular call audio.

## 8.5. Version changes

Optional additions may be backward-compatible when older peers can safely ignore them. Changing framing, field meaning or mandatory behavior requires an incompatible protocol version.

Implementations SHOULD publish tested OS versions, supported services/actions, security profile, known limitations and size limits.
