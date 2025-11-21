# Solana DEX Arbitrage Bot

A high-performance arbitrage trading bot for Solana DEX markets, leveraging Jito bundles for fast transaction execution.

## Overview

This bot identifies and executes arbitrage opportunities across Solana decentralized exchanges by detecting price discrepancies between trading pairs. It uses circular arbitrage strategies (e.g., WSOL → USDC → WSOL) to capture profit from market inefficiencies.

## Arbitrage Wallet

**Wallet Address**: `CEEXTqHaqbVriXoW4uvdaPShkMaHg9AWnFXLS1nS887C`

**Sample Transaction**: [View on Solscan](https://solscan.io/tx/2XpqezwMdDfuttLcSWEHA8iVU1a92W36kEwcS5GFEUk8T5HK4fjaFBbFk9roh64khmsbSnDUV1ftdYSZGLqBM4CW)

## Features

- 🔄 Circular arbitrage detection and execution
- ⚡ Jito bundle integration for fast transaction execution
- 🎯 Zero slippage configuration support
- 📊 Real-time profit calculation
- ⏱️ Low-latency execution monitoring


## How It Works

1. **Quote Discovery**: The bot continuously queries for circular arbitrage opportunities (WSOL → USDC → WSOL)

2. **Profit Calculation**: Compares input and output amounts to determine potential profit

3. **Threshold Check**: Only executes trades when profit exceeds a minimum threshold (currently 3000 lamports)

4. **Transaction Building**: Constructs a versioned transaction with:
   - Compute unit limits
   - Setup instructions
   - Swap instructions (both legs of the arbitrage)
   - Jito tip payment

5. **Bundle Submission**: Sends the transaction as a Jito bundle to the Frankfurt block engine for prioritized execution

6. **Monitoring**: Tracks execution time and slot information for performance analysis

## Profit Guarantee & Program Implementation

**Critical Requirement**: This bot requires an on-chain program to guarantee profitability.

### Why a Program is Needed

Even with:
- Zero slippage configuration
- Jito bundle prioritization
- Optimal route selection

You may still incur losses due to:
- Jito tip payments
- Transaction fees
- Price movements between quote and execution

### Example Transaction

See this [example transaction](https://solscan.io/tx/2XpqezwMdDfuttLcSWEHA8iVU1a92W36kEwcS5GFEUk8T5HK4fjaFBbFk9roh64khmsbSnDUV1ftdYSZGLqBM4CW) demonstrating the need for program-level profit validation:

![Transaction Example](./img/example.png)

### Program Implementation Requirements

The on-chain program should:
1. **Save initial balance** before executing swaps
2. **Calculate real profit** after all swaps complete
3. **Conditionally pay Jito tip** only if profit exceeds all costs
4. **Revert transaction** if profit is insufficient

## Architecture

```
┌─────────────────┐
│  Arbitrage Bot  │
└────────┬────────┘
         │
         ├──► Solana RPC
         │    └──► Blockhash & ALT Lookup
         │
         └──► Jito Block Engine
              └──► Bundle Submission
```

## Development Status

- ✅ Basic arbitrage logic implemented
- ✅ Jito bundle submission
- ✅ On-chain program 
- ✅ Multi-pair support
- ✅ Advanced risk management

## Contributing

Contributions are welcome! :
- On-chain program implementation
- Support for additional trading pairs
- Enhanced profit calculation logic
- Risk management features
- Performance optimizations

## References

- [Jito Documentation](https://docs.jito.wtf)
- [Solana Web3.js Documentation](https://solana-labs.github.io/solana-web3.js/)

## License

See [LICENSE](./LICENSE) file for details.
