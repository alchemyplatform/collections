# HyperCore gRPC Collection

A Bruno collection for the HyperCore (Hyperliquid) gRPC block stream
(`streams.v1.BlockStream`), served through Alchemy.

## Endpoints

| Network | URL |
|---------|-----|
| Mainnet | `https://hypercore-mainnet.g.alchemy.com/` |

## Auth

All requests send your Alchemy API key as gRPC metadata:

```
X-Token: <api_key>
```

Set `api_key` in your Bruno environment (a global environment shared across
collections works well — see the repo README).

## Protos

The gateway does not expose gRPC server reflection, so this collection bundles
the proto under `grpc/proto/`. The entrypoint is
`grpc/proto/streams/v1/blocks.proto`; `grpc/proto` is registered as the import
path in `bruno.json`.

## Requests

### grpc (`streams.v1.BlockStream`)

- `StreamBlocks` — live tail of raw execution blocks from the current tip.
- `StreamBlocks (replay)` — resume from `start_block` (inclusive), then follow
  the live stream. Only the last ~64 blocks (a few seconds of mainnet) are
  retained, so this is for reconnecting clients rather than history; older
  heights end the stream with `NOT_FOUND`.

Each `BlockMessage` carries a sequential `block_number` and `data`, the raw
`replica_cmds` block JSON exactly as the node wrote it. Protobuf JSON encodes
`bytes` as base64, so decode `data` to read the block:

```bash
echo <data> | base64 -d | jq
```

## Stream termination

Gaps end the stream with a gRPC status instead of an in-band message:

| Status | Meaning |
|--------|---------|
| `NOT_FOUND` | `start_block` is older than the retained window |
| `ABORTED` | The client fell behind the live stream |
| `UNAVAILABLE` | The feed is not ready or the server is draining |

Reconnect with `start_block` set to the last `block_number` you received.
