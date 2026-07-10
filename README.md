# RYVORA — Aster-powered Perp DEX (Display Mode)

Is version mein **trading disabled hai** — sirf live market data (Aster API se), chart,
order book, aur wallet connect kaam karte hain, jaisa tumne bola tha.

## Kya kaam karta hai
- ✅ Live symbols + prices (Aster public API)
- ✅ Candlestick chart (15m, auto-refresh)
- ✅ Live order book (bids/asks)
- ✅ Wallet connect (MetaMask/Web3 wallet — address dikhega, koi signing nahi)
- ✅ Aster-inspired dark + warm-gold theme, RYVORA branding
- ⛔ Order placement disabled ("Coming Soon" button) — Phase 2 mein aayega

## Chalane ke steps

### 1. Backend (market data proxy)
```bash
cd backend
npm install
cp .env.example .env
# .env mein ASTER_ENV=testnet rakho, baaki fields is stage mein zaroori nahi
# (BUILDER_ADDRESS / MASTER_ENCRYPTION_KEY sirf trading phase ke liye chahiye honge)
npm run dev
```
Backend `http://localhost:8787` par chalega.

### 2. Frontend
Naye terminal mein:
```bash
cd frontend
npm install
npm run dev
```
Frontend `http://localhost:5173` par khulega, backend se automatically connect ho jayega
(vite.config.ts mein `/api` proxy already set hai).

## Note
Mere paas is sandbox mein internet access nahi hai, isliye maine `npm install` khud
chala kar test nahi kiya hai — code syntactically sahi hai lekin apne machine par
`npm install` ke baad chhoti dependency-version dikkatein aa sakti hain jinhe fix karna
padega. Agar koi error aaye to error message bhejo, main fix kar dunga.

## Aage kya (jab trading enable karni ho)
`ROADMAP.md` dekho — Phase 2 (wallet approve flow) aur Phase 3 (order placement) already
planned hain, backend mein `agent.ts` / `order.ts` routes bhi pehle se bane hue hain,
bas frontend se connect karne hain.
