# LegacyLink Protocol (LLP)

An open, capability-negotiated protocol for connecting devices across platforms and operating-system generations.

**Status:** Draft 0.1.0 — actively evolving; not yet a stable 1.0 specification.

## Goals

- Connect independent devices through a secure, discoverable session.
- Use a hybrid transport: persistent TCP+TLS for control, HTTPS for bulk data.
- Use UTF-8 JSON for control messages.
- Negotiate capabilities instead of assuming platform features.
- Make legacy-platform limitations explicit and testable.

## Architecture at a glance

| Layer | Initial profile |
|---|---|
| Discovery | DNS-SD/mDNS; manual IP or QR fallback |
| Control transport | TCP + TLS |
| Control framing | 4-byte unsigned big-endian length prefix |
| Control format | UTF-8 JSON |
| Data plane | HTTP/1.1 over TLS |
| Service model | Capability-negotiated services and actions |

## Documents

- [Architecture](specification/01-architecture.md)
- [Transport](specification/02-transport.md)
- [Framing](specification/03-framing.md)
- [Message format](specification/04-message-format.md)
- [Handshake and capabilities](specification/05-handshake.md)
- [Pairing](specification/06-pairing.md)
- [Security](specification/07-security.md)
- [Compatibility and versioning](specification/08-compatibility.md)
- [Errors](specification/09-errors.md)
- [Service overview](services/README.md)

## Planned implementations

- **LegacyLink Host** — Android application.
- **LegacyLink Client** — legacy iOS application, initially targeting iPhone 4s / iOS 8.4.1.
- Independent third-party implementations are welcome.

The protocol is not restricted to Android and iOS. These are the first reference targets only.

## Important platform distinction

A service definition is a protocol contract, not a guarantee that every OS exposes the required native API. For example, sending SMS through an Android Host and displaying it in a custom iOS Client is not the same as integrating with Apple's stock Messages app. Initiating a cellular call does not imply access to cellular call audio.

## Conformance language

The words **MUST**, **MUST NOT**, **REQUIRED**, **SHOULD**, **SHOULD NOT**, and **MAY** are normative requirements.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Until LLP 1.0, wire-level details may change. Implementations should pin the exact draft revision they target.
