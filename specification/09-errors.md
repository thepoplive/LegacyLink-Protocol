# 9. Errors

## 9.1. Error envelope

```json
{
  "llp": "1.0",
  "type": "error",
  "id": "request-001",
  "error": {
    "code": "SERVICE_UNAVAILABLE",
    "message": "Requested service is unavailable",
    "retryable": false
  }
}
```

## 9.2. Fields

- `code`: stable machine-readable identifier.
- `message`: human-readable diagnostic; clients MUST NOT parse it for control flow.
- `retryable`: whether retrying may succeed without changing parameters or permissions.

An error responding to a request MUST echo that request's ID.

## 9.3. Initial codes

| Code | Meaning |
|---|---|
| `INVALID_MESSAGE` | Malformed or invalid LLP message |
| `UNSUPPORTED_VERSION` | No mutually supported version |
| `UNSUPPORTED_SERVICE` | Unknown service |
| `SERVICE_UNAVAILABLE` | Known service currently unavailable |
| `UNSUPPORTED_ACTION` | Action not implemented by this peer |
| `UNAUTHORIZED` | Caller is not authorized |
| `PAIRING_REQUIRED` | Pairing is required |
| `PAIRING_EXPIRED` | One-time pairing data expired |
| `INVALID_REQUEST` | Payload validation failed |
| `REQUEST_TIMEOUT` | Operation timed out |
| `RATE_LIMITED` | Rate limit exceeded |
| `TRANSFER_FAILED` | Data transfer failed |
| `INTERNAL_ERROR` | Unexpected implementation error |

## 9.4. Retry safety

Peers SHOULD retry only when `retryable` is true and the operation is safe to repeat. Non-idempotent operations such as sending SMS or initiating calls MUST NOT be blindly retried after an ambiguous timeout. Service definitions should specify idempotency behavior.
