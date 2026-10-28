# Slippage and price impact

| | Price impact | Slippage |
| --- | --- | --- |
| Caused by | The user's own trade | Other trades landing first |
| Known in advance | Yes, included in the quote | No |
| Controlled by | Trade size, route choice | Slippage tolerance |

## Minimum received

The slippage tolerance sets the **minimum received** for a swap:

```
minimum received = expected output × (1 − slippage tolerance)
```

If execution would return less, the transaction reverts. The user keeps the input tokens and pays only gas.

## Suggested tolerance

| Token type | Tolerance |
| --- | --- |
| Stablecoin to stablecoin | 0.1% or less |
| Major tokens (ETH, BTC, SOL, BNB) | 0.5% |
| Mid-cap tokens | 1% |
| Small, volatile or new tokens | 2% to 5% |
| Tokens with a transfer tax | Above the tax |

**Auto** slippage picks a value from the token pair and market conditions.

## Price impact bands

| Price impact | Meaning |
| --- | --- |
| Under 1% | Normal |
| 1% to 5% | Noticeable. A smaller amount, a limit order or a TWAP may do better |
| Above 5% | High. A large share of value is lost to the market |

## Why a swap fails

| Cause | Fix |
| --- | --- |
| Price moved beyond tolerance | Retry, or raise tolerance slightly |
| Not enough gas | Top up the native token |
| Transfer-tax token | Set tolerance above the tax |
| Expired quote | Refresh and confirm again |

A failed swap never takes the input tokens.
