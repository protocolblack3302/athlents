# Athlents Shopify — Project Context
# Last updated: 2026-06-11

---

## Store Details

| Key | Value |
|---|---|
| Store URL | https://athlents.myshopify.com |
| Internal domain (for CLI GraphQL) | euzrz8-u5.myshopify.com |
| Shopify Admin | https://admin.shopify.com/store/athlents |
| Storefront password | Snoopyclothing |
| Live theme name | Dawn |
| Live theme ID | 146788712610 |

---

## Local Setup

| Key | Value |
|---|---|
| Working folder | c:\Users\proto\OneDrive\Documents\codes\shopify customizations\Dawn-Dev |
| Shopify CLI version | 4.1.0 |
| Node version | v24.14.0 |

---

## All Themes on Shopify

| Name | Role | ID |
|---|---|---|
| Dawn | **LIVE** | 146788712610 |
| Dawn - DEV | unpublished | 149266235554 |
| Dawn (duplicate) | unpublished | 146788581538 |
| Radiant | unpublished | 146618679458 |
| Clarity | unpublished | 146618876066 |
| Horizon | unpublished | 146635030690 |
| Ritual | unpublished | 147219185826 |

> Dawn - DEV (#149266235554) was never touched — safe to delete for cleanup.

---

## CLI Commands Reference

### Start local dev server
```powershell
cd "c:\Users\proto\OneDrive\Documents\codes\shopify customizations\Dawn-Dev"
shopify theme dev --store=athlents.myshopify.com --store-password=Snoopyclothing --ignore="*.tmp*"
```
Preview: http://127.0.0.1:9292

### Push changes to live store
```powershell
cd "c:\Users\proto\OneDrive\Documents\codes\shopify customizations\Dawn-Dev"
shopify theme push --store=athlents.myshopify.com --theme=146788712610 --allow-live --ignore="*.tmp*"
```

### Pull latest live theme (sync any admin changes back locally)
```powershell
cd "c:\Users\proto\OneDrive\Documents\codes\shopify customizations\Dawn-Dev"
shopify theme pull --store=athlents.myshopify.com --theme=146788712610
```

### Run GraphQL queries
```powershell
shopify store execute --store=euzrz8-u5.myshopify.com --query="{ ... }"
```

### Run GraphQL mutations (modifies store data)
```powershell
shopify store execute --store=euzrz8-u5.myshopify.com --allow-mutations --query="mutation { ... }"
```

### Re-authenticate GraphQL (if token expires)
```powershell
shopify store auth --store euzrz8-u5.myshopify.com --scopes read_products,write_products,read_online_store_navigation,write_online_store_navigation,read_content,write_content
```

---

## Collections State (as of 2026-06-11)

| Title | Handle | Products | Notes |
|---|---|---|---|
| Loose Fit Pants | `loose-fit-pants` | 2 | Main product, hero + nav links here |
| Most Loved Products | `most-loved-product` | 1 | Exists but not in nav |
| Featured | `featured` | 0 | ⚠ NEEDS PRODUCTS — homepage grid + announcement bar point here |
| Hoodies | `hoodies` | 0 | Exists, removed from nav until products added |
| T-Shirts | `t-shirts` | 0 | Exists, removed from nav until products added |
| Winter Collection | `winter-collection` | 0 | Exists, removed from nav until products added |

> When products are added to Hoodies/T-Shirts/Winter Collection, add them back
> to the main menu via GraphQL (see mutation below).

### Add a collection back to nav (template)
```
mutation {
  menuUpdate(id: "gid://shopify/Menu/232405631138", title: "Main menu", items: [
    { title: "Home", type: FRONTPAGE },
    { title: "Loose Fit Pants", type: COLLECTION, resourceId: "gid://shopify/Collection/325578490018" },
    { title: "Hoodies", type: COLLECTION, resourceId: "gid://shopify/Collection/325578653858" },      # add when ready
    { title: "T-Shirts", type: COLLECTION, resourceId: "gid://shopify/Collection/325812453538" },     # add when ready
    { title: "Winter Collection", type: COLLECTION, resourceId: "gid://shopify/Collection/325812584610" }, # add when ready
    { title: "About Us", type: PAGE, resourceId: "gid://shopify/Page/112820781218" },
    { title: "Contact", type: PAGE, resourceId: "gid://shopify/Page/112741613730" },
    { title: "Track Your Order", type: HTTP, url: "/apps/ils/tracking/" }
  ]) { menu { items { title url } } userErrors { field message } }
}
```

---

## Navigation State (as of 2026-06-11)

### Main menu (handle: main-menu, ID: gid://shopify/Menu/232405631138)
- Home → /
- Loose Fit Pants → /collections/loose-fit-pants
- About Us → /pages/about-us
- Contact → /pages/contact
- Track Your Order → /apps/ils/tracking/

### Footer menu (handle: footer, ID: gid://shopify/Menu/232405663906)
- Privacy Policy
- Refund Policy
- Shipping Policy
- Terms of Service
- Contact Information

---

## URL Redirects Created
- `/collections/all` → `/collections/loose-fit-pants`

---

## Key Files Changed

| File | What changed |
|---|---|
| `sections/header-group.json` | Nav: dropdown, sticky on-scroll-up, dark announcement bar, announcement links to `featured` |
| `templates/index.json` | Hero: center aligned, both slides → `loose-fit-pants`; Featured collection: handle=`featured`, 4 cols, quick add, portrait |
| `templates/collection.json` | Quick add: standard, hover image: true, banner scheme: scheme-3 |
| `templates/product.json` | Media fit: cover, size guide block added, rating shown, icon labels fixed |
| `config/settings_data.json` | Heading scale: 110, card padding: 0, card style: standard |
| `sections/footer-group.json` | Newsletter heading: "Get Early Access to Drops" |

---

## Theme Design Settings (config/settings_data.json — current)

| Setting | Value |
|---|---|
| Header font | Oswald (n4) |
| Body font | Barlow (n4) |
| Heading scale | 110 |
| Button radius | 12px |
| Card style | standard (full bleed) |
| Card corner radius | 8px |

### Color Schemes
| Scheme | Background | Button | Usage |
|---|---|---|---|
| scheme-1 | #ffffff | #c8102e | Product pages, light sections |
| scheme-2 | #faf5f0 | #c8102e | Cards |
| scheme-3 | #0d0d0d | #c8102e | Header, hero overlays, footer |
| scheme-4 | #1a877d | #ffffff | Sale badges |
| scheme-5 | #840630 | #ffffff | Accent |
| scheme-coming-soon-hoodie | #0d0d0d | #00d4ff | (legacy — unused) |

---

## Homepage Structure (templates/index.json)

```
Homepage
├── Slideshow (full bleed, large, auto-rotate 5s)
│   ├── Slide 1: "Discover Your Style" → /collections/loose-fit-pants
│   └── Slide 2: "New Releases Dropping Soon" → /collections/loose-fit-pants
└── Featured collection → collection handle: "featured" (4 cols, portrait, quick add)
```

---

## Pending Tasks (still manual)

- [ ] **URGENT**: Add products to `featured` collection — homepage grid + announcement bar both point here, currently empty
- [ ] Add products to `hoodies` collection, then tell Claude to add "Hoodies" back to nav
- [ ] Add products to `t-shirts` collection, then tell Claude to add "T-Shirts" back to nav
- [ ] Add products to `winter-collection` collection, then tell Claude to add it back to nav
- [ ] Add social media links: Admin → Online Store → Themes → Customize → Theme settings (⚙) → Social media
- [ ] (Optional) Delete unused themes: Dawn-DEV (#149266235554), Dawn duplicate (#146788581538)

---

## Apps Installed (relevant to theme)
- **Judge.me Reviews** — review widget on product pages, preview badge on product cards
- **Omnisend** — email marketing embed
- **Kwikpass** — login block

---

## What Was Done This Session (Summary)

### Sprint 1 — P0 Conversion Fixes
- Desktop nav: drawer → dropdown
- Sticky header: none → on-scroll-up
- Collection quick add: none → standard
- Collection hover image: false → true
- Product image fit: contain → cover

### Sprint 2 — P1 UX Improvements
- Announcement bar: white → dark, removed social icons
- Removed "Coming Soon T-shirts" section from homepage
- Collection banner: off-brand cyan → scheme-3
- Hero alignment: middle-center → reverted back to middle-center (user preferred center)
- Card image padding: 12 → 0

### Sprint 3 — P2 Polish
- Related products rating: false → true
- Added size guide collapsible block to product page
- Fixed empty icon label ("Premium Quality")
- Footer newsletter: "Subscribe to our emails" → "Get Early Access to Drops"
- Heading scale: 100 → 110

### Store Data Changes (GraphQL)
- Created `featured` collection
- Rebuilt main menu with correct collection links
- Added URL redirect: /collections/all → /collections/loose-fit-pants
- Cleaned nav: removed Hoodies, T-Shirts, Winter Collection (all empty)
- Fixed announcement bar link → /collections/featured
- Fixed hero slide 2 link → /collections/loose-fit-pants
