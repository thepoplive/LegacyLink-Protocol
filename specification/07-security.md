# 7. Security considerations

## 7.1. Threat model

A local network may contain untrusted devices; discovery packets may be observed or spoofed. A device name, IP address, QR code or successful TCP connection is not proof of identity.

## 7.2. Required controls

Implementations:

- MUST use TLS 1.2 or newer in the main profile.
- MUST validate peer certificates.
- MUST verify and pin a self-signed Host certificate fingerprint during pairing.
- MUST use cryptographically secure randomness for secrets and tokens.
- MUST scope credentials to a paired device and support revocation.
- MUST rate-limit pairing and authentication attempts.
- MUST validate frame sizes and payload schemas.
- MUST authorize individual service actions.
- MUST avoid logging credentials, pairing secrets and private message content.

## 7.3. Legacy platform warning

This draft does not claim that every legacy iOS release can meet the main TLS profile. Implementations must test the actual OS networking stack, certificate validation and cipher support.

A weaker legacy profile is not defined here. Implementations MUST NOT silently disable certificate validation or downgrade security. Any future legacy profile requires a separate threat analysis and explicit documentation.

## 7.4. Least privilege and data minimization

The Host SHOULD expose only user-enabled services. Transfer tokens SHOULD be short-lived and scoped to one transfer and direction. Implementations SHOULD minimize retained personal data and provide a way to clear local pairing data.
