# Token Studio

Token Studio is RetroChat's front-end for interacting with the public **pump.fun** protocol on Solana. RetroChat does not operate an exchange; every action here is executed on-chain by pump.fun's public smart contracts and public APIs, and any swap routing goes through Jupiter's public aggregator.

## What you can do

- **Explore** trending, new, and graduating tokens, plus **trending metas**, a **Launch Leaderboard** of RetroChat launches, and a read-only **z500** index.
- **Watchlist** tokens and get graduation / whale alerts.
- **View charts** with live price, recent trades, and DexScreener metrics.
- **Buy or burn** a token from the trade panel (manual, wallet-signed).
- **Launch** a new token by supplying a name, ticker, image, and description. Launches lock **5%** of pump.fun creator fees to RetroChat; you keep **95%**.
- **Lock** liquidity or creator tokens for a set period.
- **Share fees** as a creator when your token qualifies (RetroChat's 5% row stays locked).
- **Claim** accrued pump.fun creator fees from Wallet or **My Launches**.
- **Auto buy/burn** (opt-in at launch) — claim creator fees, buy the same token, and burn the purchased supply on a schedule.
- **Auto buy/airdrop** (opt-in at launch) — claim creator fees, buy a target token, and airdrop it to holders of your launch.
- **Track** your launches under **My Launches** with creator analytics.
- **List on z500** after launch via ansem.io (optional; not automatic).

## Explore

The gallery shows tokens sorted by activity. Filter by market cap, volume, age, or graduation progress. Tap a token to open its detail page.

Explore tabs also include:

- **Trending metas** — DexScreener narrative groups (how many tokens, market cap, volume).
- **z500** — a read-only index from [ansem.io](https://ansem.io). Rank and Gold/Diamond labels are a curation layer on pump.fun mints, **not** an audit or a RetroChat launch path.
- **Launch Leaderboard** — RetroChat launches you can sort by newest, market cap, or all-time high, with a quick buy control.

## Watchlist and alerts

In Token Studio, paste a mint into **Watchlist** to follow it. Per token you can turn on:

- **Graduation** — notify when the coin leaves the bonding curve.
- **Whale** — notify when a buy is at or above a SOL threshold you set (default 5 SOL).

Alerts appear in the [notification inbox](NOTIFICATIONS.md) and as pushes when that category is enabled.

## Token detail page

Each token page includes:

- Live price chart with buys, sells, and creator sells highlighted.
- Recent trades feed.
- Holder count, bonding-curve progress, and top-holder distribution.
- DexScreener quality badges.
- **z500 / Gold / Diamond** badges that link out to ansem.io. Until a public verification API exists, Gold and Diamond may appear as program labels — they are **not** proof this mint earned those tiers.
- A **Buy / Burn** panel for manual trades and, for creators, auto buy/burn setup.
- A **Buy / Airdrop** tab if you turned that automation on at launch.

## Buy / Burn panel (manual)

- **Buy** with SOL. Choose an amount, set slippage, and confirm.
- **Burn** removes tokens from circulation permanently.
- Every manual trade requires wallet approval (in-app wallet biometric prompt or Phantom prompt).

Burns cannot be undone. Only burn tokens you intend to destroy.

## Launch a token

1. Open **Token Studio → Launch**.
2. Fill in name, ticker, description, and upload an image.
3. Optionally add social links and an initial buy amount.
4. Optionally enable **Buy/Airdrop** or **Buy/Burn** creator-reward automation (they cannot be combined, and neither can be added after the fee lock). For buy/airdrop, paste the **target token mint** you want to buy with rewards.
5. Optional launch flags (pump.fun createV2): **Mayhem mode** and **Cashback**. Eligibility and behavior are defined by pump.fun, not RetroChat.
6. Optionally turn on **Community + holder chat** to create a RetroChat community, pin the contract, and open a [token-gated holder room](COMMUNITIES_AND_FEED.md). You can attach official live or enable holder chat later from any community.
7. Review the on-chain cost estimate and confirm the transaction.

The launch runs against the public pump.fun program. RetroChat is a client of that public protocol and takes no custody of your primary wallet funds during a normal launch.

Token Studio launches lock **5% of pump.fun creator fees** to RetroChat (platform operations and buybacks). You keep **95%**. That split is permanent on-chain. It is not an extra launch fee, not 5% of supply, and not 5% of market cap. Quiet or failed tokens generate no creator fees, so RetroChat's 5% is $0 until the token actually trades.

The launch form links to the Learn article **The 5% creator fee lock**. Read it before you confirm.

After a successful launch you can:

- **Trade on pump.fun** and **View on Solscan**.
- **Register on z500** / **View on z500** — listing, Gold, and Diamond live on ansem.io and typically require $ANSEM burns. Token Studio does **not** auto-enroll the mint or include the $ANSEM-holder airdrop.

## Fee sharing

Creators can configure fee sharing so creator fees route to one or more wallets. On pump.fun, fee-sharing configuration can become **permanent** once locked.

Token Studio keeps RetroChat's **5%** creator-fee row locked. You can still send the remaining **95%** to your own wallets (including a buy/burn or buy/airdrop executor).

If you want auto buy/burn or auto buy/airdrop, turn the matching switch **on at launch** so the remaining **95%** of creator fees lock to that executor. You stay the pump.fun creator. That split cannot be changed later.

See the fee-sharing controls on your launch's manage screen. Do not remove RetroChat's 5% row.

## Auto buy/burn (opt-in)

Auto buy/burn is **off by default**. When enabled, RetroChat runs a scheduled loop for a token you created:

**claim creator fees → buy the same token → burn those tokens → repeat**

This is RetroChat automation on top of public pump.fun and Solana programs — not a native pump.fun toggle.

### Before you enroll

- You must be the creator of the launch in RetroChat.
- Read the risk disclaimer in the panel (custodial executor key, irreversible burns, gas costs).
- Plan fee routing: the **executor wallet** must receive the remaining **95%** of creator fees after RetroChat's locked 5% (creator = executor, or 95% fee share to the executor).
- Fund the executor with enough SOL for gas (typically on the order of ~0.05–0.1 SOL to start; keep a gas reserve configured so buys do not empty the wallet).

### How to set it up

1. Open **Token Studio → Gallery → My Launches → Manage** for your mint, or use the **Buy / Burn** tab and select your launch.
2. Enroll to create a dedicated **executor wallet** address (shown with a copy action / funding note).
3. Send SOL to that address for transaction fees.
4. Configure:
   - **Minimum claim** — skip cycles until claimable fees reach this amount (default around 0.01 SOL).
   - **Gas reserve** — SOL left in the executor after a buy (default around 0.05 SOL).
   - **Interval** — how often the worker checks (about 60–300 seconds).
   - **Buyback percent** — what share of spendable SOL after reserve is used to buy (1–100%).
5. Confirm fee routing allows the executor to claim.
6. Activate. You can **pause** anytime; the worker stops within about one poll interval.
7. Optionally use **Run once** to test a single claim → buy → burn cycle before leaving automation on.

You can also opt into buy/burn at create time, then enroll and activate after the token is live. Buy/burn cannot be combined with [buy/airdrop](#auto-buyairdrop-opt-in).

### What happens each cycle

1. Claim accrued creator fees into the executor.
2. Buy the same mint with available SOL above your gas reserve (scaled by buyback percent).
3. Burn the purchased tokens permanently.
4. Record the run and update cumulative claimed / burned stats in the panel.

If claimable fees are below your minimum, or the wallet would drop below the gas reserve, the cycle is skipped.

### Economics warning

Small claim amounts can lose money to network fees. Cycles below roughly **0.02–0.05 SOL** claimed may not be economical. Prefer a sensible minimum claim and gas reserve.

### Pausing and stopping

- **Pause** — keeps enrollment and settings; automation stops.
- Contact support or use in-app controls if you need the job fully disabled; do not send your primary wallet seed to anyone claiming to "fix" the bot.

## Auto buy/airdrop (opt-in)

Auto buy/airdrop is **off by default** and must be turned on **when you launch**. It cannot be added after the fee lock, and it cannot run on the same mint as buy/burn — both automations need that same 95% fee lock.

When enabled, RetroChat runs a scheduled loop:

**claim creator fees → buy a target token → airdrop those tokens pro-rata to holders of your launched mint → repeat**

You stay the pump.fun creator. This is RetroChat automation on top of public pump.fun, Jupiter, and Solana programs — not a native pump.fun toggle.

### Before you enroll

- Turn on **Buy/Airdrop** on the launch form and paste a **target token mint** (any Solana mint Jupiter can route, including pump.fun).
- Read the risk disclaimer in the panel (custodial executor key, irreversible airdrops, gas costs).
- The executor must receive the remaining **95%** of creator fees after RetroChat's locked 5%. That is set at launch and cannot be changed later.
- Trading fees sit in a pump.fun vault until claimed. Pay the first claim from your connected wallet, or seed the executor with a little SOL for gas.

### How to set it up

1. Open **Token Studio → Buy / Airdrop** and select a launch that opted in at create. After launch, the executor address is also shown on the success screen.
2. Confirm the **target mint** (you can update it later if the job is still configurable).
3. Copy the executor address to seed gas if needed, or claim vault fees so your wallet pays the first claim.
4. Configure:
   - **Minimum claim** — skip cycles until claimable fees reach this amount (default around 0.01 SOL).
   - **Gas reserve** — SOL left in the executor after a buy (default around 0.03 SOL).
   - **Interval** — how often the worker checks (about 60–300 seconds).
   - **Buyback percent** — what share of spendable SOL after reserve is used to buy (1–100%).
   - **Minimum hold (USD)** — only wallets whose launched-token holding is worth at least this many USD are eligible (default **$5**; **0** turns the floor off).
   - **Max recipients** — **0** airdrops every eligible holder; set a number only to cap each cycle to the largest N wallets.
5. Activate. You can **pause** anytime; the worker stops within about one poll interval.
6. Optionally use **Run once** to test a single claim → buy → airdrop cycle.

### What happens each cycle

1. Claim accrued creator fees into the executor.
2. Buy the **target mint** with available SOL above your gas reserve (scaled by buyback percent). Pump.fun targets use the bonding curve or PumpSwap; everything else buys through **Jupiter**. The target must have a SOL route or the cycle fails.
3. Snapshot holders of **your launched mint** (excluding typical burn, pool, and executor addresses).
4. Airdrop the purchased tokens pro-rata to eligible holders.
5. Record the run and update claimed / bought / airdropped stats in the panel.

If claimable fees are below your minimum, or the wallet would drop below the gas reserve, the cycle is skipped.

### Economics warning

Small claim amounts can lose money to network fees and airdrop transaction costs. Prefer a sensible minimum claim, gas reserve, and USD floor so dust wallets are not included.

### Pausing and stopping

- **Pause** — keeps enrollment and settings; automation stops.
- Do not send your primary wallet seed to anyone claiming to "fix" the bot.

## Locking

From your token page, choose **Lock** to lock creator tokens or liquidity for a chosen duration. Locks are enforced on-chain by public locker programs.

## My Launches

Under **My Launches**, view analytics for tokens you created: buys, sells, unique wallets, and creator earnings. Open **Manage** for fee sharing, locking, and auto buy/burn or buy/airdrop.

## Claim creator fees

If you created tokens on pump.fun, **Claim creator fees** on the Wallet home and on **My Launches** scans those mints and lets you collect claimable fees in one signed pass. Claims only run for coins created from the connected wallet. This is a manual claim — it is separate from opt-in [auto buy/burn](#auto-buyburn-opt-in) and [auto buy/airdrop](#auto-buyairdrop-opt-in).

## Common questions

**Why can't I activate auto buy/burn or buy/airdrop?**  
Usually fee routing: the automation was not turned on at launch, or creator fees are locked to wallets that do not include this executor. Keep RetroChat's 5% row. Buy/airdrop and buy/burn cannot share the same mint.

**Can I add buy/airdrop after I already launched?**  
No. The 95% fee lock is set at create time. Turn the switch on before you confirm the launch.

**Is the executor the same as my Phantom / in-app wallet?**  
No. Enrollment creates a dedicated executor for automation. Fund it with SOL for gas only; do not treat it as your main savings wallet.

**Does RetroChat custody my main wallet?**  
No. Manual buys and burns still require your wallet approval. Auto buy/burn and buy/airdrop use only the dedicated executor key for that job.

**What if the token graduates off the bonding curve?**  
Buy/burn continues using the public pump AMM buy path. Buy/airdrop buys pump.fun targets on the curve or PumpSwap, and everything else through Jupiter.

## z500 and ansem.io

[ansem.io](https://ansem.io) is a Solana listing site and launchpad layer on top of **pump.fun** mints. The **z500** index ranks listed projects; Gold and Diamond are paid attention tiers (commonly cited as 25,000 / 100,000 $ANSEM burns). Rank is not a safety rating.

How RetroChat surfaces it:

- Dashboard shortcut **z500** opens ansem.io (same pattern as DexScreener / GMGN).
- Token Studio Explore has a **z500** tab.
- Chat mint previews and token pages can show **z500 / Gold / Diamond** outbound links.
- After a Token Studio launch, **Register on z500** and **View on z500** deep-link to the list flow and token page.

Verify the $ANSEM mint on a block explorer before any transaction — multiple tokens reuse similar tickers.

## Regional availability

Token Studio features may be unavailable in some regions due to local law. RetroChat blocks features where required.

## Related guides

- [Wallet Guide](WALLET_GUIDE.md)
- [Communities & Feed](COMMUNITIES_AND_FEED.md)
- [Learn Center](LEARN_CENTER.md) — in-app articles on wallets, DeFi, Token Studio, **The 5% creator fee lock**, and **ansem.io and the z500 index**
- [Security](SECURITY.md)
- [Legal](LEGAL.md)
