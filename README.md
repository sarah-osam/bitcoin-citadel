# Bitcoin Citadel Protocol 🏰

**A fortress-grade Bitcoin-native stablecoin protocol built on Stacks Layer 2.**
Bitcoin Citadel delivers institutional-quality collateralized lending with fortress-level security, merging Bitcoin’s immutability with the programmable flexibility of Stacks.

---

## 📖 System Overview

Bitcoin Citadel establishes a **Bitcoin-backed stablecoin** ecosystem with robust risk management, deep liquidity provisioning, and transparent governance.
The protocol is designed for **institutional adoption**, offering Bitcoin-grade security while ensuring **capital efficiency** and **scalability**.

### Key Features

* **Fortress Vaults**: Over-collateralized BTC vaults with 150% minimum collateral ratio.
* **Stablecoin Minting**: Fully Bitcoin-backed stablecoin issuance, denominated in satoshi-level precision.
* **Automated Market Maker (AMM)**: Deep liquidity pools supporting efficient trading.
* **Oracle Integration**: BTC/USD feeds with multi-signature validation and strict bounds checking.
* **Liquidation Engine**: Automated solvency protection when collateral ratios fall below 130%.
* **Governance Layer**: Time-locked administrative functions with community oversight.

---

## 🏛️ Protocol Architecture

The protocol is structured into four core layers:

1. **Collateral Vault Layer**

   * Manages user-deposited BTC.
   * Tracks locked collateral, minted stablecoins, and vault state.
   * Enforces over-collateralization and liquidation thresholds.

2. **Stablecoin Layer**

   * Issues and burns Bitcoin-backed stablecoins.
   * Maintains capped supply and precision-based accounting (sats).
   * Guarantees peg via BTC/USD collateral validation.

3. **Liquidity & AMM Layer**

   * Facilitates capital-efficient swaps between BTC and stablecoin.
   * Uses geometric mean-based LP token issuance for fairness.
   * Tracks provider shares, deposits, and withdrawals.

4. **Governance & Oracle Layer**

   * Updates BTC/USD oracle price (restricted to owner/admin).
   * Validates all prices against strict caps to prevent manipulation.
   * Time-locked governance ensures secure upgrades and parameter tuning.

---

## 📜 Contract Architecture

### State Variables

* **System State**

  * `contract-initialized` → Tracks initialization status.
  * `oracle-price` → Latest BTC/USD oracle feed.
  * `total-supply` → Total stablecoins minted.

* **Pool Balances**

  * `pool-btc-balance`
  * `pool-stable-balance`

* **Mappings**

  * `balances` → BTC balances per principal.
  * `stablecoin-balances` → Stablecoin balances per principal.
  * `collateral-vaults` → User vaults (BTC locked, stable minted, last updated).
  * `liquidity-providers` → LP data (tokens, BTC provided, stable provided).

### Core Public Functions

* `initialize(initial-price)` → Bootstraps protocol with oracle price.
* `update-price(new-price)` → Updates oracle price (owner-only).
* `deposit-collateral(btc-amount)` → Locks BTC into vault.
* `mint-stablecoin(amount)` → Issues stablecoins against BTC collateral.
* `burn-stablecoin(amount)` → Burns stablecoins to reduce debt.
* `add-liquidity(btc-amount, stable-amount)` → Provides liquidity, mints LP tokens.
* `remove-liquidity(lp-tokens)` → Removes liquidity, returns BTC & stable.

### Read-Only Functions

* `get-vault-details(owner)` → Returns vault state.
* `get-collateral-ratio(owner)` → Computes vault collateral ratio.
* `get-pool-details()` → Returns AMM pool balances & metrics.
* `get-lp-details(provider)` → Returns LP’s position data.

---

## 🔄 Data Flow

**1. Collateral Deposit**
User deposits BTC → vault updated → collateral ratio checked.

**2. Stablecoin Minting**
Mint request → checks max mint limits & collateral ratio → issues stablecoins → updates user and system supply.

**3. Liquidity Provisioning**
User adds BTC + stablecoins → LP tokens calculated (geometric mean) → pool balances updated.

**4. Trading & Liquidity Withdrawal**
Liquidity providers withdraw proportional shares → pool adjusts BTC and stable balances → assets transferred back.

**5. Liquidation (future extension)**
If vault ratio < 130% → liquidation engine triggers automatic debt resolution.

---

## ⚙️ Technical Highlights

* **Bitcoin-Grade Security**: Anchored in Stacks, secured by Bitcoin.
* **Satoshi Precision**: Native sat-denominated accounting (1:100,000,000 BTC).
* **Clarity Contracts**: Deterministic, formally verifiable, non-Turing complete.
* **MEV Protection**: Mitigates front-running with predictable execution.
* **Scalable AMM Design**: Optimized for high-frequency trading.

---

## 🚀 Getting Started

1. Clone the repository:

   ```bash
   git clone https://github.com/your-org/bitcoin-citadel-protocol.git
   cd bitcoin-citadel-protocol
   ```

2. Deploy contract to local devnet:

   ```bash
   clarinet contract deploy
   ```

3. Run tests:

   ```bash
   clarinet test
   ```

4. Interact via Clarinet console or API.

---

## 📌 Roadmap

* ✅ Collateralized stablecoin issuance.
* ✅ AMM liquidity provisioning.
* 🔲 Liquidation engine & auction system.
* 🔲 Governance DAO integration.
* 🔲 Cross-chain interoperability with Lightning & Bitcoin L1.

---

## 📜 License

MIT License – open for community contribution & institutional adoption.
