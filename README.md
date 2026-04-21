# @fundxgrid/stacks-core

[![npm version](https://img.shields.io/npm/v/@fundxgrid/stacks-core.svg)](https://www.npmjs.com/package/@fundxgrid/stacks-core)
[![TypeScript](https://img.shields.io/badge/%3C%2F%3E-TypeScript-%230074c1.svg)](https://www.typescriptlang.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Core infrastructure and shared Stacks blockchain utilities powering the **FundX** and **Chessify** SDK ecosystems. 

This package provides a strongly-typed, lightweight foundation for interacting with the Stacks blockchain, handling network configuration, and abstracting cross-chain queries.

## 🚀 Features

- **Strictly Typed:** First-class TypeScript support with comprehensive interfaces.
- **Network Agnostic:** Built-in support for `mainnet`, `testnet`, and `devnet` environments.
- **Modular Architecture:** Designed to be extended by higher-level SDKs without bloating the dependency tree.

## 📦 Installation

This package requires Stacks core libraries as **peer dependencies**. You must install them alongside this core utility.

### npm
```bash
npm install @fundx-grid/stacks-core @stacks/network @stacks/transactions
```

### yarn
```bash
yarn add @fundx-grid/stacks-core @stacks/network @stacks/transactions
```

### pnpm
```bash
pnpm add @fundx-grid/stacks-core @stacks/network @stacks/transactions
```

## 💻 Quick Start

Initialize the core client by passing in your desired network configuration. The client will automatically resolve the correct Hiro API URLs.

```typescript
import { StacksClient } from '@fundxgrid/stacks-core';

// Initialize for Mainnet
const client = new StacksClient({ network: 'mainnet' });

// Or specify a custom API URL for a local Devnet node
const devClient = new StacksClient({ 
  network: 'devnet', 
  apiUrl: 'http://localhost:3999' 
});
```

## 🛠 Advanced Usage

### Querying Account Balances

The client provides abstracted methods for standard on-chain queries. Always ensure you are handling potential network errors in production environments.

```typescript
import { StacksClient } from '@fundx-grid/stacks-core';

async function fetchUserBalance(walletAddress: string) {
  const client = new StacksClient({ network: 'mainnet' });

  try {
    const balance = await client.getAccountBalance(walletAddress);
    console.log(`Balance for ${walletAddress}: ${balance} micro-STX`);
    return balance;
  } catch (error) {
    console.error('Failed to fetch balance. Ensure the Hiro API is reachable:', error);
    throw error;
  }
}
```

## 🧩 API Reference

### `StacksClient`
The primary class for interacting with the Stacks network.
* `constructor(config: StacksConfig)`
* `getAccountBalance(address: string): Promise<number>`

### `NETWORKS`
A constant record containing the default API URLs for Hiro's public nodes.
```typescript
import { NETWORKS } from '@fundxgrid/stacks-core';

console.log(NETWORKS.testnet); // '[https://api.testnet.hiro.so](https://api.testnet.hiro.so)'
```

### Types
Exported interfaces for strict typing in consumer SDKs:
* `NetworkType`: `'mainnet' | 'testnet' | 'devnet'`
* `StacksConfig`: `{ network: NetworkType; apiUrl?: string; }`

## 🤝 Development

To build this package from source:

```bash
git clone https://github.com/FundX-Grid/stacks-sdks.git
cd stacks-sdks/stacks-core
npm install
npm run build
```

## 📄 License

MIT © jadonamite
