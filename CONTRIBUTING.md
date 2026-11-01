# Contributing

LLP is an evolving protocol draft. Reviews, issue reports, test vectors and independent implementations are welcome.

## Proposing a change

1. Describe the interoperability problem.
2. Explain impact on existing implementations and older operating systems.
3. Include request/response/event examples for wire-format changes.
4. Update the relevant specification and service documents.
5. Add test vectors for framing, validation, negotiation or state-machine changes.

## Compatibility principles

- Prefer optional additions over changing existing field meanings.
- Unknown optional fields should be ignored.
- Do not silently reinterpret an unknown action.
- Breaking changes to mandatory behavior require an incompatible protocol version.
- Declare platform limitations honestly.

## Security

Never commit real pairing secrets, access tokens, private keys, personal data or production device identifiers. Use synthetic examples.
