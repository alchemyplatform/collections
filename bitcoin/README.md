# Bitcoin Collection

A comprehensive Bruno collection for Bitcoin Core RPC and Alchemy UTXO Indexer REST API requests.

## Overview

This collection contains **16 Bitcoin Core RPC methods** and **12 UTXO Indexer REST endpoints** covering blockchain operations, address/UTXO queries, balance history, and ticker data.

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

## Environment Configuration

The collection includes Bitcoin-specific environments:

- **Bitcoin-Mainnet**: `http://localhost:8332` (Bitcoin Core mainnet)
- **Bitcoin-Testnet**: `http://localhost:18332` (Bitcoin Core testnet)
- **Bitcoin-Regtest**: `http://localhost:18443` (Bitcoin Core regtest)

## Authentication

**Bitcoin Core RPC** requires HTTP Basic Authentication:

1. Configure `rpcUser` and `rpcPassword` in your environment
2. These correspond to `rpcuser` and `rpcpassword` in your `bitcoin.conf`

**UTXO Indexer REST API** uses the Alchemy API key embedded in the URL.

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
