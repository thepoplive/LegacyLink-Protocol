# LLP services

Services define interoperable operations exposed by a Host or Client. A service is available only when the peer advertises it during capability negotiation.

| Service | Example actions | Example events |
|---|---|---|
| `device` | `get_info`, `get_status` | `status_changed` |
| `network` | `get_status`, `get_hotspot_info` | `network_changed` |
| `messaging` | `send`, `get_conversations`, `get_history` | `message_received`, `message_status` |
| `telephony` | `start_call`, `get_call_state`, `end_call` | `incoming_call`, `call_state_changed` |
| `contacts` | `list`, `get`, `sync` | `contact_changed` |
| `notifications` | `list`, `dismiss` | `notification_received` |
| `files` | `create_transfer`, `cancel_transfer` | `transfer_progress`, `transfer_completed` |
| `media` | `list`, `get_metadata` | `media_changed` |
| `audio` | `start_stream`, `stop_stream` | `stream_state_changed` |

These names are an initial catalogue, not finalized payload schemas. Each service will receive a dedicated specification before being considered stable.

## Platform notes

- SMS sent by an Android Host is presented in the LegacyLink Client UI; this does not imply writing into the stock iOS Messages database or app.
- Cellular call initiation does not imply call-audio capture or routing.
- Audio streaming is a separate capability and does not grant access to system cellular call audio.
- Permissions and OS restrictions must be reflected in runtime capabilities.
