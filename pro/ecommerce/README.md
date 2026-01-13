# FlinUI PRO E-commerce Components

**Professional e-commerce components for online stores and marketplaces.**

Built with FLIN's zero-import philosophy and African Dusk design system.

---

## 📦 Available Components (14 Total)

### Core Product Display (Session 096 - NEW!)
1. **ProductCard** - Full-featured product card with image, pricing, rating, badges, and CTA
2. **ProductCardGrid** - Responsive grid layout with 2-4 columns, loading states, and animations
3. **ProductGallery** - Multi-image gallery with thumbnails, zoom, fullscreen, and autoplay
4. **ProductQuickview** - Modal quick view with gallery, variant selector, and add to cart
5. **ProductVariantSelector** - Size/color/material picker with visual swatches and availability

### Product Information
6. **ProductPricing** - Display product prices with sale pricing and discount badges
7. **ProductRating** - Star rating display with review count and optional link
8. **ProductBadge** - Badge component for product labels (Sale, New, Out of Stock, etc.)

### Reviews & Social Proof
9. **ProductReviews** - Review list with filters, sorting, and pagination
10. **ProductReviewForm** - Submit review form with rating selector and validation

### Additional Features
11. **ProductImageZoom** - Advanced image zoom with magnifier lens
12. **ProductCompare** - Side-by-side product comparison
13. **ProductCardList** - List view alternative to grid
14. **RecentlyViewed** - Recently viewed products carousel

---

## 🎨 Design Philosophy

**100% Design Tokens** - Zero hardcoded colors!

### African Dusk Theme:
- `--flin-accent-gold` - Primary CTAs and accents
- `--flin-bg-deep` - Base background (#0a0a0f)
- `--flin-bg-surface` - Card backgrounds (#12121a)
- `--flin-bg-elevated` - Elevated elements (#1a1a25)
- `--flin-text-primary` - Main text (#f5f5f7)
- `--flin-text-secondary` - Secondary text (#a0a0b0)

### Key Features:
- Smooth transitions and hover effects
- Responsive design (320px to 1920px+)
- Accessibility built-in (ARIA labels, semantic HTML)
- Production-ready quality

---

## 🚀 Quick Examples

### ProductCard
```flin
<ProductCard
    image="/product.jpg"
    title="African Sunset Hoodie"
    description="Premium cotton hoodie with hand-drawn design"
    price={89.99}
    originalPrice={129.99}
    rating={4.5}
    reviewCount={128}
    badge="Sale"
    badgeVariant="gold"
    onAddToCart={handleAddToCart}
    onQuickView={handleQuickView}
/>
```

### ProductCardGrid
```flin
<ProductCardGrid
    products={productsArray}
    columns={3}
    gap="md"
    cardVariant="default"
    showRating={true}
    showDescription={true}
    onAddToCart={handleAddToCart}
    onQuickView={handleQuickView}
/>
```

### ProductGallery
```flin
<ProductGallery
    images={[
        { url: "/img1.jpg", alt: "Front view", thumbnail: "/thumb1.jpg" },
        { url: "/img2.jpg", alt: "Back view", thumbnail: "/thumb2.jpg" }
    ]}
    aspectRatio="square"
    thumbnailPosition="bottom"
    showZoom={true}
    showFullscreen={true}
/>
```

### ProductQuickview
```flin
<ProductQuickview
    isOpen={showModal}
    onClose={handleClose}
    product={selectedProduct}
    onAddToCart={handleAddToCart}
    onViewFullDetails={handleViewDetails}
/>
```

### ProductVariantSelector
```flin
<ProductVariantSelector
    variants={[
        { type: "size", name: "M", value: "medium", available: true },
        { type: "color", name: "Gold", value: "gold", color: "#d4a853", available: true }
    ]}
    selected={selectedVariant}
    onSelect={handleVariantSelect}
    layout="inline"
    size="md"
/>
```

---

## 📋 Props Reference

### ProductCard Props
- `image` - Product image URL (text)
- `title` - Product name (text)
- `description` - Product description (text)
- `price` - Product price (number)
- `originalPrice` - Original price for discount display (number or none)
- `currency` - Currency code (text, default "USD")
- `rating` - Product rating 0-5 (number)
- `reviewCount` - Number of reviews (number)
- `badge` - Badge text (text or none)
- `badgeVariant` - Badge color: "gold", "emerald", "rose" (text)
- `inStock` - Stock status (bool)
- `onAddToCart` - Add to cart handler (function or none)
- `onQuickView` - Quick view handler (function or none)
- `variant` - Card style: "default", "compact", "minimal" (text)
- `showRating` - Show rating display (bool)
- `showDescription` - Show description text (bool)

### ProductCardGrid Props
- `products` - Array of product objects (array)
- `columns` - Number of columns: 2, 3, 4 (number)
- `gap` - Gap between cards: "sm", "md", "lg" (text)
- `cardVariant` - Variant for all cards (text)
- `loading` - Show loading skeleton (bool)
- `emptyMessage` - Message when no products (text)
- `onProductClick`, `onAddToCart`, `onQuickView` - Event handlers

### ProductGallery Props
- `images` - Array of image objects with url, alt, thumbnail (array)
- `variant` - Layout: "default", "slider", "grid" (text)
- `aspectRatio` - Main image ratio: "square", "portrait", "landscape" (text)
- `thumbnailPosition` - Position: "bottom", "left", "right" (text)
- `showZoom` - Enable zoom on hover (bool)
- `showFullscreen` - Show fullscreen button (bool)
- `autoplay` - Autoplay slideshow (bool)
- `autoplayDelay` - Delay between slides in ms (number)

### ProductQuickview Props
- `isOpen` - Modal open state (bool)
- `onClose` - Close handler (function or none)
- `product` - Product object with all details (object or none)
- `onAddToCart` - Add to cart handler (function or none)
- `onViewFullDetails` - View full product page handler (function or none)

### ProductVariantSelector Props
- `variants` - Array of variant options (array)
- `selected` - Currently selected variant (object or none)
- `onSelect` - Selection handler (function or none)
- `layout` - Display layout: "inline", "grid", "dropdown" (text)
- `showUnavailable` - Show unavailable options (bool)
- `size` - Swatch size: "sm", "md", "lg" (text)

---

## 🎯 Component Patterns

### FLIN Syntax (NOT Svelte!)
```flin
// ✅ CORRECT FLIN syntax
{if condition}...{/if}
{for item in items}...{/for}
click={handler}

// ❌ WRONG (Svelte syntax)
{#if condition}
{#each items as item}
on:click={handler}
```

### Props Access Pattern
```flin
// ✅ CORRECT
title = props.title || "Default"
variant = props.variant || "primary"

// ❌ WRONG
title = title ?? "Default"
```

### Use `none` not `null`
```flin
// ✅ CORRECT
image = props.image || none
if image != none { ... }

// ❌ WRONG
image = props.image || null
```

### Browser Code in onMount
```flin
// ✅ CORRECT
onMount {
    window.addEventListener("resize", handleResize)
}

// ❌ WRONG (top-level if)
if typeof window != "undefined" { ... }
```

---

## 📂 Files

```
flinui/pro/ecommerce/
├── ProductCard.flin              (460 lines)
├── ProductCardGrid.flin          (286 lines)
├── ProductGallery.flin           (471 lines)
├── ProductQuickview.flin         (567 lines)
├── ProductVariantSelector.flin   (380 lines)
├── ProductPricing.flin           (175 lines)
├── ProductRating.flin            (208 lines)
├── ProductBadge.flin             (181 lines)
├── ProductReviews.flin           (404 lines)
├── ProductReviewForm.flin        (556 lines)
├── ProductImageZoom.flin         (321 lines)
├── ProductCompare.flin           (339 lines)
├── ProductCardList.flin          (367 lines)
├── RecentlyViewed.flin           (?)
├── index.flin
└── README.md (this file)
```

**Total: ~5,000+ lines of production-ready e-commerce components**

---

## 🧪 Demos

- **Full Demo:** `/examples/ecommerce-grid-gallery-demo.flin` (NEW!)
- **Reviews Demo:** `/examples/ecommerce-demo.flin`
- **Tokens Reference:** `/flinui/theme/tokens.flin`

---

## ✅ Quality Checklist

- [x] 100% design token usage (no hardcoded colors)
- [x] Declarative top-level (no `if` statements outside functions)
- [x] Proper FLIN syntax (not Svelte)
- [x] Props access pattern (`props.propName`)
- [x] Use `none` instead of `null`
- [x] Responsive design (320px to 1920px+)
- [x] Accessibility (ARIA labels, semantic HTML)
- [x] Smooth animations and transitions
- [x] Loading states and error handling
- [x] Production-ready quality

---

**Session:** 096
**Created:** January 2026
**Theme:** African Dusk (Dark mode first)
**Philosophy:** "If you know HTML, you know FLIN."
