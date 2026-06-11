# GST & Profit Guide — Athlents
# Written: 2026-06-11

---

## Your Current Situation

| Item | Detail |
|---|---|
| GST Status | Registered (Regular Scheme) |
| Turnover so far | ~50 pieces × ₹1299 = ~₹65,000 |
| GST owed so far | ~₹7,000 (12% on clothing above ₹1000) |
| Stock bought | Without GST invoice from manufacturer |
| ITC available | None (no GST invoice from supplier) |

---

## Step 1 — Pay the GST You Owe Now

You've sold ~50 pieces. The GST on those is approximately ₹7,000.

- File **GSTR-1** (sales invoice report) — due monthly or quarterly
- File **GSTR-3B** (summary + payment) — pay ₹7,000 here
- Do this before the due date to avoid late fees (₹50/day penalty)

If you haven't filed since registration, file NIL returns for the months you had no sales. Missing returns = penalties.

---

## Step 2 — Decide: Regular Scheme vs Composition Scheme

This is the most important decision. Talk to a CA this week.

### Regular Scheme (what you're on now)
- Charge 12% GST on every sale above ₹1000
- File GSTR-1 + GSTR-3B every month
- Issue proper GST Tax Invoice to customers
- Since you have no ITC (bought without GST) — full 12% is your liability

**On ₹10L revenue: pay ~₹1.07L in GST**

### Composition Scheme (recommended at your scale)
- Pay only 1% of total turnover to government
- Do NOT charge GST to customers (issue Bill of Supply instead)
- File CMP-08 quarterly (much simpler)
- Cannot claim ITC (doesn't matter — you have none anyway)

**On ₹10L revenue: pay only ₹10,000 in GST**

### Ask your CA specifically:
> "I am GST registered on Regular Scheme. My turnover is under ₹10 lakh. I buy stock from unregistered manufacturers so I have no ITC. Should I switch to Composition Scheme, and how do I do it?"

Switching is done via GST portal (Form CMP-02). CA can do it in a day.

---

## Step 3 — PayU Payment Gateway Setup

PayU and GST are **separate things**. Don't wait on GST decisions to set up PayU.

**What you need for PayU:**
- Current account (business bank account) — mandatory
- PAN (business or personal if sole proprietor)
- GSTIN — for PayU's own billing (they'll send you a GST invoice for their fees)
- Cancelled cheque or bank statement

**Important:** PayU giving you their GST invoice ≠ your product GST is handled.
Your product GST is still your own responsibility to file.

**PayU transaction fee:** ~1.9–2.5% per transaction
On ₹1299 order: ~₹25–32 goes to PayU

---

## Step 4 — Shopify Tax Configuration

### If you stay on Regular Scheme:
- Keep `taxesIncluded: true` ✓ (prices shown include GST — correct for India)
- Keep products `taxable: true` ✓
- Add GSTIN in: Admin → Settings → Taxes and duties → India
- Add HSN code `6103` to all clothing products (knitted trousers/pants)
- Shopify will show GST breakdown on invoices automatically

### If you switch to Composition Scheme:
- Set all products to `taxable: false`
- Remove any tax rates from India settings
- ₹1299 is simply your selling price, no GST line on invoice
- Issue "Bill of Supply" (not Tax Invoice)

---

## Profit Breakdown Per Item (₹1299 selling price)

### Scenario A — Regular GST Scheme
| Item | Amount |
|---|---|
| Selling price | ₹1299 |
| GST (12%, included) | -₹139 |
| PayU fee (~2%) | -₹26 |
| Estimated cost of goods | -₹400 to ₹600 |
| Shipping (if not charged) | -₹60 to ₹100 |
| **Net profit per piece** | **~₹434 to ₹674** |

### Scenario B — Composition Scheme (1%)
| Item | Amount |
|---|---|
| Selling price | ₹1299 |
| Composition tax (1%) | -₹13 |
| PayU fee (~2%) | -₹26 |
| Estimated cost of goods | -₹400 to ₹600 |
| Shipping (if not charged) | -₹60 to ₹100 |
| **Net profit per piece** | **~₹560 to ₹800** |

**Composition saves you ~₹126 per item in tax.**

---

## Profit Optimization Tips

### 1. Charge shipping separately
If you offer free shipping, you're absorbing ₹60–100 per order. Consider:
- Free shipping above ₹1999 (encourages larger orders)
- ₹79–99 flat shipping below that threshold

### 2. Bundle products
Once you have multiple products (hoodies, t-shirts etc.), offer bundles.
A ₹2499 bundle has lower per-unit cost and lower PayU % impact.

### 3. Get a GST invoice from your manufacturer
Even small manufacturers can register for GST. If yours does:
- You get ITC credit on your purchases
- On Regular Scheme, this reduces your GST liability significantly
- On ₹600 purchase with 5% GST → ₹30 ITC per unit

### 4. COD vs Prepaid
COD orders have:
- Higher return rates (15–25% for apparel)
- Extra COD handling fee (₹25–40 per order)
- Cash collection delays
Encourage prepaid with a small discount (₹50–100 off) to protect margins.

### 5. Return rate management
Apparel returns kill margins. Reduce with:
- Clear size chart (already done ✓)
- Detailed product photos showing fit
- Size recommendation on product page

---

## Immediate Action Checklist

- [ ] Book 30-min call with CA — ask about Composition Scheme switch
- [ ] File pending GST returns (NIL for zero-sale months, actual for sales months)
- [ ] Open current account if not done (needed for PayU)
- [ ] Set up PayU with current account + GSTIN
- [ ] Once CA confirms scheme — tell Claude to configure Shopify taxes correctly
- [ ] Get GST invoice from manufacturer for future stock purchases (for ITC)

---

## Key Numbers to Remember

| Threshold | Amount |
|---|---|
| Mandatory GST registration | ₹40L turnover |
| Composition scheme eligibility | Up to ₹1.5 crore turnover |
| Clothing GST (≤₹1000) | 5% |
| Clothing GST (>₹1000) | 12% |
| Composition rate (manufacturer) | 1% |
| GSTR-1 due date (quarterly) | 13th of month after quarter |
| GSTR-3B due date | 20th of following month |
| Late filing penalty | ₹50/day (₹20/day for NIL) |
