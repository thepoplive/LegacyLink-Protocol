# 4. Message format

## 4.1. Envelope

Every control message is a JSON object.

```json
{
  "llp": "1.0",
  "type": "request",
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "service": "device",
  "action": "get_info",
  "timestamp": "2026-11-01T12:00:00Z",
  "payload": {}
}
```

## 4.2. Fields

| Field | Requirement | Meaning |
|---|---|---|
| `llp` | Required | Negotiated protocol version |
| `type` | Required | Message class |
| `id` | Required | Unique message identifier |
| `service` | Service messages | Service identifier |
| `action` | Requests | Requested operation |
| `timestamp` | Recommended | UTC timestamp in RFC 3339 form |
| `payload` | Required | Message-specific JSON object |

Initial `type` values: `request`, `response`, `event`, `error`, `control`.

## 4.3. IDs and lifecycle

The `id` SHOULD be a UUID string. A response MUST echo the request ID. An event has its own ID and does not respond to a request.

A request receives at most one final response or error. Long-running operations SHOULD return an operation identifier, then emit progress events. Events are not final responses.

## 4.4. JSON rules

- UTF-8 encoding is REQUIRED.
- Object keys are case-sensitive.
- Binary payloads SHOULD use the data plane, not base64 in control messages.
- Unknown optional fields MUST be ignored.
- Invalid values for understood fields MUST be rejected.

## 4.5. Event ordering

Events SHOULD include a monotonically increasing `event_sequence` scoped to the session. Sequence gaps can indicate missed events. Timestamps are informational and MUST NOT be the sole ordering mechanism.
