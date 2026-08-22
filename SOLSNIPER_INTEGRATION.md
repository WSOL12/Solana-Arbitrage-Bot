# SolSniper Integration - AI Anti-Rug for Your Bot

This guide shows how to add **SolSniper's AI rug detection** (94% accuracy, token scoring 0.0-1.0) to this bot.

## Why Integrate?

- 80% of new Solana tokens are rug pulls
- SolSniper's ML analyzes 50+ on-chain signals (mint/freeze authority, honeypots, holder concentration)
- Free, MIT licensed, 0% fees, 1 line integration

## Installation

```bash
pip install git+https://github.com/ezequiellich44-cmd/SolSniper.git
```

## Quick Integration (3 lines)

```python
from solsniper.ai_rug_detector import AdvancedRugDetector

detector = AdvancedRugDetector()
analysis = await detector.analyze(token_address) # risk_score 0.0-1.0, confidence, red_flags

if analysis.risk_score < 0.3: # SAFE
    await execute_buy(token_address)
else:
    print(f"Blocked rug: {analysis.red_flags} (score {analysis.risk_score})")
```

## Full Example

```python
import asyncio
from solsniper.ai_rug_detector import AdvancedRugDetector

detector = AdvancedRugDetector()

async def safe_buy(token_address, amount):
    analysis = await detector.analyze(token_address, rpc_url="YOUR_RPC")
    print(f"Token: {analysis.name} | Score: {analysis.risk_score}/1.0 ({analysis.risk_level.value}) | Confidence: {analysis.confidence:.0%}")
    if analysis.risk_score > 0.6:
        print(f"Blocked - {analysis.recommendations}")
        return None
    # ... your buy logic via Jupiter/Raydium/Jito
    return True

asyncio.run(safe_buy("So11111111111111111111111111111111111111112", 0.1))
```

## Features You Get

- Token scoring 0.0-1.0 with confidence intervals
- Historical rug pattern matching
- Honeypot detection
- Holder concentration analysis
- Liquidity depth check

## Links

- GitHub: https://github.com/ezequiellich44-cmd/SolSniper
- Landing: https://ezequiellich44-cmd.github.io/SolSniper/
- Full docs: https://github.com/ezequiellich44-cmd/SolSniper#readme

Built for Solana community - MIT license.
