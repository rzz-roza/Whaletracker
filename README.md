
# 🐋 RZZ ROZA Whale Tracker

Real-time whale transaction monitor for **Bitcoin** and **45+ EVM chains**.  
Tracks 500+ labeled addresses (Smart Money, CEX, DEX, Bridges).  
Advanced BUY/SELL detection with **DEX decoder**, **live price feed**, **rule engine**, and **mempool monitor**.

```

██████╗ ███████╗███████╗    ██████╗  ██████╗ ███████╗ █████╗ 
██╔══██╗╚══███╔╝╚══███╔╝    ██╔══██╗██╔═══██╗╚══███╔╝██╔══██╗
██████╔╝  ███╔╝   ███╔╝     ██████╔╝██║   ██║  ███╔╝ ███████║
██╔══██╗ ███╔╝   ███╔╝      ██╔══██╗██║   ██║ ███╔╝  ██╔══██║
██║  ██║███████╗███████╗    ██║  ██║╚██████╔╝███████╗██║  ██║
╚═╝  ╚═╝╚══════╝╚══════╝    ╚═╝  ╚═╝ ╚═════╝ ╚══════╝╚═╝  ╚═╝

```

---

## ✨ Features

- **45+ Chains** – Bitcoin + Ethereum, BSC, Arbitrum, Base, Polygon, Optimism, Avalanche, Fantom, and more.
- **500+ Labeled Addresses** – Smart Money (Jump, Wintermute, a16z, etc.), CEX wallets, DEX routers, bridges, lending.
- **Advanced Signal Detection**  
  - `BUY` = transfer to DEX / fresh wallet from CEX  
  - `SELL` = transfer to CEX  
  - `SMART MONEY` = any transaction involving labeled smart money  
  - `BRIDGE` / `LENDING` detection
- **DEX Swap Decoder** – Shows which router was used (Uniswap, 1inch, PancakeSwap, etc.)
- **Live Price Feed** – Fetches real-time USD prices from CoinGecko (auto fallback to estimates).
- **Rule Engine** – Create custom alert rules based on value, chain, address type, signal, etc.
- **Mempool Monitor** – Detect large pending transactions before they are mined (Ethereum, BSC, Polygon, Arbitrum, Base).
- **Termux Compatible** – Works on Android (Termux) with color support.

---

## 📦 Installation

### 1. Requirements
- Python **3.7+**
- `pip` package manager

### 2. Clone & Setup
```bash
git clone https://github.com/yourusername/rzz-whale-tracker.git
cd rzz-whale-tracker
```

3. Install Dependencies

```bash
pip install -r requirements.txt
```

If you don't have requirements.txt, install manually:

```bash
pip install aiohttp websockets requests
```

4. (Optional) Termux Additional Setup

If running on Termux (Android):

```bash
pkg install python
pip install aiohttp websockets requests
```

---

🚀 Usage

Run the tracker:

```bash
python rzz.py
```

The dashboard will appear showing:

· Real‑time whale alerts (value, chain, from address, signal)
· Chain activity bars
· Live BTC/ETH prices
· Rule engine matches ([!] or [R] indicator)

Press Ctrl+C to stop – a session summary will be displayed.

---

⚙️ Configuration

All settings are inside rzz.py. You can easily adjust:

Variable / Section Description
CHAINS list Add/remove chains, change RPC URLs or thresholds.
SMART_MONEY, CEX_WALLETS Extend the labeled address database.
PRICE_ESTIMATES Fallback prices if CoinGecko fails.
RuleEngine._init_default_rules() Modify default alert rules.
MempoolMonitor.monitored_chains Change which chains to monitor pending txs.

Example: Adding a custom rule

Edit the _init_default_rules method:

```python
self.add_rule(AlertRule(
    name="My Custom Rule",
    conditions={"min_usd": 100_000, "chains": ["Ethereum", "Arbitrum"]},
    action="highlight",
    priority=50
))
```

---

📊 Dashboard Legend

Symbol Meaning
[P] chain Pending transaction detected in mempool.
[!] signal Alert matched a notify or highlight rule.
[R] signal Alert matched at least one rule.
* in FROM The address is labeled (e.g., *Jump Trading).
[CEX] or [DEX] Address type when no specific label exists.
↳ Uniswap V3 Decoded DEX router info (if available).

---

🔧 Troubleshooting

Problem Solution
ModuleNotFoundError Install missing packages: pip install aiohttp websockets requests
No alerts / slow scanning Some public RPCs may be rate‑limited. Replace with your own RPC URL in CHAINS.
CoinGecko price fetch fails Automatic fallback to PRICE_ESTIMATES. Works offline.
Mempool monitor not showing data Only 5 chains are monitored by default. Add more in MempoolMonitor.monitored_chains.
Termux colors not displaying correctly The script auto‑detects Termux and adjusts terminal settings.

---

📁 File Structure

```
rzz.py          # Main application (everything is in one file)
```

All logic – scanners, rule engine, mempool monitor, dashboard – is contained in a single Python script for easy deployment.

---

🧑‍💻 Author

RZZ ROZA
Version: 1.0.0-Beta
“Track the whales. Follow the smart money.”

---

📝 License

This project is provided for educational and informational purposes only.
Use at your own risk. The author is not responsible for any financial decisions made based on this tool.

