# 5. Handshake and capabilities

## 5.1. Sequence

After TCP and TLS are established, peers exchange:

1. `hello`
2. `hello_ack`
3. `capabilities`
4. `capabilities_ack`
5. `session_ready`
6. `session_ready_ack`

The session is CONNECTED only after the final acknowledgement.

## 5.2. HELLO

The initiating peer declares its implementation, device metadata and supported protocol versions.

```json
{
  "llp": "1.0",
  "type": "control",
  "id": "hello-001",
  "action": "hello",
  "payload": {
    "implementation": "LegacyLink-iOS-Legacy",
    "implementation_version": "0.1.0",
    "device": {
      "id": "client-uuid",
      "name": "iPhone 4s",
      "platform": "ios",
      "os_version": "8.4.1"
    },
    "supported_protocol_versions": ["1.0"]
  }
}
```

Implementations SHOULD avoid exposing hardware serial numbers or other sensitive identifiers.

## 5.3. HELLO_ACK

```json
{
  "llp": "1.0",
  "type": "control",
  "id": "hello-ack-001",
  "action": "hello_ack",
  "payload": {
    "accepted": true,
    "host": {
      "id": "host-uuid",
      "name": "Android Host",
      "platform": "android"
    },
    "selected_protocol_version": "1.0",
    "session_id": "session-uuid"
  }
}
```

If no common protocol version exists, the peer MUST reject the handshake with `UNSUPPORTED_VERSION`.

## 5.4. Capabilities

Each peer advertises available services and actions. Example:

```json
{
  "llp": "1.0",
  "type": "control",
  "id": "caps-001",
  "action": "capabilities",
  "payload": {
    "services": {
      "messaging": {
        "available": true,
        "actions": ["send", "get_conversations", "get_history"]
      },
      "telephony": {
        "available": true,
        "actions": ["start_call", "get_call_state"],
        "limitations": ["call_audio_bridge_not_supported"]
      }
    },
    "max_control_message_bytes": 1048576,
    "data": {
      "http_version": "1.1",
      "max_transfer_bytes": 104857600
    }
  }
}
```

Capabilities are runtime declarations. Availability may depend on permissions, hardware, OS, carrier restrictions or current state.

## 5.5. Session state

`DISCONNECTED → CONNECTING → AUTHENTICATING → HANDSHAKING → NEGOTIATING → CONNECTED`

A transport failure moves the session to RECONNECTING or DISCONNECTED. Reconnection requires authentication and a new handshake.
