# FlinUI PRO Product Cards — Quick Start

## The 5 Components at a Glance

| Component | Best For | Layout | Lines |
|-----------|----------|--------|-------|
| **ProductCardBasic** | Grid listings, categories | Vertical | 359 |
| **ProductCardHover** | Featured, hero sections | Vertical + overlay | 486 |
| **ProductCardCompact** | Cart, sidebars, lists | Horizontal | 433 |
| **ProductCardLarge** | Detail showcase, premium | Vertical, large | 484 |
| **ProductCardGrid** | Container for all | Grid layout | 404 |

## Basic Usage (5 Minutes)

### 1. Simple Grid

```flin
<ProductCardGrid
    products={products}
    columns={3}
    cardVariant="basic"
/>
```

### 2. Individual Card

```flin
<ProductCardBasic
    image="/watch.jpg"
    title="Premium Watch"
    price={299}
    originalPrice={399}
    rating={4.5}
    badge="Sale"
    onAddToCart={handleCart}
/>
```

### 3. With Features

```flin
<ProductCardLarge
    image="/camera.jpg"
    title="Pro Camera"
    description="High-performance DSLR"
    price={1299}
    features={["4K Video", "Weather Sealed", "Fast AF"]}
    onAddToCart={handleCart}
/>
```

### 4. Grid with Different Variant

```flin
<ProductCardGrid
    products={products}
    columns={4}
    gap="lg"
    cardVariant="hover"
    onAddToCart={handleCart}
    onQuickView={handleQuickView}
/>
```

### 5. Compact Card (Sidebar)

```flin
<ProductCardCompact
    image="/item.jpg"
    title="Item"
    price={29.99}
    rating={4}
    inStock={true}
    onAddToCart={handleCart}
/>
```

## Props Quick Reference

### All Cards Support

```flin
image          : string          // Image URL
imageAlt       : string          // Alt text
title          : string          // Product name
price          : number          // Current price
originalPrice  : number | none    // Original (for discount)
currency       : string          // "USD", "EUR", "GBP"
rating         : number (0-5)    // Star rating
badge          : string | none   // "Sale", "New", etc.
badgeColor     : "gold" | "emerald" | "rose"
inStock        : boolean         // Stock status
```

### Card-Specific Props

**Hover/Compact/Large:**
```flin
reviewCount    : number          // Number of reviews
category       : string          // Product category (Hover only)
description    : string          // Full description (Large only)
features       : array<string>   // Feature list (Large only)
stockCount     : number | none    // Qty in stock (Compact only)
```

### Handlers

```flin
onAddToCart    : function | none  // Add to cart handler
onQuickView    : function | none  // Quick view (Hover/Large)
onWishlist     : function | none  // Wishlist toggle (Hover)
onRemove       : function | none  // Remove item (Compact)
onViewDetails  : function | none  // Details page (Large)
```

### Grid-Only Props

```flin
products       : array<object>    // Product array
columns        : 2 | 3 | 4        // Grid columns
gap            : "sm" | "md" | "lg" // Gap size
cardVariant    : "basic" | "hover" | "compact" | "large"
loading        : boolean          // Show skeleton
emptyMessage   : string           // Empty state text
minCardWidth   : string           // Min card width
autoColumns    : boolean          // Auto-fit columns
```

## Data Structure

### Minimal Product Object

```flin
product = {
    image: "/photo.jpg",
    imageAlt: "Product",
    title: "Product Name",
    price: 99.99,
    inStock: true
}
```

### Complete Product Object

```flin
product = {
    // Basic
    image: "/photo.jpg",
    imageAlt: "Product photo",
    title: "Premium Headphones",
    description: "High-quality wireless headphones",
    price: 299.99,
    originalPrice: 399.99,
    currency: "USD",

    // Ratings & Reviews
    rating: 4.5,
    reviewCount: 128,

    // Stock
    inStock: true,
    stockCount: 5,

    // Display
    badge: "Sale",
    badgeColor: "gold",
    category: "Electronics",

    // Features (Large card)
    features: [
        "Noise Cancellation",
        "40-Hour Battery",
        "Premium Sound Quality"
    ]
}
```

## Common Tasks

### Show Product List

```flin
<ProductCardGrid
    products={allProducts}
    columns={3}
    cardVariant="basic"
    onAddToCart={handleAddToCart}
/>
```

### Add to Cart Handler

```flin
handleAddToCart = fn(product) {
    // Add product to cart
    cart = cart + [product]
}
```

### Toggle Wishlist

```flin
handleWishlist = fn(isWishlisted) {
    if isWishlisted {
        // Add to wishlist
    } else {
        // Remove from wishlist
    }
}
```

### Handle Quick View

```flin
handleQuickView = fn(product) {
    // Show modal with product details
    showModal = true
    selectedProduct = product
}
```

### Filter Products by Price

```flin
minPrice = 100
maxPrice = 500
filteredProducts = products
filtered = {}
for product in products {
    if product.price >= minPrice && product.price <= maxPrice {
        filtered = filtered + [product]
    }
}
filteredProducts = filtered
```

### Sort by Rating

```flin
sortedByRating = fn(products, desc) {
    // Products automatically sorted
    // (would implement sort logic)
    return products
}
```

## Styling & Theming

### Override Badge Colors

```css
.product-badge.gold {
    background: #custom-gold;
}
```

### Adjust Spacing

```css
:root {
    --flin-space-4: 1.2rem; /* Increase spacing */
    --flin-space-5: 1.5rem;
}
```

### Change Hover Effects

Edit component `<style>` section:
```css
.flin-product-card-basic:hover {
    transform: scale(1.02);    /* Instead of translateY */
}
```

## Responsive Behavior

All components auto-adjust:

| Screen | Columns | Layout |
|--------|---------|--------|
| Mobile (< 640px) | 1 | Stacked |
| Tablet (768px) | 2 | Side-by-side |
| Desktop (1024px) | 3 | Grid |
| Large (1280px+) | 4 | Wide grid |

**Compact card:** Horizontal → Vertical on mobile
**Large card:** Maintains aspect ratios at all sizes

## Accessibility

All components include:
- Semantic HTML elements
- Alt text on images
- Descriptive button labels
- Keyboard navigation
- WCAG AA color contrast
- Focus states

## Common Errors & Fixes

### Error: Component not found

```flin
// ❌ Wrong - No imports in FLIN
import { ProductCardBasic } from "./ProductCardBasic.flin"

// ✅ Right - Use like HTML
<ProductCardBasic ... />
```

### Error: undefined props

```flin
// ❌ Wrong - No defaults
title = props.title

// ✅ Right - Always provide defaults
title = props.title || "Product Name"
```

### Error: null/undefined values

```flin
// ❌ Wrong - Using null
badge = null

// ✅ Right - Use 'none'
badge = none
```

### Error: Hardcoded colors

```flin
// ❌ Wrong - No design tokens
color: #FFD700;

// ✅ Right - Use design tokens
color: var(--flin-accent-gold);
```

## Browser Support

✓ Chrome 90+
✓ Firefox 88+
✓ Safari 14+
✓ Edge 90+
✓ Mobile browsers (iOS Safari 14+, Chrome Android 90+)

## Performance Tips

1. **Use ProductCardGrid** for lists (optimized)
2. **Lazy load images** with native `loading="lazy"`
3. **Limit products per grid** (avoid loading 1000+ items)
4. **Use skeleton loading** (set `loading={true}`)
5. **Cache product data** (don't refetch on every render)

## Next Steps

1. ✓ Check `PRODUCT-CARDS-GUIDE.md` for detailed docs
2. ✓ Review `COMPONENTS-SUMMARY.txt` for technical specs
3. ✓ Copy examples above into your app
4. ✓ Replace image URLs with your products
5. ✓ Add handlers to connect to your store logic

## Getting Help

- **Syntax:** Check `FLIN-SYNTAX-FINAL.md`
- **Design tokens:** See FlinUI token definitions
- **Components:** Read full component files
- **Examples:** See demo files in `/examples`

---

**Version:** 1.0.0 | **Status:** Production Ready ✓
