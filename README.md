# Crypto Perp Funding Rate Arbitrage, DeFi Yields & Macro Radar MCP Server

[![MCP Compatible](https://img.shields.io/badge/MCP-2024--11--05%20%7C%202025--06--18-blue)](https://modelcontextprotocol.io)
[![Zero Dependencies](https://img.shields.io/badge/dependencies-0-brightgreen)](#)
[![Free Tier](https://img.shields.io/badge/Free%20Tier-2%20Calls%2FDay-success)](https://agent-kiosk.vercel.app/mcp)
[![Unlimited Pass](https://img.shields.io/badge/Unlimited%20Pass-%241%20%2F%20%245-purple)](https://agent-kiosk.vercel.app/buy)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

> Live Hyperliquid vs dYdX v4 perpetual funding rate arbitrage APR scanner, global TradFi/crypto macro radar (VIX, DXY, S&P 500, 10Y, BTC Dom) & DeFi stablecoin yields MCP.

Need a **Crypto Funding Rate Arbitrage MCP**, **Hyperliquid / dYdX Perp Basis MCP**, or **DeFi Yield & Macro Radar MCP server**? `crypto-funding-arb-mcp` streams delta-neutral perpetual funding spreads (APR), open interest crowding, safe high-TVL stablecoin pools, and live cross-asset TradFi macro indicators directly into Claude, Cursor, Codex, and quant agents.

---

## Why Use `crypto-funding-arb-mcp`?

- **Hyperliquid vs dYdX v4 Funding Rate Arbitrage (`perp_funding_arbitrage`)** — Calculates annualized funding basis spreads (APR), long/short direction, and open-interest crowding across perpetual DEXs.
- **Global TradFi & Crypto Macro Radar (`tradfi_macro_radar`)** — Live S&P 500, Nasdaq, CBOE VIX volatility, DXY Dollar Index, US 10Y Treasury Yield, Gold, WTI Oil, Crypto Fear & Greed, BTC Dominance, and chain TVL.
- **TVL-Filtered DeFi Yield Scanner (`defi_yields`)** — Finds the highest real APY pools for `USDC`, `USDT`, `ETH`, or `SOL` across Base, Ethereum, Arbitrum, and Solana filtered by minimum TVL.
- **2 Free Calls / Day Out of the Box** — Works immediately with **zero configuration** and **no API key required**.
- **Instant Unlimited Upgrade** — Need high-volume production calls? Grab an instant API key at **[https://agent-kiosk.vercel.app/buy](https://agent-kiosk.vercel.app/buy)** (**$1 Starter 7-Day Pass** or **$5 Pro 30-Day Pass**) or pay per request natively via **x402 (USDC on Base)**.

---

## Option 1: Zero-Install Remote MCP URL (Fastest)

Connect directly via **Streamable-HTTP MCP** without installing anything locally:

- **Free Tier (2 Free Calls/Day, Zero Config):**
  ```text
  https://agent-kiosk.vercel.app/mcp
  ```
- **Paid Unlimited URL (With Prepaid Pass Key):**
  ```text
  https://agent-kiosk.vercel.app/mcp?api_key=ak_live_YOUR_KEY_HERE
  ```

> **Get an Instant API Key in 10 Seconds:** **[https://agent-kiosk.vercel.app/buy](https://agent-kiosk.vercel.app/buy)**
> - **$1.00 USDC** — **7-Day Starter Pass** (Instant `ak_live_...` key)
> - **$5.00 USDC** — **30-Day Pro Pass** (Full unmasked datasets across all endpoints)

---

## Option 2: Local `npx` / Stdio Setup (Claude Desktop, Cursor, Codex)

This package is **pure Node.js >= 18** with **zero external npm dependencies**, exposing **only** the 3 focused tools for this workflow so your LLM context window stays lean.

### Claude Desktop (`claude_desktop_config.json`)

```json
{
  "mcpServers": {
    "crypto-funding-arb-mcp": {
      "command": "npx",
      "args": ["-y", "github:ralf9090/crypto-funding-arb-mcp"],
      "env": {
        "AGENT_KIOSK_API_KEY": ""
      }
    }
  }
}
```
*(Leave `AGENT_KIOSK_API_KEY` empty for **2 free calls/day**, or paste your `ak_live_...` key from [agent-kiosk.vercel.app/buy](https://agent-kiosk.vercel.app/buy) for unlimited access.)*

### Cursor (`.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "crypto-funding-arb-mcp": {
      "command": "npx",
      "args": ["-y", "github:ralf9090/crypto-funding-arb-mcp"],
      "env": {
        "AGENT_KIOSK_API_KEY": "ak_live_OPTIONAL_PASS_KEY"
      }
    }
  }
}
```

### OpenAI Codex CLI (`~/.codex/config.toml`)

```toml
[mcp_servers.crypto_funding_arb_mcp]
command = "npx"
args = ["-y", "github:ralf9090/crypto-funding-arb-mcp"]
env = { AGENT_KIOSK_API_KEY = "" }
```

### Run Directly via `git clone` + `node index.js`

```bash
git clone https://github.com/ralf9090/crypto-funding-arb-mcp.git
cd crypto-funding-arb-mcp
node index.js
```

---

## Included MCP Tools (3)

### `perp_funding_arbitrage`
Real-time Cross-Exchange Perpetual Funding Rate Arbitrage, Annualized Basis Spread (APR), Open Interest & Crowded Positioning Radar ($0.008 USDC) across Hyperliquid and dYdX v4.

| Parameter | Type | Required | Description |
| :--- | :--- | :---: | :--- |
| `symbol` | `string` | No | Optional coin ticker filter (e.g., 'BTC', 'ETH', 'SOL', 'AERO') or omit for highest APR spreads |
| `limit` | `number` | No | Max perpetual markets to return (1-40, default: 15) |
| `x_api_key` | `string` | No | Optional ak_live_... 30-day Prepaid API Pass key to unlock the full unmasked dataset |

### `tradfi_macro_radar`
Global TradFi, Macro & DeFi Capital Flow Intelligence Radar ($0.008 USDC). Returns live S&P 500, Nasdaq, CBOE VIX Volatility, US Dollar Index (DXY), US 10Y Treasury Yield, Gold, WTI Crude Oil, Crypto Fear & Greed Index, BTC Dominance, and top DeFi chain TVL.

| Parameter | Type | Required | Description |
| :--- | :--- | :---: | :--- |
| `focus` | `all \| tradfi \| crypto \| defi` | No | Macro intelligence focus area (default: 'all') |
| `x_api_key` | `string` | No | Optional ak_live_... 30-day Prepaid API Pass key to unlock the full unmasked dataset |

### `defi_yields`
DeFi highest APY & yield radar powered by DeFiLlama. Finds top lending and liquidity pools for any token (USDC, ETH, USDT, WBTC) filtered by blockchain and minimum TVL.

| Parameter | Type | Required | Description |
| :--- | :--- | :---: | :--- |
| `symbol` | `string` | No | Token symbol to earn yield on (default: 'USDC') |
| `chain` | `string` | No | Blockchain name such as 'Base', 'Ethereum', 'Arbitrum', 'Solana', or 'all' (default: 'Base') |
| `min_tvl_usd` | `number` | No | Minimum pool TVL in USD for safety filtering (default: 100000) |
| `limit` | `number` | No | Number of top pools to return (1-20, default: 5) |
| `x_api_key` | `string` | No | Optional ak_live_... 30-day Prepaid API Pass key to unlock the full unmasked dataset |


---

## Example Prompts

- "Find the highest annualized perpetual funding rate arbitrage spreads between Hyperliquid and dYdX right now."
- "Check tradfi_macro_radar for VIX, DXY, US 10Y yield, and Crypto Fear & Greed before opening delta-neutral positions."
- "Show top USDC DeFi yield pools on Base and Arbitrum with at least $1,000,000 TVL."

---

## Pricing & Rate Limits

| Tier | Cost | Quota | Setup |
| :--- | :--- | :--- | :--- |
| **Free Trial** | **$0** | **2 Free Calls / Day** | Zero config — works out of the box |
| **Starter Pass** | **$1 USDC** | **7 Days Unlimited** | Get `ak_live_...` at [agent-kiosk.vercel.app/buy](https://agent-kiosk.vercel.app/buy) |
| **Pro Pass** | **$5 USDC** | **30 Days Unlimited** | Get `ak_live_...` at [agent-kiosk.vercel.app/buy](https://agent-kiosk.vercel.app/buy) |
| **x402 Pay-Per-Call** | **$0.008–$0.10** | Unlimited autonomous | Pass `payment_signature` (Base USDC EIP-3009) |

---

## License

MIT © [ralf9090](https://github.com/ralf9090) — Powered by [Agent Kiosk](https://agent-kiosk.vercel.app) ([Upgrade / Buy API Key](https://agent-kiosk.vercel.app/buy)).
