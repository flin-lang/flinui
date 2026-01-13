# FlinUI PRO Product Card Components

## Overview

Five production-ready, pixel-perfect e-commerce product card components built with FLIN syntax. Each component is fully functional, uses design tokens (no hardcoded colors), and follows modern e-commerce UI patterns.

**Total Components:** 5
**Total Lines:** 2,166
**Design System:** FlinUI Design Tokens
**Status:** Production Ready ✓

---

## Components

### 1. ProductCardBasic.flin (~359 lines)

**Purpose:** Essential product card for grid layouts
**Best For:** Product listing pages, category views, search results

**Features:**
- Product image with smooth loading animation
- Product title (2-line truncation)
- Star rating with review count
- Price display with discount calculation
- Badge support (Sale, New, Featured)
- Stock status indicator
- Add to cart button
- Hover effects with image zoom
- Fully responsive

**Props:**
```flin
image: text (URL)
imageAlt: text
title: text
price: number
originalPrice: number | none
currency: text (USD, EUR, GBP)
rating: number (0-5)
reviewCount: number
badge: text | none
badgeColor: "gold" | "emerald" | "rose"
inStock: boolean
onAddToCart: function | none
```

**Usage Example:**
```flin
<ProductCardBasic
    image="/product-1.jpg"
    title="Premium Wireless Headphones"
    price={99.99}
    originalPrice={149.99}
    rating={4.5}
    reviewCount={128}
    badge="Sale"
    badgeColor="gold"
    inStock={true}
    onAddToCart={handleAddToCart}
/>
```

---

### 2. ProductCardHover.flin (~486 lines)

**Purpose:** Advanced card with rich hover interactions
**Best For:** Featured products, hero sections, premium displays

**Features:**
- All ProductCardBasic features plus:
- Advanced hover overlay with quick actions
- Quick View button with handler
- Wishlist/Love button with state
- Category label
- Image zoom on hover (1.10x scale)
- Smooth action button animations
- Bottom gradient overlay on hover
- Card lift effect (6px transform)

**Props:**
```flin
image: text
imageAlt: text
title: text
price: number
originalPrice: number | none
currency: text
rating: number
reviewCount: number
category: text
badge: text | none
badgeColor: "gold" | "emerald" | "rose"
inStock: boolean
onAddToCart: function | none
onQuickView: function | none
onWishlist: function | none
```

**Usage Example:**
```flin
<ProductCardHover
    image="/product-premium.jpg"
    title="Designer Watch"
    category="Accessories"
    price={299.99}
    rating={4.8}
    reviewCount={256}
    badge="Limited"
    badgeColor="rose"
    onAddToCart={handleCart}
    onQuickView={handleQuickView}
    onWishlist={handleWishlist}
/>
```

---

### 3. ProductCardCompact.flin (~433 lines)

**Purpose:** Horizontal compact layout for lists and sidebars
**Best For:** Cart items, related products, sidebar recommendations

**Features:**
- Horizontal layout (image left, content right)
- Smaller image (140x140px)
- Minimal content area
- Quick add to cart button
- Remove/action button
- Low stock indicator with count
- Compact price display
- Optimized for small spaces
- Mobile-responsive (stacks on small screens)

**Props:**
```flin
image: text
imageAlt: text
title: text
price: number
originalPrice: number | none
currency: text
rating: number
inStock: boolean
stockCount: number | none
badge: text | none
badgeColor: "gold" | "emerald" | "rose"
onAddToCart: function | none
onRemove: function | none
```

**Usage Example:**
```flin
<ProductCardCompact
    image="/product-2.jpg"
    title="USB-C Cable"
    price={12.99}
    originalPrice={19.99}
    rating={4.2}
    inStock={true}
    stockCount={3}
    badge="Sale"
    badgeColor="emerald"
    onAddToCart={handleAddToCart}
    onRemove={handleRemove}
/>
```

---

### 4. ProductCardLarge.flin (~484 lines)

**Purpose:** Detailed card with full product information
**Best For:** Featured products, product detail cards, premium showcases

**Features:**
- Large 4:3 aspect ratio image
- Full product description (3-line truncation)
- Features list with checkmarks
- Prominent rating display
- Large price section (4xl font)
- Multiple CTA buttons:
  - Primary: Add to Cart (full width)
  - Secondary: Quick View
  - Secondary: View Details
- Discount display with colored badge
- Stock status badge
- Elegant spacing and typography

**Props:**
```flin
image: text
imageAlt: text
title: text
description: text
price: number
originalPrice: number | none
currency: text
rating: number
reviewCount: number
features: array<text> | none
badge: text | none
badgeColor: "gold" | "emerald" | "rose"
inStock: boolean
onAddToCart: function | none
onQuickView: function | none
onViewDetails: function | none
```

**Usage Example:**
```flin
<ProductCardLarge
    image="/product-large.jpg"
    title="Professional Camera"
    description="High-performance DSLR with advanced autofocus"
    price={1299.99}
    originalPrice={1599.99}
    rating={4.9}
    reviewCount={512}
    features={[
        "4K Video Recording",
        "Weather Sealed Body",
        "Fast Autofocus System",
        "12fps Continuous Shooting"
    ]}
    badge="Best Seller"
    badgeColor="gold"
    inStock={true}
    onAddToCart={handleCart}
    onQuickView={handleQuickView}
    onViewDetails={handleDetails}
/>
```

---

### 5. ProductCardGrid.flin (~404 lines)

**Purpose:** Responsive grid container for all card types
**Best For:** Product listing pages, category pages, search results, collections

**Features:**
- Responsive grid layout (2, 3, 4 columns)
- Auto-flow grid support
- Configurable gap sizes (sm, md, lg)
- Support all 4 card variants (basic, hover, compact, large)
- Loading skeleton with pulse animation
- Empty state display
- Staggered fade-in animation
- Responsive breakpoints:
  - 1280px: 4 cols → 3 cols
  - 1024px: 3 cols → 2 cols
  - 768px: 2 cols
  - 640px: 1 col (mobile)
- Minimum card width support
- Auto-fit responsive flow

**Props:**
```flin
products: array<object>
columns: 2 | 3 | 4 (default 3)
gap: "sm" | "md" | "lg"
cardVariant: "basic" | "hover" | "compact" | "large"
onProductClick: function | none
onAddToCart: function | none
onQuickView: function | none
loading: boolean
emptyMessage: text
minCardWidth: text (e.g., "280px")
autoColumns: boolean
```

**Usage Example:**
```flin
<ProductCardGrid
    products={productList}
    columns={3}
    gap="md"
    cardVariant="basic"
    loading={isLoading}
    onAddToCart={handleAddToCart}
    onQuickView={handleQuickView}
    minCardWidth="280px"
/>
```

---

## Design Tokens Used

All components use FlinUI design tokens (zero hardcoded colors):

### Colors
- `var(--flin-accent-gold)` - Primary brand color
- `var(--flin-accent-gold-bright)` - Hover state
- `var(--flin-accent-emerald)` - Success/In stock
- `var(--flin-accent-rose)` - Error/Out of stock
- `var(--flin-accent-cyan)` - New/Featured
- `var(--flin-accent-violet)` - Limited/Premium

### Backgrounds
- `var(--flin-bg-surface)` - Card background
- `var(--flin-bg-elevated)` - Image backgrounds
- `var(--flin-bg-hover)` - Hover states
- `var(--flin-bg-error)` - Error backgrounds
- `var(--flin-bg-warning)` - Warning backgrounds

### Text
- `var(--flin-text-primary)` - Main text
- `var(--flin-text-secondary)` - Secondary text
- `var(--flin-text-muted)` - Muted text
- `var(--flin-text-inverse)` - On colored backgrounds

### Borders & Shadows
- `var(--flin-border-subtle)` - Subtle borders
- `var(--flin-border-medium)` - Medium borders
- `var(--flin-shadow-sm)` - Small shadow
- `var(--flin-shadow-md)` - Medium shadow
- `var(--flin-shadow-card-hover)` - Card hover shadow
- `var(--flin-shadow-glow-gold)` - Gold glow shadow

### Typography
- `var(--flin-text-2xs)` - Badge text
- `var(--flin-text-xs)` - Small text
- `var(--flin-text-sm)` - Small body
- `var(--flin-text-base)` - Body text
- `var(--flin-text-lg)` - Large text
- `var(--flin-text-2xl)` - Extra large
- `var(--flin-font-medium)` - Medium weight
- `var(--flin-font-semibold)` - Semibold
- `var(--flin-font-bold)` - Bold

### Spacing
- `var(--flin-space-1)` through `var(--flin-space-20)` - Consistent spacing

### Borders & Radius
- `var(--flin-radius-sm)` - Small radius
- `var(--flin-radius-md)` - Medium radius
- `var(--flin-radius-button)` - Button radius
- `var(--flin-radius-card)` - Card radius
- `var(--flin-radius-badge)` - Badge radius

### Transitions
- `var(--flin-transition-fast)` - Fast animation
- `var(--flin-transition-normal)` - Normal animation
- `var(--flin-transition-slow)` - Slow animation

---

## Best Practices

### 1. Choosing the Right Component

| Use Case | Component | Why |
|----------|-----------|-----|
| Grid listing | ProductCardBasic | Efficient, clean, responsive |
| Feature section | ProductCardHover | Rich interactions, engagement |
| Cart items | ProductCardCompact | Space-efficient, horizontal |
| Featured product | ProductCardLarge | Full details, prominent display |
| Grid layouts | ProductCardGrid | Responsive, supports all variants |

### 2. Prop Handling

```flin
// Always provide defaults
product = props.product || {}
image = product.image || "/placeholder.png"
price = product.price || 0

// Use 'none' instead of null/undefined
badge = product.badge || none

// Type-safe comparisons
inStock = product.inStock != false
hasDiscount = originalPrice != none && originalPrice > price
```

### 3. Event Handlers

```flin
// Always check if handler exists before calling
handleAddToCart = fn() {
    if onAddToCart != none && inStock {
        onAddToCart()
    }
}

// Pass product data to parent handlers
handleAddToCart = fn(product) {
    if onAddToCart != none {
        onAddToCart(product)
    }
}
```

### 4. Responsive Design

All components are mobile-optimized:
- Single column on mobile (< 640px)
- Two columns on tablet (768px)
- Three columns on desktop (1024px+)
- Four columns on large screens (1280px+)

### 5. Accessibility

- Semantic HTML elements
- Proper alt text on images
- Descriptive button labels
- Clear color contrast (WCAG AA)
- Keyboard navigable

---

## Animation Details

### Hover Effects
- **Image zoom:** 1.06x - 1.10x scale
- **Card lift:** 4px - 8px translateY
- **Transition timing:** 0.15s - 0.5s ease-out
- **Button interactions:** Subtle translate on hover/active

### Loading State
- **Skeleton pulse:** 1.5s infinite animation
- **Opacity fade:** 0 → 1 on image load

### Grid Items
- **Fade in animation:** 0.5s ease-out
- **Staggered delays:** 0-550ms per item (12 items)
- **Smooth entrance:** Subtle translateY from bottom

---

## Customization

### Modify Colors

To change the gold accent throughout:
```css
:root {
    --flin-accent-gold: #your-color;
    --flin-accent-gold-bright: #your-hover-color;
}
```

### Adjust Spacing

Components respect the spacing scale:
```css
--flin-space-3: 0.75rem;    /* 12px */
--flin-space-4: 1rem;       /* 16px */
--flin-space-5: 1.25rem;    /* 20px */
```

### Custom Variants

Create variants by:
1. Duplicating the component
2. Modifying CSS classes
3. Adjusting prop structure
4. Testing responsive behavior

---

## Performance Notes

- **Lazy image loading:** Use native `load` event
- **Animation optimization:** CSS transforms (GPU accelerated)
- **Grid layout:** Modern CSS Grid for efficiency
- **No JavaScript bloat:** Pure FLIN + CSS
- **Responsive efficiency:** CSS media queries
- **Memory efficient:** No data cloning or transformation overhead

---

## Testing Checklist

- [ ] Images load correctly
- [ ] Hover effects smooth on desktop
- [ ] Mobile layout works (single column)
- [ ] Price formatting correct for different currencies
- [ ] Discount calculation accurate
- [ ] Rating stars display properly
- [ ] Buttons are clickable with proper states
- [ ] Out of stock state disables buttons
- [ ] Loading skeleton appears while loading
- [ ] Empty state shows when no products
- [ ] Responsive breakpoints work
- [ ] Keyboard navigation works
- [ ] Color contrast meets WCAG AA

---

## File Locations

```
flinui/ecommerce/
├── ProductCardBasic.flin         (359 lines)
├── ProductCardHover.flin         (486 lines)
├── ProductCardCompact.flin       (433 lines)
├── ProductCardLarge.flin         (484 lines)
├── ProductCardGrid.flin          (404 lines)
└── PRODUCT-CARDS-GUIDE.md        (This file)
```

---

## Browser Support

All components use modern CSS:
- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Mobile browsers (iOS Safari 14+, Chrome Android 90+)

---

## Future Enhancements

Potential additions:
- ProductCardCarousel - Horizontal scrolling cards
- ProductCardComparison - Side-by-side product comparison
- ProductCardVariants - Variant selector integration
- ProductCardReviews - Inline review snippets
- ProductCardArtwork - Image gallery support

---

## Support

For questions or issues:
1. Check component props documentation
2. Review FLIN-SYNTAX-FINAL.md
3. Check FlinUI design token definitions
4. Verify product data structure matches component expectations

---

**Version:** 1.0.0
**Last Updated:** January 2026
**Status:** Production Ready ✓
**FlinUI Version:** PRO

---

Generated with FlinUI PRO E-Commerce Component Suite
