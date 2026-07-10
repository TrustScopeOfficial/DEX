# RYVORA: Orderly → Aster Migration Roadmap

## Kyun phased hai?
Orderly ek **ready-made frontend trading kit** deta tha (order book, chart, positions — sab
pre-built components). Aster sirf **raw REST + WebSocket API** deta hai — koi UI kit nahi.
Iska matlab poori trading UI (order book, chart, order form, positions, PnL) humein khud
banani hogi, Aster ke data se connect karke. Isliye chhote, testable phases mein todna zaroori hai.

## Architecture badlaav (sabse important baat)
Orderly wala setup **pure frontend (static site)** tha — koi backend server nahi tha.
Aster ka "Builder" model kaam hi backend ke bina nahi karta:
- Har user ke liye ek "Agent" (API wallet) banta hai
- Us Agent ki **private key backend par securely store** karni padti hai (encrypted)
- Backend hi Aster ko signed order requests bhejta hai (EIP-712 signing)

**Isliye ab do hisse honge:**
- `backend/` — naya Node.js server jo Agent keys sambhalta hai aur Aster API se baat karta hai
- `frontend/` — tumhari existing site, dheere-dheere Orderly SDK hata kar Aster se connect hogi

---

## Phase 1 — Foundation (✅ is response mein shuru)
- [x] Backend scaffold (Node + TypeScript + Express)
- [x] Aster REST client — public market data (symbols, prices, order book) — auth ki zarurat nahi
- [x] Encrypted Agent-key storage (AES-256, master key .env se)
- [x] EIP-712 signing helper (order/agent requests sign karne ke liye)
- [x] Aster-inspired color theme (dark + warm tan accent) — RYVORA branding ke saath
- [ ] Backend ko test karna apne Aster testnet account se

## Phase 2 — Wallet & Agent Onboarding
- [ ] Frontend mein wallet connect (RainbowKit/wagmi — Orderly ka wallet-connector hata kar)
- [ ] "Enable Trading" flow: user `approveAgent` + `approveBuilder` sign kare
- [ ] Backend: naya Agent generate + encrypted store per user

## Phase 3 — Core Trading UI
- [ ] Market list + live prices (WebSocket)
- [ ] Chart (TradingView library already available — reuse ho sakti hai)
- [ ] Order book widget
- [ ] Order form (Market/Limit) → backend → Aster `/fapi/v3/order`
- [ ] Open positions + open orders table

## Phase 4 — Portfolio & Account
- [ ] Balance, PnL, margin
- [ ] Trade history
- [ ] Deposit/withdraw flow (Aster ke multi-chain bridge ke through)

## Phase 5 — Polish & Extra Features
- [ ] Leaderboard/points (Aster ke Rh Points se, agar API available ho)
- [ ] Full RYVORA-on-Aster theme polish, mobile responsive
- [ ] Production security review (key storage, rate limits)

## Zaroori Business Requirement (code se solve nahi hota)
- Apne builder wallet mein **kam se kam 100 $ASTER** deposit karna hoga (Aster ka requirement)
- Ek production server chahiye hoga (VPS/cloud) jo backend ko 24x7 host kare — GitHub Pages
  jaisi static hosting is baar kaam nahi karegi kyunki ab backend bhi hai
