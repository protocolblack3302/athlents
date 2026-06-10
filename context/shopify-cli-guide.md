# Shopify CLI & GraphQL — How We Work

## 1. Authentication

### First-time login
```powershell
shopify auth login --store=athlents.myshopify.com
```
- Opens a browser tab → approve access → done
- Credentials are stored locally, persists across sessions

### If the OAuth callback gives a different domain
Shopify sometimes returns an internal domain instead of your store domain.
Use whatever domain it returned for all `--store=` flags after that.

**Our store has two domains:**
- `athlents.myshopify.com` → use for `shopify theme` commands
- `euzrz8-u5.myshopify.com` → use for `shopify store execute` (GraphQL) commands

### Re-authenticate with extra scopes
```powershell
shopify auth login --store=athlents.myshopify.com --scopes=read_products,write_products,read_publications,write_publications
```

---

## 2. Shopify CLI — Theme Commands

All run from inside the theme folder:
```powershell
cd "c:\Users\proto\OneDrive\Documents\codes\shopify customizations\Dawn-Dev"
```

| What | Command |
|---|---|
| Start local dev server | `shopify theme dev --store=athlents.myshopify.com --store-password=Snoopyclothing --ignore="*.tmp*"` |
| Push changes to live theme | `shopify theme push --store=athlents.myshopify.com --theme=146788712610 --allow-live --ignore="*.tmp*"` |
| Pull latest live theme | `shopify theme pull --store=athlents.myshopify.com --theme=146788712610` |
| List all themes | `shopify theme list --store=athlents.myshopify.com` |

**`--ignore="*.tmp*"`** — suppresses Windows temp file upload errors (always use this)  
**`--allow-live`** — required when pushing to the currently published/live theme  
**`--theme=146788712610`** — our live Dawn theme ID

---

## 3. GraphQL — How It Works

Shopify's Admin API uses GraphQL. You write a **query** (read) or **mutation** (write/update) and run it against the store.

### Running a GraphQL operation

**Method A — inline string (quick one-liners):**
```powershell
shopify store execute --store=euzrz8-u5.myshopify.com --query "query { shop { name } }"
```

**Method B — from a file (recommended for anything longer):**
```powershell
shopify store execute --store=euzrz8-u5.myshopify.com --query-file "path\to\operation.graphql"
```

**For mutations (writes), always add `--allow-mutations`:**
```powershell
shopify store execute --store=euzrz8-u5.myshopify.com --allow-mutations --query-file "path\to\mutation.graphql"
```

---

## 4. GraphQL File Examples

### Query — read a product
```graphql
query {
  productByHandle(handle: "loose-fit-pants") {
    id
    title
    descriptionHtml
  }
}
```

### Query — read a collection
```graphql
query {
  collectionByHandle(handle: "loose-fit-pants") {
    id
    title
    descriptionHtml
  }
}
```

### Query — list all products
```graphql
query {
  products(first: 10) {
    nodes {
      id
      title
      handle
    }
  }
}
```

### Mutation — update product description
```graphql
mutation {
  productUpdate(input: {
    id: "gid://shopify/Product/PRODUCT_ID_HERE"
    descriptionHtml: "<p>Your new description HTML here.</p>"
  }) {
    product { id title }
    userErrors { field message }
  }
}
```

### Mutation — update collection description
```graphql
mutation {
  collectionUpdate(input: {
    id: "gid://shopify/Collection/COLLECTION_ID_HERE"
    descriptionHtml: ""
  }) {
    collection { id title }
    userErrors { field message }
  }
}
```

### Mutation — update navigation menu
```graphql
mutation {
  menuUpdate(id: "gid://shopify/Menu/MENU_ID_HERE", title: "Main menu", items: [
    { title: "Home", url: "/" },
    { title: "Shop", url: "/collections/loose-fit-pants" }
  ]) {
    menu { id title items { title url } }
    userErrors { field message }
  }
}
```

### Mutation — create a page
```graphql
mutation {
  pageCreate(page: {
    title: "My Page"
    handle: "my-page"
    templateSuffix: "my-page"
  }) {
    page { id handle title }
    userErrors { field message }
  }
}
```

### Mutation — publish a collection to storefront
```graphql
mutation {
  publishablePublish(
    id: "gid://shopify/Collection/COLLECTION_ID_HERE"
    input: { publicationId: "gid://shopify/Publication/174651146402" }
  ) {
    publishable { ... on Collection { id title } }
    userErrors { field message }
  }
}
```

---

## 5. Key IDs (Athlents Store)

| Item | ID |
|---|---|
| Live theme | `146788712610` |
| Main menu | `gid://shopify/Menu/232405631138` |
| Online Store publication | `gid://shopify/Publication/174651146402` |
| Featured collection | `gid://shopify/Collection/QUERY_FOR_IT` |
| Product: Loose Fit Pants | `gid://shopify/Product/8905416310946` |
| Product: Sweatpants | `gid://shopify/Product/8905425617058` |
| Collection: Loose Fit Pants | `gid://shopify/Collection/325578490018` |
| New Releases page | `gid://shopify/Page/115765018786` |

---

## 6. Workflow Summary

```
Edit files locally (Dawn-Dev folder)
       ↓
shopify theme dev   ← preview at http://127.0.0.1:9292
       ↓
happy with changes?
       ↓
shopify theme push  ← goes live immediately
       ↓
need to update product/collection data?
       ↓
write .graphql file → shopify store execute
```

---

## 7. File Structure (What We Edit)

| File | What it controls |
|---|---|
| `templates/index.json` | Homepage sections and settings |
| `templates/collection.json` | Collection page layout |
| `templates/product.json` | Product detail page layout |
| `templates/page.*.json` | Custom page templates (e.g. page.new-releases.json) |
| `sections/header-group.json` | Header + announcement bar |
| `sections/footer-group.json` | Footer |
| `config/settings_data.json` | Global theme settings (fonts, colors, spacing) |
| `sections/*.liquid` | Section logic and markup |
