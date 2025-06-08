# DrainerLESS

DrainerLESS is a decentralized application (DApp) designed to rescue ERC20 tokens, NFTs, and airdrops from compromised wallets across multiple EVM-compatible networks. With the latest update incorporating **EIP-7702**, DrainerLESS now offers enhanced flexibility, security, and efficiency compared to its previous services: **Permit Rescue** and **Bundle Rescue**. This README provides an overview of the DApp, its features, the advantages of the EIP-7702 update, and setup instructions.

## Table of Contents
- [About DrainerLESS](#about-drainerless)
- [Features](#features)
- [EIP-7702 Update](#eip-7702-update)
- [Comparison with Previous Services](#comparison-with-previous-services)
- [Supported Networks](#supported-networks)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## About DrainerLESS

DrainerLESS enables users to safely recover assets (ERC20 tokens, NFTs, and airdrops) from compromised wallets by leveraging smart contracts and secure transaction mechanisms. Deployed on the Base network and extended to other EVM chains, it provides a user-friendly interface to execute rescue operations with a transparent 5% fee on successful rescues (no fees for failed operations).

The DApp uses a database contract (`DrainerLESSDB.sol`) to log transactions and supports multiple networks for writes, with reads primarily from the Base network. The latest update introduces **EIP-7702** support, significantly enhancing the rescue process.

## Features
- **Rescue ERC20 Tokens, NFTs, and Airdrops**: Recover assets from compromised wallets securely.
- **Multi-Network Support**: Operates on Base, Ethereum, Optimism, Arbitrum, BNB Chain, Polygon, Berachain, Sepolia, Linea, Monad, MegaETH, Pharos, and Mantle.
- **EIP-7702 Batched Transactions**: Execute complex rescue operations in a single transaction, improving efficiency and reducing gas costs.
- **Simulation Mode**: Preview rescue operations (including fees) before execution.
- **Transparent Fee Structure**: 5% fee on successful rescues; no fees for failed attempts.
- **Responsive UI**: Built with React, featuring a clean interface for desktop and mobile users.
- **Wallet Integration**: Connect via Reown (WalletConnect) for secure wallet interactions.
- **Internationalization**: Supports multiple languages using `react-i18next`.

## EIP-7702 Update

The **EIP-7702** update introduces a new transaction type that allows batched, programmable authorizations, replacing the earlier EIP-3074. This enables DrainerLESS to execute complex rescue operations in a single transaction, offering significant improvements:

- **Enhanced Flexibility**: EIP-7702 allows dynamic authorization of multiple actions (e.g., token transfers, NFT rescues, airdrop claims) in one transaction, reducing user interaction and gas costs.
- **Improved Security**: Temporary authorizations are cryptographically signed, ensuring only approved actions are executed without permanent control over the wallet.
- **Cross-Chain Compatibility**: Unlike previous services limited to Ethereum and BNB Chain, EIP-7702 is supported across all EVM-compatible networks listed in the DApp, enabling broader asset recovery.
- **Gas Efficiency**: Batching multiple operations reduces the number of transactions, lowering gas fees compared to sequential executions.

This update is implemented in `RescueEIP7702.tsx`, which handles batched transactions via the `batchTransactions` function in the `Recover` contract, ensuring seamless asset recovery across supported networks.

## Comparison with Previous Services

DrainerLESS previously offered two rescue methods: **Permit Rescue** and **Bundle Rescue**, the latter limited to Ethereum and BNB Chain, while **Permit Rescue** was limited to tokens with the permit function enabled. The EIP-7702 update significantly improves both methods:

| Feature                  | Permit Rescue (Old)                     | Bundle Rescue (Old)                    | EIP-7702 Rescue (New)                  |
|--------------------------|-----------------------------------------|----------------------------------------|----------------------------------------|
| **Supported Networks**   | Ethereum, BNB Chain                    | Ethereum, BNB Chain                    | All EVM networks (Base, Optimism, etc.)|
| **Transaction Type**     | Single ERC20 permit transaction         | Multiple transactions in a bundle       | Single batched transaction             |
| **Gas Efficiency**       | Moderate (single transaction)           | Low (multiple transactions)            | High (batched operations)             |
| **Complexity**           | Limited to ERC20 tokens                | Supports ERC20 and some NFTs           | Supports ERC20, NFTs, and airdrops     |
| **Security**             | Relies on permit signatures            | Relies on pre-signed transactions      | Cryptographic temporary authorizations |
| **User Experience**      | Requires multiple approvals            | Complex setup for bundling             | Simplified, single-step process        |

**Key Improvements**:
- **Broader Network Support**: EIP-7702 extends rescue capabilities to 14 EVM networks, compared to only Ethereum and BNB Chain previously.
- **Simplified Workflow**: Users no longer need multiple approvals or complex bundling; EIP-7702 batches all actions into one transaction.
- **Comprehensive Asset Recovery**: Unlike Permit (ERC20 only) and Bundle (limited NFT support), EIP-7702 handles ERC20, ERC721, ERC1155, and airdrop claims.
- **Cost-Effective**: Reduced gas costs due to batched transactions make rescues more affordable.

## Supported Networks
DrainerLESS supports the following networks (status as of v3.0.1):
- **Functional**: Ethereum, Base, Optimism, zkSync, Arbitrum, Berachain, Sepolia, Linea, Monad, MegaETH, Pharos, Mantle
- **Pending**: BNB Chain
- **Not Functional**: Polygon

Check the [Home.js](src/pages/Home.js) file for the latest network status and contract addresses.

## Installation

### Prerequisites
- Node.js (v18 or higher)
- npm or yarn
- A Web3 wallet (e.g., MetaMask) for testing
- Environment variables (see `.env` example below)

### Steps
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/edwinosky/DrainerLESS-frontend.git
   cd DrainerLESS-frontend
