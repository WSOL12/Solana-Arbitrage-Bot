# Solana Dex Arbitrage Bot

To run this bot, you'll need a Solana RPC node and a self-hosted Jupiter v6 node.

> Note: This bot is not fully developed, lacks program implementation, and is limited to a WSOL/USDC trading pair. However, the basic logic is fully implemented.

## Steps

1. Select Trading Pairs

2. Run The Jupiter v6 Node

enable `--allow-circular-arbitrage`

```
./jupiter-swap-api --rpc-url https://mainnet-ams.chainbuff.com --yellowstone-grpc-endpoint https://grpc-ams.chainbuff.com --allow-circular-arbitrage --market-mode remote --filter-markets-with-mints So11111111111111111111111111111111111111112,EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v
```

3. Run the Bot

```
npx esrun src/index.ts
```

```
sent to frankfurt, bundle id: 429a763afe889b5c5694dc5405063506b7e463a6b0fe339d89a0b0991868edd2
So11111111111111111111111111111111111111112 - EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v
slot: 302063575, total duration: 85ms
diffLamports: 16189
```

## Profit Guarantee

The bot requires a program to ensure profitability. Without it, even if the slippage is set to 0 and the Jito bundle service is used, you may still incur losses due to the Jito tip. [See the example](https://solscan.io/tx/3DoYWBvnE826cqKM6pkFQvLzZ9qhzGrFFjaxbj6LahGcm1M9HicchAwibkBV5ZGb2gtymWSHPWM7owvBuYPDv3UR):

![](./img/tx-example.png)

# References

- https://station.jup.ag/docs/apis/self-hosted
- https://docs.jito.wtf
- https://docs.solanamevbot.com

# Feedback

Buff community: https://t.me/chainbuff