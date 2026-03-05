# 🌱 Bitcoin Garden — Tamagotchi DCA Vault on Bitcoin L1

> **Grow your Bitcoin savings like a plant. Miss a DCA cycle and it wilts.**  
> A gamified, on-chain Dollar Cost Averaging vault built on OPNet smart contracts — where your investment discipline becomes a living garden.

[![Bitcoin](https://img.shields.io/badge/Bitcoin-L1-f7931a?style=flat-square&logo=bitcoin&logoColor=white)](https://bitcoin.org)
[![OPNet](https://img.shields.io/badge/OPNet-Regtest-9fd855?style=flat-square)](https://opnet.org)
[![Bob MCP](https://img.shields.io/badge/Bob_MCP-ai.opnet.org-4d9fff?style=flat-square)](https://ai.opnet.org)
[![Responsive](https://img.shields.io/badge/Responsive-Mobile%20Ready-4a7c2f?style=flat-square)](#responsive-design)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

---

## 🎮 The Concept

**Bitcoin Garden** turns boring DCA investing into a Tamagotchi-style game. Your vault is a living plant — it grows every time you water it (execute a DCA cycle), and wilts when you miss one. The further you are from your last DCA, the sicker your plant gets. Harvest when it blooms for maximum gains.

```
🌰 SEED → 🌱 SPROUT → 🪴 SAPLING → 🌸 BLOOMING → 💰 HARVEST
   0%        25%          40%           75%          100%
```

**Core mechanic:** every DCA cycle = 💧 water. Miss a cycle = health drops. Plant dies at 0% health = emergency withdraw penalty.

---

## 📸 Preview

```
┌─────────────────────────────────────────────────────────────────────┐
│  🌱 BITCOIN GARDEN v1.0  | 🌿 GARDEN  📊 STATS  🏆 BOARD | #891234 │
├──────────────────┬────────────────────────────────┬─────────────────┤
│ 🏡 MY GARDEN     │                                │ 🪴 VAULT STATUS  │
│ SATOSHI'S GARDEN │          🌸                    │ STAGE: BLOOMING  │
│                  │         💛💛💛                  │ DEPOSITED: 0.012 │
│ BALANCE  0.0482  │        🌿 │ 🌿                 │ STREAK:   🔥 7   │
│ VAULT    0.012   │           │                    │ P&L:    +4.82%   │
│ STREAK   🔥 7    │  ┌────────────────┐            │                  │
│ NEXT DCA 3 blks  │  │    🪴 POT      │            │ ⛓️ ON-CHAIN TXS  │
│                  │  └────────────────┘            │ 💧 DCA #7 done   │
│ ⚙️ DCA CONFIG    │  ████████████░░░░ 78%          │ 🌱 Vault Planted │
│ 0.001 tBTC/10blk │  ── BLOOMING 🌸 ──             │ 🔗 Connected     │
│                  │         ☀️ 🦋 ☀️               │                  │
│ [🌱 PLANT VAULT] │                                │                  │
│ [💧 WATER (DCA)] │                                │                  │
│ [🪙 HARVEST BTC] │                                │                  │
└──────────────────┴────────────────────────────────┴─────────────────┘

MOBILE (≤480px):
┌─────────────────────┐
│ 🌱 BITCOIN GARDEN   │
│ 🌿GARDEN 📊STATS 🏆 │
│ 🔌 CONNECT WALLET   │
├─────────────────────┤
│                     │
│         🌸          │
│        💛💛💛        │
│       🌿 │ 🌿       │
│          │          │
│  ████████████░ 78%  │
│  ── BLOOMING 🌸 ──  │
│       ☀️ 🦋 ☀️      │
├──────┬──────┬───────┤
│VAULT │STREAK│STAGE  │
│0.012 │🔥 7  │🌸BLOOM│
├──────┴──────┴───────┤
│ [🌱][💧][🪙][📤]   │ ← fixed bottom bar
└─────────────────────┘
```

---

## 🚀 Quick Start

### Prerequisites

| Tool | Version | Link |
|------|---------|------|
| OP_WALLET Extension | Latest | [Chrome Store](https://chromewebstore.google.com/detail/opwallet/pmbjpcmaaladnfpacpmhmnfmpklgbdjb) |
| Node.js | ≥ 18.x | [nodejs.org](https://nodejs.org) |
| OPNet CLI | Latest | `npm install -g @btc-vision/opnet-cli` |

### 1. Clone & Open

```bash
git clone https://github.com/YOUR_USERNAME/bitcoin-garden.git
cd bitcoin-garden

# No build step needed — single HTML file
open bitcoin-garden.html

# Or serve locally for wallet access (file:// blocks some wallet APIs)
npx serve .
# → http://localhost:3000
```

### 2. Setup OP_WALLET

```
1. Install OP_WALLET from Chrome Store (link above)
2. Create or import wallet
3. Open extension → Settings → Network → Select "Regtest"
4. Get free tBTC: https://faucet.opnet.org
```

### 3. Deploy the Vault Contract

```bash
# Install OPNet CLI
npm install -g @btc-vision/opnet-cli

# Deploy DCA Vault contract to regtest
opnet deploy --network regtest --contract ./contracts/DCAVault.ts

# Paste the deployed address into bitcoin-garden.html:
# const VAULT_CONTRACT = 'bcrt1p_YOUR_VAULT_CONTRACT_ADDRESS';
```

### 4. Plant & Grow

```
1. Open bitcoin-garden.html → Click "CONNECT" → Approve in OP_WALLET
2. Configure DCA: Amount per cycle, Block interval, Max cycles
3. Click "🌱 PLANT VAULT" → Sign transaction → Watch your plant sprout
4. Click "💧 WATER (DCA NOW)" every interval to keep it healthy
5. Reach 🌸 BLOOMING stage → Click "🪙 HARVEST BTC" to claim
```

---

## 🌿 Plant Life Cycle

| Stage | Trigger | Visual | Health |
|-------|---------|--------|--------|
| 🌰 **Seed** | Vault created | Empty pot | — |
| 🌱 **Sprout** | First DCA (≥1 cycle) | Small green shoot | 80% |
| 🪴 **Sapling** | ≥40% cycles done | Stem + leaves | 70%+ |
| 🌸 **Blooming** | ≥75% cycles done | Full bloom + BTC flower | 60%+ |
| 💰 **Harvest** | All cycles complete | Golden bitcoin bloom | Any |

### Health Mechanics

```
Health starts at 80% after planting.

Each successful DCA:     +15% health (capped at 100%)
Each missed interval:    -5%  health every poll cycle
Streak broken:           streak resets to 0
Health reaches 0%:       Plant wilts, emergency withdraw triggers 5% fee
```

### Weather System

The garden background weather reflects your plant health in real time:

| Health | Weather | Mood |
|--------|---------|------|
| > 80% | ☀️ 🦋 | Thriving |
| 40–80% | ⛅ 🌿 | Growing |
| < 20% | ⛈️ 🌩️ | Critical |

---

## 🏗️ Architecture

```
┌────────────────────────────────────────────────────────────────┐
│                    FRONTEND (bitcoin-garden.html)               │
│                                                                │
│  ┌─────────────────┐  ┌────────────────┐  ┌────────────────┐  │
│  │  Left Panel     │  │  Garden Stage  │  │  Right Panel   │  │
│  │  DCA Config     │  │  CSS Plant Art │  │  Vault Stats   │  │
│  │  Action Buttons │  │  Health Bar    │  │  TX Feed       │  │
│  │  Achievements   │  │  Weather FX    │  │  Analytics     │  │
│  └─────────────────┘  └────────────────┘  └────────────────┘  │
│                              │                                 │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  Mobile Layer (≤480px)                                   │  │
│  │  Stats Strip · TX Feed · Fixed Action Bar                │  │
│  └──────────────────────────────────────────────────────────┘  │
│                                                                │
│  Wallet Layer    → window.unisat (OP_WALLET API)               │
│  RPC Layer       → fetch POST → regtest.opnet.org              │
│  State Layer     → localStorage (persists between sessions)    │
│  Chart Layer     → Canvas 2D (pixel-art style chart)           │
└──────────────────────────┬─────────────────────────────────────┘
                           │  PSBT / signInteraction
                           ▼
┌────────────────────────────────────────────────────────────────┐
│                     OP_WALLET EXTENSION                         │
│  Signs PSBT with user private key → Broadcasts to OPNet node   │
└──────────────────────────┬─────────────────────────────────────┘
                           │  Signed Bitcoin TX
                           ▼
┌────────────────────────────────────────────────────────────────┐
│              OPNet Regtest Node (regtest.opnet.org)             │
│                                                                │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │               DCAVault.ts (Smart Contract)                │  │
│  │                                                          │  │
│  │  createVault(uint64 amount, uint32 interval, uint32 max) │  │
│  │  executeDCA()           — water the plant                │  │
│  │  withdrawAll()          — harvest or emergency exit      │  │
│  │  getVault(address)      — read vault state               │  │
│  │  getStats()             — protocol-wide stats            │  │
│  └──────────────────────────────────────────────────────────┘  │
│                         │                                      │
│                   Bitcoin L1 Blocks (~10 min each)             │
└────────────────────────────────────────────────────────────────┘
```

---

## 📁 Project Structure

```
bitcoin-garden/
├── bitcoin-garden.html      # Main app — complete single-file dApp
├── contracts/
│   └── DCAVault.ts          # OPNet smart contract (AssemblyScript/WASM)
├── README.md
└── LICENSE
```

---

## 🔗 On-chain Integration

### Wallet Connection

OP_WALLET injects as `window.unisat` (forked from UniSat). The app detects either `window.unisat` or `window.opnet`:

```javascript
// Detect provider
const provider = window.unisat || window.opnet;

// Connect
const accounts   = await provider.requestAccounts();
const publicKey  = await provider.getPublicKey();
await provider.switchNetwork('regtest');

// Get live balance from OPNet RPC
const balance = await rpc('op_getBalance', [address]);
```

### Sending Transactions

Three fallback methods in priority order:

```javascript
// Method 1: Native OPNet API
const result = await provider.signInteraction({
  to:      vaultContract,
  data:    calldata,        // ABI-encoded
  value:   amountInSats,
  network: 'regtest',
});

// Method 2: sendBitcoin (value transfers)
const txid = await provider.sendBitcoin(vaultContract, amountSats);

// Method 3: pushTx (raw PSBT with OP_RETURN calldata)
const txid = await provider.pushTx({ rawtx: psbtHex });
```

### Calldata Encoding

All contract calls use ABI-encoded calldata:

```javascript
// Create vault: createVault(uint64 amount, uint32 interval, uint32 maxCycles)
const calldata = '0x' + SEL.createVault
  + Math.floor(amount * 1e8).toString(16).padStart(64, '0')  // satoshis
  + interval.toString(16).padStart(64, '0')
  + maxCycles.toString(16).padStart(64, '0');

// Execute DCA: executeDCA() — no params, just the selector
const calldata = '0x' + SEL.executeDCA;

// Withdraw all: withdrawAll()
const calldata = '0x' + SEL.withdrawAll;
```

### Live RPC

Block height polled from OPNet every 12 seconds:

```javascript
const RPC = 'https://regtest.opnet.org';

const result = await fetch(RPC, {
  method: 'POST',
  body: JSON.stringify({ jsonrpc: '2.0', method: 'op_blockNumber', params: [], id: 1 })
});
// Fallback: eth_blockNumber (EVM-compatible method)
```

---

## 📊 Analytics Dashboard

The Stats view includes a **real-time pixel-art canvas chart** comparing three strategies:

| Strategy | Color | Description |
|----------|-------|-------------|
| 🟠 DCA | Orange | Your vault's accumulated value over time |
| 🔵 Lump Sum | Blue | What a single full-amount buy would be worth |
| ⬜ HODL | Gray | Baseline: just holding from day one |

Additional analytics cards:

- **Total Deposited** — cumulative tBTC in vault
- **P&L %** — profit/loss vs average buy price
- **Streak** — consecutive DCA cycles completed
- **Progress** — % of max cycles done
- **DCA Count** — total cycles executed
- **Stage** — current plant growth stage

---

## 📱 Responsive Design

Bitcoin Garden is fully responsive across all screen sizes:

| Breakpoint | Layout |
|-----------|--------|
| **> 1200px** | Full 3-panel: Left config + Garden + Right stats |
| **768–1200px** | Left panel hidden, right panel shrinks to 220px |
| **480–768px** | Single column, right panel becomes horizontal strip below garden |
| **≤ 480px** | Mobile: garden + stats grid (2×3) + scrollable TX feed + fixed action bar at bottom |

Mobile-specific UI elements (hidden on desktop, shown via JS on mobile):

```
mobile-stats   → 6-card stats grid (vault, streak, stage, P&L, cycles, next DCA)
mobile-tx      → scrollable on-chain TX feed
mobile-actions → fixed bottom action bar (🌱💧🪙📤)
```

The layout is toggled by `applyResponsiveLayout()` which fires on load and every `window.resize`.

---

## 🏅 Achievements

| Badge | Name | Condition |
|-------|------|-----------|
| 🌱 | FIRST SEED | Plant your first vault |
| 💧 | FIRST WATER | Complete first DCA cycle |
| 🔥 | ON FIRE | 3 consecutive DCA streaks |
| ⚡ | LIGHTNING | 7 consecutive DCA streaks |
| 🌸 | IN BLOOM | Reach blooming stage |
| 💎 | DIAMOND HANDS | Hold for 50+ DCA cycles |
| 💰 | BIG BAGS | Vault exceeds 0.1 tBTC |
| 🪙 | HARVESTER | Complete a full harvest |

---

## 📜 Smart Contract

`DCAVault.ts` is written in AssemblyScript, compiled to WebAssembly, and deployed on OPNet as an OP_20-compatible contract.

```typescript
// DCAVault.ts (AssemblyScript)

export function createVault(
  amountPerCycle: u64,   // satoshis per DCA cycle
  blockInterval: u32,    // blocks between each DCA
  maxCycles: u32         // total cycles before harvest
): void { /* ... */ }

export function executeDCA(): void {
  // Verifies caller owns vault
  // Checks block height >= lastDcaBlock + interval
  // Executes buy, updates streak, advances nextDcaBlock
}

export function withdrawAll(): void {
  // Returns deposited tBTC to owner
  // Applies 5% early-exit fee if health < 20%
}

export function getVault(owner: string): VaultState { /* ... */ }
export function getStats(): ProtocolStats { /* ... */ }
```

### Deploy to Regtest

```bash
# Using OPNet CLI
opnet deploy --network regtest --contract ./contracts/DCAVault.ts --wallet ./wallet.json

# Or ask Bob MCP to scaffold and deploy for you:
claude mcp add opnet-bob --transport http https://ai.opnet.org/mcp
# "Deploy a DCA vault contract with executeDCA, withdrawAll, getVault to OPNet regtest"
```

---

## 🌐 Network Configuration

| Parameter | Value |
|-----------|-------|
| Network | OPNet Regtest |
| RPC Endpoint | `https://regtest.opnet.org` |
| Explorer | `https://opscan.org` |
| Faucet | `https://faucet.opnet.org` |
| Block Time | ~10 min (Bitcoin L1) |
| Fee Unit | Satoshis (sats) |
| Token Decimals | 8 (OP_20 standard) |

---

## 🔧 Customization

### Change DCA defaults

```javascript
// In bitcoin-garden.html, update initial vault state:
let vault = {
  dcaAmount:    0.001,   // tBTC per cycle
  dcaInterval:  10,      // blocks between cycles
  dcaMaxCycles: 12,      // total cycles for full harvest
  // ...
};
```

### Swap contract address

```javascript
const VAULT_CONTRACT = 'bcrt1p_YOUR_DEPLOYED_CONTRACT_ADDRESS_HERE';
```

### Add a new achievement

```javascript
const ACHIEVEMENTS = [
  // ... existing achievements
  {
    id:    'my_milestone',
    icon:  '🚀',
    name:  'MOON SHOT',
    desc:  'Vault exceeds 1.0 tBTC',
    earned: false
  },
];

// Trigger it anywhere:
if (vault.deposited >= 1.0) unlockAchievement('my_milestone');
```

---

## 🗺️ Roadmap

- [ ] Deploy `DCAVault.ts` contract to OPNet regtest
- [ ] Real block-triggered auto-DCA via OPNet contract callbacks
- [ ] Price oracle integration (CryptoCharts via Bob MCP) for real P&L
- [ ] NFT plant skin minting — rare plants for streak milestones
- [ ] Multiplayer garden — visit and water friends' plants
- [ ] OPNet mainnet deployment
- [ ] PWA support — install as mobile app with push notifications for DCA reminders

---

## 📚 Resources

| Resource | Link |
|----------|------|
| OPNet Documentation | [docs.opnet.org](https://docs.opnet.org) |
| OPNet GitHub | [github.com/btc-vision](https://github.com/btc-vision) |
| OP_WALLET Extension | [Chrome Store](https://chromewebstore.google.com/detail/opwallet/pmbjpcmaaladnfpacpmhmnfmpklgbdjb) |
| Bob MCP Agent | [ai.opnet.org](https://ai.opnet.org) |
| OPScan Explorer | [opscan.org](https://opscan.org) |
| Regtest Faucet | [faucet.opnet.org](https://faucet.opnet.org) |
| Vibecode Event | [vibecode.finance](https://vibecode.finance) |

---

## 🏆 Built For

This project was built for the **[Vibecode.finance](https://vibecode.finance) OPNet Vibe Coding Event** — a hackathon for builders shipping dApps on Bitcoin L1 powered by OPNet smart contracts and Bob MCP AI agent.

> *"Grow your stack. One block at a time."* 🌱₿

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

<div align="center">

**🌱 Grow · 💧 Water · 🌸 Bloom · 🪙 Harvest**

Built on Bitcoin L1 · Powered by OPNet · AI by Bob MCP

[OPNet](https://opnet.org) · [OPScan](https://opscan.org) · [Motoswap](https://motoswap.org) · [Vibecode](https://vibecode.finance)

</div>
