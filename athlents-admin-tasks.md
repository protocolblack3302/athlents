# Athlents — Shopify Admin Manual Tasks
# (with exact navigation paths)

---

## TASK 1 — Fix the orange "Featured collection" warning (URGENT)
The homepage featured grid is empty because the collection handle `featured` doesn't exist yet.

**Navigate to:**
Shopify Admin → Products → Collections → [ Create collection ]

**Fill in:**
- Title: `Featured`
- (Shopify auto-sets the URL handle to `featured` — do not change it)
- Collection type: `Manual`
- Click [ Save ]

**Add products:**
- Scroll down to "Products" section on the collection page
- Click [ Browse ] → search and select the products you want on the homepage
- Click [ Save ]

**Verify fix:**
- Go back to: Online Store → Themes → [ Customize ] → (left sidebar) Home page
- The "Featured collection" item should no longer be orange
- In the canvas you should see your products in a grid

---

## TASK 2 — Remove "All Products" from the navigation menu

**Navigate to:**
Shopify Admin → Online Store → Navigation → Main menu

**What to do:**
- Find the menu item named "All Products" (or "Catalog" / "Collections")
- Click the [ ··· ] or trash icon next to it → Delete
- Click [ Save menu ]

---

## TASK 3 — Redirect `/collections/all` so it doesn't show a dump of everything

**Navigate to:**
Shopify Admin → Online Store → Navigation → (scroll to bottom) → URL Redirects → [ Add URL redirect ]

**Fill in:**
- Redirect from: `/collections/all`
- Redirect to: `/collections/trousers`
- Click [ Save redirect ]

---

## TASK 4 — Create a "Trousers" collection (hero button target)

The first hero slide "Explore Collection" button now points to `/collections/trousers`.
This will 404 until you create the collection.

**Navigate to:**
Shopify Admin → Products → Collections → [ Create collection ]

**Fill in:**
- Title: `Trousers`
- Handle must be: `trousers` (auto-set, do not change)
- Collection type: `Manual`
- Click [ Save ] → then add all trouser products via [ Browse ]

---

## TASK 5 — Create a "T-Shirts" collection (hero slide 2 button target)

The second hero slide "Shop Now" button points to `/collections/t-shirts`.

**Navigate to:**
Shopify Admin → Products → Collections → [ Create collection ]

**Fill in:**
- Title: `T-Shirts`
- Handle must be: `t-shirts` (auto-set, do not change)
- Collection type: `Manual`
- Click [ Save ] → add all T-shirt products via [ Browse ]

---

## TASK 6 — Create a "Loose Fit Pants" collection (category page)

Currently `/products/loose-fit-pants` opens a single product.
You want `/collections/loose-fit-pants` to show a grid of all pants first.

**Navigate to:**
Shopify Admin → Products → Collections → [ Create collection ]

**Fill in:**
- Title: `Loose Fit Pants`
- Handle must be: `loose-fit-pants` (auto-set, do not change)
- Collection type: `Manual`
- Click [ Save ] → add all loose fit pants products via [ Browse ]

---

## TASK 7 — Update navigation links to point to collection pages

**Navigate to:**
Shopify Admin → Online Store → Navigation → Main menu

**What to do:**
- Edit each nav link that currently points to a product URL (`/products/...`)
  and change it to point to the matching collection URL (`/collections/...`)
- Example: change `/products/loose-fit-pants` → `/collections/loose-fit-pants`
- Click [ Save menu ]

---

## TASK 8 — Add social media links (footer icons are blank)

**Navigate to:**
Online Store → Themes → [ Customize ]
→ (bottom-left) click the [ ⚙ Theme settings ] gear icon
→ Social media

**Fill in your handles/URLs:**
- Instagram: `https://www.instagram.com/yourusername`
- TikTok: `https://www.tiktok.com/@yourusername`
- etc.
- Click [ Save ]

---

## TASK 9 — Verify the Featured collection section in Theme Editor

After completing Task 1, confirm it looks right:

**Navigate to:**
Online Store → Themes → [ Customize ]
→ (left sidebar top dropdown) Select: `Home page`
→ Under "Template" section click `Featured collection`
→ In the right panel confirm "Collection" is set to `Featured`
→ If it shows a different collection or is blank, click the collection picker and select `Featured`
→ Click [ Save ]

---

## Quick Reference — Theme Editor Left Sidebar Sections

From the screenshots, your Theme Editor (Customize) shows:

```
Home page
├── Header
│   ├── Announcement bar     ← dark background, free shipping text
│   └── Header               ← logo + dropdown nav
│
├── Template
│   ├── Slideshow            ← 2 hero slides
│   └── Featured collection  ← ⚠ orange = collection missing (fix in Task 1)
│
└── Footer
    └── Footer               ← newsletter + social links
```

To edit any section: click it in the left sidebar → settings appear in the right panel.

---

## Priority Order

| # | Task | Urgency |
|---|---|---|
| 1 | Create `featured` collection | 🔴 Do first — homepage is broken without it |
| 2 | Create `trousers` collection | 🔴 Hero button 404s without it |
| 3 | Create `t-shirts` collection | 🔴 Hero slide 2 button 404s without it |
| 4 | Remove "All Products" nav link | 🟡 Do soon |
| 5 | Redirect `/collections/all` | 🟡 Do soon |
| 6 | Create `loose-fit-pants` collection | 🟡 When ready |
| 7 | Update nav links to collections | 🟡 After collections are created |
| 8 | Add social media links | 🟢 Low urgency |
| 9 | Verify Featured collection in Theme Editor | 🟢 After Task 1 |
