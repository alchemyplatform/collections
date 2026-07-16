# TRON gRPC Collection

A Bruno collection for TRON's native gRPC API (`protocol.Wallet` and
`protocol.WalletSolidity` services), served through Alchemy.

## Endpoints

| Network | URL |
|---------|-----|
| Mainnet | `https://tron-mainnet.g.alchemy.com/` |
| Nile testnet | `https://tron-testnet.g.alchemy.com/` |

## Auth

All requests send your Alchemy API key as gRPC metadata:

```
X-Token: <api_key>
```

Set `api_key` in your Bruno environment (a global environment shared across
collections works well — see the repo README).

## Protos

The gateway does not expose gRPC server reflection, so this collection bundles
the real TRON protos under `grpc/proto/` (unmodified, from
[tronprotocol/protocol](https://github.com/tronprotocol/protocol)). The
entrypoint is `grpc/proto/api/api.proto`; `grpc/proto` is registered as the
import path in `bruno.json`.

## Bytes fields (addresses, txids, call data)

Protobuf's JSON mapping encodes `bytes` fields as **base64 of the raw bytes** —
not hex, not base58. To convert a TRON address:

```bash
# from the 21-byte hex form (starts with 41):
echo 41E552F6487585C2B58BC2C9BB4492BC1F17132CD0 | xxd -r -p | base64
# => QeVS9kh1hcK1i8LJu0SSvB8XEyzQ
```

For a base58 `T...` address, base58check-decode it first (the payload is the
21-byte `41...` form). Transaction IDs are the raw 32 bytes, base64-encoded.

## Requests

### wallet (`protocol.Wallet` — latest state)

Account: `GetAccount`, `GetAccountResource`, `GetAccountNet`

Blocks: `GetNowBlock2`, `GetBlock`, `GetBlockByNum2`, `GetBlockByLatestNum2`,
`GetTransactionCountByBlockNum`

Transactions: `GetTransactionById`, `GetTransactionInfoById`,
`GetTransactionInfoByBlockNum`, `CreateTransaction2`, `BroadcastTransaction`

Smart contracts: `TriggerConstantContract`, `TriggerContract`,
`EstimateEnergy`, `GetContract`, `GetContractInfo`

Staking (Stake 2.0): `FreezeBalanceV2`, `UnfreezeBalanceV2`,
`DelegateResource`, `GetDelegatedResourceV2`

Network: `GetChainParameters`, `GetNodeInfo`, `GetEnergyPrices`,
`GetBandwidthPrices`, `ListWitnesses`, `TotalTransaction`, `GetBurnTrx`

### walletsolidity (`protocol.WalletSolidity` — confirmed state)

`GetAccount`, `GetNowBlock2`, `GetBlock`, `GetBlockByNum2`,
`GetTransactionById`, `GetTransactionInfoById`,
`GetTransactionInfoByBlockNum`, `TriggerConstantContract`, `GetBurnTrx`

The full method surface enabled on Alchemy is larger (most of the
`protocol.Wallet` / `protocol.WalletSolidity` unary methods); any method in
`api.proto` can be called by duplicating a request and changing `method` and
the body.

## Write flow

TRON write methods return **unsigned** transactions. The flow is:

1. Build the transaction (`CreateTransaction2`, `TriggerContract`,
   `FreezeBalanceV2`, ...).
2. Sign the returned `raw_data` locally (e.g. with TronWeb — never send a
   private key to the API).
3. Submit the signed transaction with `BroadcastTransaction`.
