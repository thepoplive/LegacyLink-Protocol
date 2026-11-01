# 3. Control framing

## 3.1. Frame layout

Each control message is transmitted as:

| Field | Size | Description |
|---|---:|---|
| Length | 4 bytes | Unsigned big-endian body length |
| Body | N bytes | UTF-8 JSON object |

The length excludes the four-byte header.

## 3.2. Limits

- Maximum body size: **1,048,576 bytes (1 MiB)**.
- Zero-length bodies are invalid.
- A receiver MUST reject a declared length above its configured or negotiated maximum before allocating the body.
- A sender MUST respect the peer's advertised receive limit.

## 3.3. TCP stream behavior

TCP is a byte stream. A receiver MUST read exactly four bytes for the header, decode the length, then read exactly N body bytes. A single socket read is not guaranteed to contain one complete frame; a frame may be split across reads, and multiple frames may arrive together.

## 3.4. Validation

The body MUST be valid UTF-8 and contain exactly one valid JSON value whose top-level type is an object. Invalid UTF-8, malformed JSON, empty frames and oversized frames MUST be rejected.

After a framing violation, the receiver SHOULD close the connection because the next frame boundary may no longer be trustworthy.

## 3.5. Example

A body length of 74 bytes is prefixed by the bytes:

`00 00 00 4A`

The next 74 bytes are the UTF-8 JSON body.
