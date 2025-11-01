# Collections

Pre-configured collections to interact with 20+ blockchains & Alchemy endpoints.

You'll find 200+ ready-to-use requests across various blockchain ecosystems (Ethereum, Solana, Bitcoin, etc..) and protocols (json-rpc, rest, websocket, grpc).

We use [Bruno](https://www.usebruno.com/), an open-source, git-integrated and fully offline API client.

---

## Support

| Collection | JSON-RPC | REST API | WebSocket | GraphQL | gRPC |
|------------|----------|----------|-----------|---------|------|
| **evm** | ✓ | N/A | ✓ | N/A | N/A |
| **solana** | ✓ | N/A | ✓ | N/A | ✓ |
| **bitcoin** | ✓ | N/A | N/A | N/A | N/A |
| **aptos** | N/A | ✓ | N/A | N/A | ✓ |
| **sui** | ✓ | N/A | N/A | ✓ | ✓ |
| **zksync** | ✓ | N/A | N/A | N/A | N/A |
| **alchemy** | ✓ | ✓ | N/A | N/A | N/A |

### Available Collections

- **`evm/`** - Ethereum JSON-RPC (`eth_*`, `debug_*`, `trace_*`) + WebSockets
- **`solana/`** - Solana JSON-RPC + WebSockets + gRPC
- **`bitcoin/`** - Bitcoin Core JSON-RPC methods
- **`aptos/`** - Aptos REST APIs + Indexing GraphQL APIs + gRPC Transaction Stream
- **`sui/`** - Sui JSON-RPC + GraphQL + gRPC
- **`zksync/`** - zkSync JSON-RPC (`zks_*`)
- **`alchemy/`** - Alchemy APIs (Gas Manager, Token APIs, NFT, Portfolio, Simulation, Webhooks CRUD APIs)

---

## Getting Started

### Prerequisites

Install [Bruno](https://www.usebruno.com/downloads) or use Homebrew:

```bash
brew install bruno
```

### Installation

1. **Clone the repository:**
```bash
git clone https://github.com/alchemyplatform/collections.git
cd collections
```

2. **Open a collection in Bruno:**
   - Launch Bruno
   - Click **Open Collection**
   - Select a collection folder (e.g., `evm/`, `solana/`, `alchemy/`)

3. **Configure your API key:**
   - Open the collection in Bruno
   - Go to **Environments** tab
   - Create a Global environment to use across multiple collections.
   - Set your Alchemy API key:
     ```
     api_key: your-alchemy-api-key-here
     ```
  
  image.png

4. **Start testing:**
   - Browse available requests
   - Click **Send** to execute
   - View responses and documentation

### Using Collections

Each `.bru` file contains:
- Pre-configured request with example parameters
- Inline documentation and use cases
- Real-world parameter values

**Example workflow:**
1. Open `eth_getBalance.bru` in the `evm` collection
2. Review the documentation
3. Modify the address parameter if needed
4. Click **Send**
5. Inspect the response

**Stay updated:**
```bash
git pull
```
Bruno automatically loads new requests.

---

## Contributing 🙋

We welcome contributions! 

### How to Contribute

To add new blockchain methods or improve existing collections:

1. **Fork the repository**

2. **Add your `.bru` file:**
   - Place it in the appropriate collection folder (e.g., `evm/eth/`, `solana/`, `alchemy/`)
   - Follow the existing format with example parameters and documentation
   - Include inline docs describing the method, parameters, and use cases

3. **Create a Pull Request:**
   - Provide a clear description of what you're adding or fixing
   - Include example usage if adding a new method
   - Reference any related issues

### Examples

- **New methods** - Add missing RPC methods or API endpoints
- **Better examples** - Improve parameter values with real-world use cases  
- **Documentation** - Enhance inline documentation in `.bru` files
- **Bug fixes** - Fix incorrect parameters or broken requests

---

## Contributors

This repo is maintained by [Alchemy's Solutions Engineering team](https://github.com/alchemyplatform/lab).
