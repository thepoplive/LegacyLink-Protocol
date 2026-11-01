# 2. Transport

## 2.1. Control transport

The initial profile uses TCP with TLS.

- The Host listens on a configurable TCP port.
- The default port convention is **47832**.
- The Client establishes an outbound connection.
- Multiple LLP messages share one connection.
- Implementations MUST handle connection loss and reconnection.

The default port is not authoritative; discovery or manual configuration supplies the actual endpoint.

## 2.2. TLS

The main profile requires TLS 1.2 or newer; TLS 1.3 is preferred when both peers support it.

Peers MUST validate certificates. For a locally paired Host using a self-signed certificate, the fingerprint MUST be verified during pairing and pinned for subsequent sessions. Disabling certificate validation is not an acceptable workaround.

Older OS releases may not support the main profile. Implementations MUST test the actual TLS stack, certificate validation behavior and cipher support before claiming compatibility. A weaker legacy profile is not defined in this draft and MUST NOT be silently substituted.

## 2.3. Data transport

Bulk data uses HTTP/1.1 over TLS. HTTP/1.1 is the baseline for older platform compatibility. HTTP/2 MAY be added in a later profile.

The Host advertises the data-plane endpoint during session negotiation. It MAY share the control port only if the implementation explicitly supports both protocols on that endpoint.

## 2.4. Lifecycle

A session SHOULD remain open while the application is active. Either peer MAY close it. Reconnection MUST repeat authentication and the LLP handshake; a TCP connection alone does not establish an LLP session.
