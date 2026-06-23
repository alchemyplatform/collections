# Bitcoin Collection

A comprehensive Bruno collection for Bitcoin Core RPC, Alchemy UTXO Indexer REST API, and UTXO WebSocket subscriptions.

## Overview

This collection contains **16 Bitcoin Core RPC methods**, **12 UTXO Indexer REST endpoints**, and **4 UTXO WebSocket subscriptions** covering blockchain operations, address/UTXO queries, balance history, and ticker data.

## Available Methods (16)

### Blockchain RPCs (4)

- `getbestblockhash` - Get the hash of the best block
- `getblock` - Get block information by hash
- `getblockcount` - Get current blockchain height
- `getblockchaininfo` - Get comprehensive blockchain state info

### Network RPCs (3)

- `getnetworkinfo` - Get P2P networking information
- `getpeerinfo` - Get data about connected peers
- `getconnectioncount` - Get number of peer connections

### Raw Transaction RPCs (3)

- `getrawtransaction` - Get raw transaction data by txid
- `sendrawtransaction` - Broadcast a raw transaction
- `decoderawtransaction` - Decode a raw transaction hex

### Mining RPCs (2)

- `getmininginfo` - Get mining-related information
- `getblocktemplate` - Get block template for mining

### Mempool RPCs (2)

- `getmempoolinfo` - Get memory pool statistics
- `getrawmempool` - Get all transactions in mempool

### Utility RPCs (2)

- `estimatesmartfee` - Estimate transaction fees
- `validateaddress` - Validate Bitcoin addresses

## Indexer REST API (12)

### Block Endpoints (2)

- `get_block_hash` - Get block hash by block height
- `get_block` - Get block data by hash or height

### Transaction Endpoints (3)

- `get_transaction` - Get normalized transaction by txid
- `get_transaction_specific` - Get transaction in native node format by txid
- `send_transaction_get` / `send_transaction_post` - Broadcast a signed raw transaction

### Address & UTXO Endpoints (3)

- `get_address` - Get balance and transaction history for an address
- `get_xpub` - Get aggregated balance and history for an extended public key
- `get_utxos` - Get unspent transaction outputs for an address or xpub

### Market Data Endpoints (3)

- `get_tickers_list` - Get list of supported fiat currency tickers
- `get_tickers` - Get current Bitcoin exchange rates
- `get_balance_history` - Get balance history over time for an address or xpub

## Indexer WebSockets (4)

Stream block, transaction, address, and fiat rate updates over a persistent WebSocket connection. Uses the same Alchemy API key and host as the REST indexer (`wss://bitcoin-mainnet.g.alchemy.com/v2/{apiKey}`).

### Subscriptions (4)

- `subscribe_new_block` - Emits when a new block is added to the chain
- `subscribe_new_transaction` - Emits every new transaction across all addresses (high volume; may not be enabled on all networks)
- `subscribe_addresses` - Emits when a transaction touches watched addresses
- `subscribe_fiat_rates` - Emits when fiat rate tickers update

### Request methods (over WebSocket)

The same WebSocket connection also accepts one-shot request methods using the same message envelope (`id`, `method`, `params`). These are useful when you already have an open connection for subscriptions and want to fetch data without a separate HTTP call. Many mirror the indexer REST endpoints above; others are WebSocket-only.

- `getInfo` - Backend and Blockbook status
- `getBlockHash` - Block hash for a given height
- `getAccountInfo` - Balances and transactions for an address or xpub
- `getAccountUtxo` - UTXOs for an address or xpub
- `getTransaction` - Normalized transaction data
- `getTransactionSpecific` - Coin-specific raw transaction
- `getBalanceHistory` - Address balance history over time
- `estimateFee` - Fee estimate for a target confirmation depth
- `sendTransaction` - Broadcast a signed raw transaction
- `getCurrentFiatRates` - Current fiat exchange rates
- `getFiatRatesTickersList` - Available fiat tickers for a timestamp
- `getFiatRatesForTimestamps` - Historical fiat rates for specific timestamps
- `getMempoolFilters` - Compact block filters for the mempool
- `getBlockFilter` - Compact block filter for a given block
- `ping` - Connection health check

See the [UTXO WebSockets docs](https://www.alchemy.com/docs/bitcoin/utxo-websockets) for message format and payload details.

## Environment Configuration

The collection includes Bitcoin-specific environments:

- **Bitcoin-Mainnet**: `http://localhost:8332` (Bitcoin Core mainnet)
- **Bitcoin-Testnet**: `http://localhost:18332` (Bitcoin Core testnet)
- **Bitcoin-Regtest**: `http://localhost:18443` (Bitcoin Core regtest)

## Authentication

**Bitcoin Core RPC** requires HTTP Basic Authentication:

1. Configure `rpcUser` and `rpcPassword` in your environment
2. These correspond to `rpcuser` and `rpcpassword` in your `bitcoin.conf`

**UTXO Indexer REST API and WebSockets** use the Alchemy API key embedded in the URL.

## Usage

1. Open this collection in Bruno
2. Select a Bitcoin environment (Mainnet, Testnet, or Regtest)
3. Configure your RPC credentials in the environment variables
4. Execute requests to interact with your Bitcoin node

## Usage Notes

- Bitcoin uses JSON-RPC 1.0 (not 2.0 like Ethereum)
- Replace sample transaction hashes and block hashes with real values
- Some methods require `txindex=1` in bitcoin.conf for full functionality
- Regtest environment is ideal for development and testing

---

Based on the official [Bitcoin Core RPC API Reference](https://developer.bitcoin.org/reference/rpc/).
