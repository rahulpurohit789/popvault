# PopVault — Launch Checklist

**Goal:** Go live on your Shopify store (`nswvki-2c.myshopify.com`) for the AP × Swatch Royal Pop drop on **May 16, 2026 (Saturday)**.

---

## ✅ Already done (by me, in your Shopify store)

- [x] 8 products created with official names (HUIT BLANC, OTTO ROSSO, GREEN EIGHT, BLAUE ACHT, LÀN BA, OTG ROZ, OCHO NEGRO, ORENJI HACHI)
- [x] Real product imagery from Swatch's CDN attached to each product
- [x] Royal Pop collection grouping all 8 watches
- [x] Pricing set in INR (₹147k Lépine / ₹164k Savonnette)
- [x] All 8 products flipped from DRAFT → ACTIVE
- [x] Custom landing page `/pages/royal-pop` created with hero video, countdown, all 8 colorways, Lépine vs Savonnette explainer, Mumbai/Tokyo/Delhi delivery cards

---

## 🛠 What you need to do (admin-only steps)

### 1. Upgrade trial → Basic plan (~₹360 for first 3 months)

- Shopify admin → **Settings → Plan → Choose a plan**
- Pick **Basic** plan, annual billing for best rate
- Promo: ₹20/month for first 3 months, then ₹1,499/month
- Required before customers can see your store publicly

### 2. Change your `myshopify.com` URL to `popvault.myshopify.com`

- Shopify admin → **Settings → Domains → Change Shopify domain**
- Set new name: `popvault`
- ⚠️ **This can only be changed once per store.** If `popvault.myshopify.com` is taken, try alternates: `popvaultco`, `popvaultofficial`, `getpopvault`, etc.
- This becomes your permanent backend URL even after you buy a real domain

### 3. Install a free waitlist app

Pick one of these from the Shopify App Store:

- **STOQ — Restock, Pre-order, Notify Me** (recommended) → [apps.shopify.com/restock-rocket](https://apps.shopify.com/restock-rocket) — free tier: 30 emails/month
- **Restock Alert & Waitlist Mini** → [apps.shopify.com/mini-vacation-mode](https://apps.shopify.com/mini-vacation-mode) — free plan available
- **Wait.li — Viral Waiting Lists** → [apps.shopify.com/product-waiting-lists](https://apps.shopify.com/product-waiting-lists) — free trial then $11.99/mo

After install:
- Enable the "Notify Me" / "Join Waitlist" button on each of the 8 Royal Pop products
- Set up email notifications going to your `support@weseegpt.com` inbox
- Customize button text to "JOIN WAITLIST" or "RESERVE" to match the PopVault brand

### 4. Set the `/royal-pop` page as your homepage

- Shopify admin → **Online Store → Navigation → Home page** (or via theme editor)
- For Dawn theme: **Online Store → Themes → Customize → Home page → Add section → Page → select `royal-pop`**
- Alternatively: redirect `/` to `/pages/royal-pop` via **Online Store → Navigation → URL redirects**

### 5. Set up a payment gateway (since Shopify Payments isn't in India)

- Shopify admin → **Settings → Payments → Choose a provider**
- Recommended: **Razorpay** (most popular in India) or **PayU**
- Both charge ~2% + GST per transaction
- Plus Shopify adds 2% third-party gateway fee on Basic plan

### 6. Remove the password page

- Shopify admin → **Online Store → Preferences → Password protection**
- Toggle off "Enable password"
- ⚠️ Don't do this until you're ready to go live publicly

### 7. (Optional but recommended) Buy a real domain

- Inside Shopify: **Settings → Domains → Buy new domain**
- Suggestions:
  - `popvault.in` (~₹800/yr)
  - `popvault.co.in` (~₹500/yr)
  - `popvault.club` (~$25/yr — premium TLD that fits the "vault" branding)
  - `getpopvault.com` (~$15/yr — if `.com` is taken)
- Shopify auto-configures DNS — takes 5 minutes

### 8. Re-host the product images on Shopify's CDN

Right now product images load directly from `www.swatch.com/dw/image/...`. For production:

- Download each of the 8 product images from Swatch's CDN
- Re-upload via **Products → [product] → Media → Upload**
- This protects you if Swatch ever changes URLs or blocks hotlinking
- Or ask me to do this when you have product time

---

## 📅 Timeline to launch (May 16)

| When | Step |
|---|---|
| **Now** | Upgrade plan, change `myshopify.com` URL, install waitlist app |
| **Today/tomorrow** | Set homepage, configure payment gateway, customize theme |
| **May 15** | Test full purchase flow with a test order |
| **May 15 night** | Remove password page → live |
| **May 16** | Drop day — drive traffic |

---

## 💰 Cost summary

| Item | Cost |
|---|---|
| Shopify Basic (first 3 mo promo) | ₹60 total |
| Shopify Basic (after promo, annual) | ~₹1,769/mo with GST |
| Domain (popvault.in) | ~₹100/mo amortized |
| Waitlist app | ₹0 (free tier) |
| Payment gateway fees | ~4% per sale (Razorpay 2% + Shopify 2%) |
| **Year 1 estimated fixed cost** | **~₹17,500–19,000** + ~4% of revenue |

---

## 🔗 Quick links inside your Shopify admin

- Landing page: **Online Store → Pages → Royal Pop — AP × Swatch | PopVault**
- Collection: **Products → Collections → Royal Pop — AP × Swatch**
- 8 products: **Products** (filter by Vendor = "PopVault")
- Plan upgrade: **Settings → Plan**
- Domain: **Settings → Domains**
- Payment: **Settings → Payments**

---

*Generated by your PopVault setup session — last updated May 14, 2026.*
