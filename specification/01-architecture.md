# 1. Architecture

## 1.1. Roles

A **Host** exposes services. A **Client** discovers or connects to a Host and invokes those services. Roles describe a session, not a permanent device identity; a future implementation MAY support both roles.

The first reference scenario is an Android Host paired with an older iPhone Client. LLP itself is platform-neutral.

## 1.2. Protocol planes

### Control plane

Small structured messages: requests, responses, events, errors, authentication, negotiation and session control. The initial profile uses one persistent TCP connection protected by TLS.

### Data plane

Large payloads such as files and media. The initial profile uses HTTP/1.1 over TLS. Control messages create and authorize transfers; bulk bytes SHOULD NOT be embedded as base64 in JSON control messages.

## 1.3. Layers

1. Discovery — DNS-SD/mDNS or manual endpoint exchange.
2. Secure transport — TCP protected by TLS.
3. Framing — four-byte length prefix.
4. Control encoding — UTF-8 JSON.
5. Session protocol — handshake, authentication, negotiation and request lifecycle.
6. Services — device, network, messaging, telephony, contacts, notifications, files, media and audio.

## 1.4. Capability model

Each peer advertises only the services and actions it can currently provide. Availability may depend on OS version, permissions, hardware, carrier policy or device state.

A service being defined by LLP does not imply that every implementation supports it.

## 1.5. Discovery is not trust

Discovery returns a candidate endpoint and public metadata only. A discovered device MUST NOT be treated as paired or authenticated until pairing and authentication succeed.
