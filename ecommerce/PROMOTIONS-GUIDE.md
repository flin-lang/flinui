# FlinUI PRO - Promotions & Banners Components

**5 Production-Ready Promotional Components for E-commerce**

Drive conversions, create urgency, and boost sales with beautifully designed promotional components.

---

## 🎯 Components Overview

| Component | Purpose | Key Features | Lines |
|-----------|---------|--------------|-------|
| **PromoBanner** | Top-of-page promotions | Countdown timer, dismissible, eye-catching | ~100 |
| **FlashSale** | Urgency-driven sales | Stock progress, timer, product card | ~110 |
| **DealOfTheDay** | Featured daily deals | Ratings, features, full product details | ~105 |
| **FreeShippingBanner** | Shipping threshold tracker | Progress bar, dynamic messaging | ~85 |
| **CouponCode** | Promotional codes | Copy to clipboard, expiry tracking | ~95 |

---

## 📦 Installation

**NO INSTALLATION NEEDED!** These components work like HTML tags in FLIN.

Just place them in your `flinui/ecommerce/` directory and use them:

```flin
// No imports! Just use them:
<PromoBanner title="Sale!" ctaText="Shop Now" />
```

---

## 1️⃣ PromoBanner

Eye-catching promotional banner with countdown timer and dismissible option.

### Props

```flin
title              string    "Limited Time Offer!"     Banner title
description        string    "Get amazing deals..."    Banner description
ctaText           string    "Shop Now"                 CTA button text
ctaLink           string    "#"                        CTA link (if no onCta)
onCta             function  none                       CTA click handler
endTime           timestamp none                       Countdown end time (timestamp)
dismissible       boolean   true                       Show dismiss button
onDismiss         function  none                       Dismiss handler
variant           string    "primary"                  Style variant
showIcon          boolean   true                       Show tag icon
```

### Variants

- `primary` - Primary brand color gradient
- `secondary` - Secondary color gradient
- `danger` - Red urgent gradient
- `success` - Green success gradient
- `gradient` - Purple gradient (premium look)

### Usage Examples

```flin
// Basic banner
<PromoBanner
    title="Summer Sale 2026!"
    description="Get up to 70% off on selected items"
    ctaText="Shop Now"
/>

// With countdown timer
now = Date.now()
oneDay = 24 * 60 * 60 * 1000

<PromoBanner
    title="Flash Sale Ends Soon!"
    description="Last chance for amazing deals"
    ctaText="Shop Now"
    endTime={now + oneDay}
    onCta={handleShopClick}
    variant="danger"
/>

// Dismissible banner
<PromoBanner
    title="New Arrivals!"
    description="Check out our latest collection"
    ctaText="Explore"
    dismissible={true}
    onDismiss={handleDismiss}
    variant="gradient"
/>
```

### Features

- Smooth slide-in animation
- Countdown timer with days, hours, minutes, seconds
- Dismissible with smooth fade-out
- Fully responsive
- Multiple color variants
- Dark mode support

---

## 2️⃣ FlashSale

Flash sale card with countdown timer and stock progress bar.

### Props

```flin
title             string    "Flash Sale"               Sale badge text
productName       string    "Limited Edition..."       Product name
originalPrice     number    99.99                      Original price
salePrice         number    49.99                      Sale price
currency          string    "$"                        Currency symbol
endTime           timestamp none                       Sale end time
totalStock        number    100                        Total stock available
remainingStock    number    45                         Remaining stock
imageUrl          string    none                       Product image URL
onShopNow         function  none                       Shop Now click handler
variant           string    "hot"                      Style variant
```

### Variants

- `hot` - Red hot sale theme (default)
- `cool` - Blue cool deal theme
- `electric` - Purple electric theme

### Usage Examples

```flin
now = Date.now()
twoHours = 2 * 60 * 60 * 1000

<FlashSale
    title="FLASH SALE"
    productName="Premium Wireless Headphones"
    originalPrice={199.99}
    salePrice={99.99}
    endTime={now + twoHours}
    totalStock={100}
    remainingStock={23}
    imageUrl="/products/headphones.jpg"
    onShopNow={handleShopNow}
    variant="hot"
/>

// Cool variant
<FlashSale
    title="COOL DEAL"
    productName="Smart Watch Pro"
    originalPrice={299.99}
    salePrice={179.99}
    endTime={now + twoHours}
    totalStock={50}
    remainingStock={38}
    variant="cool"
/>
```

### Features

- Auto-calculated discount percentage
- Stock progress bar with urgency colors
  - Green: >50% stock remaining
  - Orange: 20-50% stock remaining
  - Red (pulsing): <20% stock remaining
- Countdown timer with hours, minutes, seconds
- Image zoom on hover
- Responsive grid layout
- Glowing border animation

---

## 3️⃣ DealOfTheDay

Daily deal showcase with full product details, ratings, and features.

### Props

```flin
title             string    "Deal of the Day"          Section title
productName       string    "Premium Product"          Product name
description       string    "Amazing product..."       Product description
originalPrice     number    199.99                     Original price
dealPrice         number    99.99                      Deal price
currency          string    "$"                        Currency symbol
imageUrl          string    none                       Product image URL
rating            number    4.5                        Star rating (0-5)
reviewCount       number    128                        Number of reviews
endTime           timestamp none                       Deal end time
features          array     []                         Product features list
onClaim           function  none                       Claim deal handler
badge             string    "Today Only"               Badge text
variant           string    "default"                  Style variant
```

### Variants

- `default` - Standard white background
- `premium` - Gold accent for premium deals
- `hot` - Red accent for hot deals

### Usage Examples

```flin
now = Date.now()
oneDay = 24 * 60 * 60 * 1000

<DealOfTheDay
    title="Deal of the Day"
    productName="Ultra HD 4K Smart TV - 55 inch"
    description="Stunning picture quality with HDR and Dolby Vision"
    originalPrice={799.99}
    dealPrice={499.99}
    imageUrl="/products/tv.jpg"
    rating={4.5}
    reviewCount={342}
    endTime={now + oneDay}
    features={[
        "4K Ultra HD Resolution",
        "Smart TV with Built-in Apps",
        "HDR & Dolby Vision",
        "3 HDMI Ports",
        "1 Year Warranty"
    ]}
    onClaim={handleDealClaim}
    badge="Today Only"
    variant="default"
/>
```

### Features

- Full 5-star rating display (supports half stars)
- Product features with checkmark icons
- Savings badge showing amount saved
- Countdown timer in header
- Large discount tag on image
- Image zoom on hover
- Fully responsive with mobile-optimized layout

---

## 4️⃣ FreeShippingBanner

Free shipping notification with dynamic progress bar and threshold tracker.

### Props

```flin
cartTotal            number    0                       Current cart total
threshold            number    50                      Free shipping threshold
currency             string    "$"                     Currency symbol
freeShippingMessage  string    "You qualify..."        Message when qualified
progressMessage      string    "Add {amount} more..."  Message when not qualified
variant              string    "primary"               Style variant
showIcon             boolean   true                    Show truck/check icon
position             string    "top"                   Animation direction
```

### Variants

- `primary` - Primary brand color
- `success` - Green success color
- `info` - Blue info color
- `accent` - Purple accent color

### Usage Examples

```flin
cartTotal = 35.00

<FreeShippingBanner
    cartTotal={cartTotal}
    threshold={50}
    currency="$"
    variant="primary"
    showIcon={true}
/>

// Custom messages
<FreeShippingBanner
    cartTotal={cartTotal}
    threshold={75}
    freeShippingMessage="Congratulations! FREE express shipping unlocked!"
    progressMessage="Add {amount} more for FREE express shipping"
    variant="success"
/>
```

### Features

- Dynamic progress bar (0-100%)
- Auto-calculated remaining amount
- Current vs. target amount display
- Smooth progress animation with shimmer effect
- Celebration animation when threshold reached
- Icon changes from truck to checkmark
- Fully responsive

---

## 5️⃣ CouponCode

Coupon code display with copy to clipboard and expiry tracking.

### Props

```flin
code             string    "SAVE20"              Coupon code
discount         string    "20% OFF"             Discount text
description      string    "Get 20% off..."      Description
expiryDate       timestamp none                  Expiry timestamp
minPurchase      number    none                  Minimum purchase amount
currency         string    "$"                   Currency symbol
termsUrl         string    "#"                   Terms & conditions URL
onCopy           function  none                  Copy handler
onApply          function  none                  Apply handler (shows button)
variant          string    "gradient"            Style variant
showTerms        boolean   true                  Show terms link
```

### Variants

- `gradient` - Colorful gradient border (default)
- `simple` - Clean white with primary border
- `elegant` - Subtle gray gradient
- `bold` - Primary color background

### Usage Examples

```flin
now = Date.now()
sevenDays = 7 * 24 * 60 * 60 * 1000

<CouponCode
    code="SAVE20"
    discount="20% OFF"
    description="Get 20% off your next purchase"
    expiryDate={now + sevenDays}
    minPurchase={50}
    currency="$"
    onCopy={handleCouponCopy}
    onApply={handleCouponApply}
    variant="gradient"
/>

// Simple variant
<CouponCode
    code="FIRST10"
    discount="$10 OFF"
    description="First-time customer discount"
    onCopy={handleCopy}
    variant="simple"
/>

// With apply button
<CouponCode
    code="FREESHIP"
    discount="FREE SHIPPING"
    description="Free shipping on all orders"
    onCopy={handleCopy}
    onApply={handleApply}
    variant="elegant"
/>
```

### Features

- One-click copy to clipboard
- Visual feedback when copied (checkmark + "Copied!")
- Countdown to expiry (updates every minute)
- Urgent styling when expiring soon (<48 hours)
- Decorative perforated edge circles
- Minimum purchase requirement display
- Optional apply button
- Terms & conditions link
- Multiple style variants

---

## 🎨 Design Tokens Used

All components use FLIN design tokens for consistency:

```css
/* Colors */
var(--flin-primary)
var(--flin-primary-dark)
var(--flin-secondary)
var(--flin-danger)
var(--flin-success)
var(--flin-warning)
var(--flin-info)
var(--flin-neutral-*)

/* Spacing */
var(--flin-space-1) through var(--flin-space-6)

/* Typography */
var(--flin-text-xs) through var(--flin-text-3xl)
var(--flin-font-sans)
var(--flin-font-mono)
var(--flin-font-bold)

/* Effects */
var(--flin-shadow-md)
var(--flin-shadow-lg)
var(--flin-shadow-xl)
var(--flin-radius-md)
var(--flin-radius-lg)
var(--flin-transition-base)
```

---

## 🚀 Best Practices

### 1. Timing Functions

Use consistent timing for countdown timers:

```flin
now = Date.now()

// Helper constants
oneHour = 60 * 60 * 1000
oneDay = 24 * 60 * 60 * 1000
oneWeek = 7 * 24 * 60 * 60 * 1000

// Set end times
flashSaleEnd = now + (2 * oneHour)    // 2 hours
dealEnd = now + oneDay                 // 24 hours
couponExpiry = now + oneWeek          // 7 days
```

### 2. Progressive Disclosure

Stack banners from most to least important:

```flin
<div style="display: flex; flex-direction: column; gap: 1rem;">
    <PromoBanner />           // Most important
    <FreeShippingBanner />    // Encourages higher cart value
    <CouponCode />            // Additional incentive
</div>
```

### 3. Urgency Hierarchy

- **Critical (< 2 hours)**: Use FlashSale with `variant="hot"`
- **Important (< 24 hours)**: Use DealOfTheDay or PromoBanner
- **Standard (< 7 days)**: Use CouponCode

### 4. Responsive Layouts

All components are fully responsive. For optimal mobile experience:

```flin
// Desktop: Side-by-side
<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 1rem;">
    <FlashSale ... />
    <FlashSale ... />
    <FlashSale ... />
</div>
```

### 5. Dark Mode

All components support dark mode automatically. No additional configuration needed.

---

## 📊 Component Combinations

### Homepage Hero Section

```flin
<div>
    <PromoBanner
        title="Summer Sale!"
        endTime={now + oneDay}
        variant="gradient"
    />

    <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 2rem; margin-top: 2rem;">
        <FlashSale ... />
        <FlashSale ... />
        <FlashSale ... />
    </div>
</div>
```

### Cart Page

```flin
<div>
    <FreeShippingBanner cartTotal={cartTotal} threshold={50} />

    // Cart items...

    <CouponCode
        code="CART10"
        discount="$10 OFF"
        onApply={applyCoupon}
    />
</div>
```

### Product Page

```flin
<div>
    <DealOfTheDay
        productName={product.name}
        originalPrice={product.price}
        dealPrice={product.salePrice}
        rating={product.rating}
        features={product.features}
    />

    <CouponCode
        code="FIRST15"
        discount="15% OFF"
        description="First-time buyer discount"
    />
</div>
```

---

## 🎯 Conversion Optimization Tips

1. **Use Countdown Timers**: Creates urgency and FOMO
2. **Show Stock Levels**: Low stock = higher conversion
3. **Clear CTAs**: "Shop Now", "Claim Deal" are action-oriented
4. **Progress Bars**: Visualize progress toward free shipping
5. **Social Proof**: Display ratings and review counts
6. **Multiple Variants**: A/B test different color schemes

---

## 📱 Accessibility

All components are built with accessibility in mind:

- ✅ Semantic HTML
- ✅ ARIA labels on interactive elements
- ✅ Keyboard navigation support
- ✅ Focus indicators
- ✅ Sufficient color contrast
- ✅ Responsive text sizing

---

## 🐘 The FLIN Way

Remember: **NO IMPORTS!**

```flin
// ❌ WRONG (JavaScript thinking)
import { PromoBanner } from "./PromoBanner.flin"

// ✅ CORRECT (FLIN way)
<PromoBanner title="Sale!" />
```

Components work like HTML tags. If you know HTML, you know FLIN.

---

## 📚 See Also

- [Cart & Checkout Components](./CART-QUICK-START.md)
- [Payment Components](./PAYMENT-COMPONENTS.md)
- [FlinUI Component Guide](../FLIN-COMPONENT-GUIDE.md)
- [E-commerce Demo](../../examples/ecommerce-promotions-demo.flin)

---

**Created with**: FLIN Language
**Author**: Claude (AI CTO, ZeroSuite Inc.)
**Last Updated**: January 8, 2026

🐘 **É flîn nù** - It Remembers Things
