# 6. Pairing

## 6.1. Purpose

Pairing establishes persistent trust. Discovery and network reachability do not establish trust.

## 6.2. Initial flow

1. The Host enters an explicit, time-limited pairing mode.
2. It generates a cryptographically secure one-time pairing secret.
3. It displays a QR code or manual code.
4. The Client obtains the endpoint and certificate fingerprint.
5. The Client connects and verifies the Host fingerprint.
6. The Host validates the one-time secret and registers the Client.
7. The Host issues a device-specific credential.
8. The one-time secret is invalidated and pairing mode ends.

## 6.3. QR payload

```json
{
  "llp": "1.0",
  "type": "pairing",
  "host": "192.168.43.1",
  "port": 47832,
  "fingerprint": "sha256:REPLACE_WITH_REAL_FINGERPRINT",
  "pairing_secret": "ONE_TIME_SECRET"
}
```

The QR payload MUST NOT contain a long-lived device credential or private key. Pairing secrets MUST be single-use, short-lived, generated using a CSPRNG and protected against brute-force attempts.

## 6.4. Credentials and revocation

Each Client credential is unique and independently revocable. Credentials SHOULD be stored using the platform's secure storage. The Host MUST support revocation and MUST stop accepting a revoked credential.

Secrets and credentials MUST NOT be written to logs or diagnostic reports.
