# FlinUI PRO E-commerce Components

Production-ready shopping cart components for modern e-commerce applications.

**Version**: 1.0.0
**Status**: Production Ready
**Total Components**: 19 (5 Cart + 9 Checkout + 5 Payment)

---

## Shopping Cart Components (5)

### 1. CartBadge.flin

Shopping cart icon with animated item count badge.

**Props:**
- `itemCount` (Number) - Number of items in cart (default: 0)
- `size` (String) - Badge size: "sm" | "md" | "lg" (default: "md")
- `showPulse` (Boolean) - Show pulse animation (default: false)
- `onClick` (Function) - Click handler
- `variant` (String) - Color variant: "primary" | "secondary" | "danger" (default: "primary")

**Features:**
- Animated item count badge
- Pulse animation on cart updates
- Responsive icon sizing
- Accessibility support with ARIA labels

**Usage:**
```flin
<CartBadge
    itemCount={5}
    showPulse={true}
    onClick={handleCartClick}
    size="lg"
/>
```

---

### 2. CartItem.flin

Individual cart item card with quantity controls.

**Props:**
- `image` (String) - Product image URL (default: "")
- `name` (String) - Product name (default: "Product Name")
- `price` (Number) - Product price (default: 0)
- `quantity` (Number) - Item quantity (default: 1)
- `variant` (String) - Product variant (default: "")
- `size` (String) - Product size (default: "")
- `color` (String) - Product color (default: "")
- `maxQuantity` (Number) - Maximum allowed quantity (default: 99)
- `onQuantityChange` (Function) - Quantity change handler
- `onRemove` (Function) - Remove item handler

**Features:**
- Product image with fallback placeholder
- Quantity increment/decrement buttons
- Variant/size/color display
- Remove item button
- Price calculations
- Hover effects and transitions

**Usage:**
```flin
<CartItem
    image="product.jpg"
    name="Premium Headphones"
    price={299}
    quantity={2}
    size="One Size"
    color="Black"
    onQuantityChange={handleQtyChange}
    onRemove={handleRemove}
/>
```

---

### 3. CartEmptyState.flin

Empty cart state with illustration and call-to-action.

**Props:**
- `title` (String) - Empty state title (default: "Your cart is empty")
- `description` (String) - Description text (default: "Add items to get started")
- `ctaText` (String) - CTA button text (default: "Browse Products")
- `onCtaClick` (Function) - CTA click handler
- `showRecentItems` (Boolean) - Show recently viewed items (default: false)
- `recentItems` (Array) - Recently viewed items array (default: [])

**Features:**
- Custom SVG cart illustration with floating animation
- Recently viewed products grid
- Responsive layout
- Call-to-action button with hover effects

**Recent Items Format:**
```flin
recentItems = [
    { id: "1", name: "Product", price: 99, image: "url.jpg" },
    // ...
]
```

**Usage:**
```flin
<CartEmptyState
    title="Your cart is empty"
    description="Start shopping now!"
    ctaText="Browse Products"
    onCtaClick={handleBrowse}
    showRecentItems={true}
    recentItems={recentProducts}
/>
```

---

### 4. CartSummary.flin

Complete cart summary with totals and promo codes.

**Props:**
- `items` (Array) - Cart items for line-item display (default: [])
- `subtotal` (Number) - Cart subtotal (default: 0)
- `tax` (Number) - Tax amount (default: 0)
- `shipping` (Number) - Shipping cost (default: 0)
- `discount` (Number) - Discount amount (default: 0)
- `promoCode` (String) - Applied promo code (default: "")
- `onPromoApply` (Function) - Promo code application handler
- `onCheckout` (Function) - Checkout button handler
- `showLineItems` (Boolean) - Show individual line items (default: true)
- `shippingThreshold` (Number) - Free shipping threshold (default: 50)
- `currency` (String) - Currency symbol (default: "$")

**Features:**
- Line-by-line item breakdown
- Promo code input with validation
- Free shipping progress bar
- Subtotal, tax, shipping, discount calculation
- Bold total display
- Security badge
- Checkout CTA button

**Promo Handler Format:**
```flin
fn handlePromoApply(code) {
    if code == "VALID" {
        { success: true }
    } else {
        { error: "Invalid code" }
    }
}
```

**Usage:**
```flin
<CartSummary
    items={cartItems}
    subtotal={299}
    tax={23.92}
    shipping={0}
    discount={29.90}
    promoCode="SAVE10"
    onPromoApply={handlePromo}
    onCheckout={handleCheckout}
    shippingThreshold={50}
/>
```

---

### 5. CartDrawer.flin

Slide-in cart drawer with full cart management.

**Props:**
- `isOpen` (Boolean) - Drawer open state (default: false)
- `items` (Array) - Cart items (default: [])
- `subtotal` (Number) - Cart subtotal (default: 0)
- `itemCount` (Number) - Total item count (default: 0)
- `onClose` (Function) - Close drawer handler
- `onCheckout` (Function) - Checkout handler
- `onContinueShopping` (Function) - Continue shopping handler
- `onItemRemove` (Function) - Remove item handler
- `onQuantityChange` (Function) - Quantity change handler
- `position` (String) - Drawer position: "left" | "right" (default: "right")
- `currency` (String) - Currency symbol (default: "$")

**Features:**
- Slide-in animation from left or right
- Backdrop overlay
- Scrollable items list
- Inline quantity controls
- Empty state handling
- Subtotal calculation
- Sticky footer with checkout button
- Responsive (full-width on mobile)

**Item Format:**
```flin
items = [
    {
        id: "1",
        name: "Product Name",
        price: 99,
        quantity: 2,
        image: "url.jpg",
        variant: "Variant",
        size: "Size",
        color: "Color"
    }
]
```

**Usage:**
```flin
<CartDrawer
    isOpen={drawerOpen}
    items={cartItems}
    subtotal={598}
    itemCount={5}
    onClose={handleClose}
    onCheckout={handleCheckout}
    onItemRemove={handleRemove}
    onQuantityChange={handleQtyChange}
    position="right"
/>
```

---

## Design Tokens

All components use FlinUI design tokens for consistent styling:

**Colors:**
- `--flin-primary` - Primary brand color
- `--flin-neutral-*` - Neutral grays (50-900)
- `--flin-success` - Success states
- `--flin-danger` - Error/delete states
- `--flin-warning` - Warning states

**Spacing:**
- `--flin-space-1` through `--flin-space-12` - Consistent spacing scale

**Typography:**
- `--flin-font-sans` - Sans-serif font family
- `--flin-text-xs` through `--flin-text-3xl` - Font sizes
- `--flin-font-medium`, `--flin-font-semibold`, `--flin-font-bold` - Font weights

**Borders:**
- `--flin-radius-sm` through `--flin-radius-xl` - Border radius scale

**Transitions:**
- `--flin-transition-fast` - Quick transitions (150ms)
- `--flin-transition-normal` - Standard transitions (300ms)

---

## Complete Integration Example

```flin
// Cart state management
cartItems = []
drawerOpen = false
subtotal = 0
itemCount = 0

fn calculateTotals() {
    subtotal = 0
    itemCount = 0
    for item in cartItems {
        subtotal = subtotal + (item.price * item.quantity)
        itemCount = itemCount + item.quantity
    }
}

fn handleAddToCart(product) {
    cartItems.push({
        id: product.id,
        name: product.name,
        price: product.price,
        quantity: 1,
        image: product.image
    })
    calculateTotals()
    drawerOpen = true
}

fn handleRemoveItem(itemId) {
    cartItems = cartItems.filter(item => item.id != itemId)
    calculateTotals()
}

fn handleQuantityChange(itemId, newQty) {
    for item in cartItems {
        if item.id == itemId {
            item.quantity = newQty
        }
    }
    calculateTotals()
}

<div>
    <!-- Header with cart badge -->
    <header>
        <CartBadge
            itemCount={itemCount}
            onClick={() => drawerOpen = true}
        />
    </header>

    <!-- Cart page -->
    {if cartItems.length > 0}
        <div class="cart-layout">
            <div class="cart-items">
                {for item in cartItems}
                    <CartItem
                        image={item.image}
                        name={item.name}
                        price={item.price}
                        quantity={item.quantity}
                        onQuantityChange={(qty) => handleQuantityChange(item.id, qty)}
                        onRemove={() => handleRemoveItem(item.id)}
                    />
                {/for}
            </div>

            <CartSummary
                items={cartItems}
                subtotal={subtotal}
                tax={subtotal * 0.08}
                shipping={subtotal > 50 ? 0 : 10}
                onCheckout={handleCheckout}
            />
        </div>
    {else}
        <CartEmptyState
            onCtaClick={handleBrowseProducts}
        />
    {/if}

    <!-- Slide-out drawer -->
    <CartDrawer
        isOpen={drawerOpen}
        items={cartItems}
        subtotal={subtotal}
        itemCount={itemCount}
        onClose={() => drawerOpen = false}
        onCheckout={handleCheckout}
        onItemRemove={handleRemoveItem}
        onQuantityChange={handleQuantityChange}
    />
</div>
```

---

## Accessibility Features

All components include:
- ✅ ARIA labels and roles
- ✅ Keyboard navigation support
- ✅ Focus visible states
- ✅ Screen reader friendly
- ✅ Semantic HTML structure

---

## Browser Support

- ✅ Chrome/Edge 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Mobile browsers (iOS Safari, Chrome Mobile)

---

## Dark Mode

All components automatically support dark mode via `@media (prefers-color-scheme: dark)`.

---

## Performance

- **Optimized animations** - GPU-accelerated transforms
- **Lazy loading** - Images load on-demand
- **Minimal re-renders** - Efficient state management
- **Small footprint** - ~50KB total (uncompressed)

---

## Component Sizes

| Component | Lines of Code | File Size |
|-----------|--------------|-----------|
| CartBadge | 180 lines | 3.8 KB |
| CartItem | 320 lines | 8.5 KB |
| CartEmptyState | 280 lines | 8.0 KB |
| CartSummary | 450 lines | 13 KB |
| CartDrawer | 650 lines | 18 KB |

**Total**: ~1,880 lines | ~51 KB

---

## License

Part of FlinUI PRO - Production-ready components for FLIN applications.

**Author**: Claude (AI CTO, ZeroSuite Inc.)
**Date**: January 8, 2026
**FLIN Version**: 0.1.0+

---

---

## Payment Integration Components (5)

### 6. PaymentForm.flin

Complete payment form with card validation and type detection.

**Props:**
- `onSubmit` (Function) - Form submission handler
- `showSaveCard` (Boolean) - Show save card checkbox (default: true)
- `disabled` (Boolean) - Disable form (default: false)
- `processing` (Boolean) - Show processing state (default: false)

**Features:**
- Card number auto-formatting (4-digit groups)
- Card type detection (Visa, MC, Amex, Discover)
- Expiry date formatting (MM/YY)
- CVV validation (3-4 digits)
- Name on card field
- Save card checkbox
- Real-time validation
- Security badges

**Usage:**
```flin
<PaymentForm
    onSubmit={handlePayment}
    showSaveCard={true}
    processing={isProcessing}
/>
```

---

### 7. PaymentMethodSelector.flin

Visual payment method selection with icons and badges.

**Props:**
- `selectedMethod` (String) - Selected method (default: "card")
- `onMethodSelect` (Function) - Selection handler
- `showRecommended` (Boolean) - Show recommended badge (default: true)
- `disabled` (Boolean) - Disable selection (default: false)

**Features:**
- 4 payment method tiles (Card, PayPal, Apple Pay, Google Pay)
- Visual radio selection
- Icons for each type
- Recommended badge
- Security badges (SSL, PCI)
- Hover effects
- Responsive grid

**Usage:**
```flin
<PaymentMethodSelector
    selectedMethod={method}
    onMethodSelect={handleMethodChange}
/>
```

---

### 8. CreditCardInput.flin

Specialized credit card input with auto-formatting.

**Props:**
- `value` (String) - Initial card number (default: "")
- `onCardChange` (Function) - Card change handler
- `onExpiryChange` (Function) - Expiry change handler
- `onCVVChange` (Function) - CVV change handler
- `disabled` (Boolean) - Disable inputs (default: false)
- `size` (String) - Size: "sm", "md", "lg" (default: "md")

**Features:**
- Masked card input with formatting
- Card brand detection and icons
- Expiry auto-formatting (MM / YY)
- CVV with tooltip
- Validation states
- Multiple sizes
- Brand-specific validation

**Usage:**
```flin
<CreditCardInput
    onCardChange={handleCardChange}
    size="md"
/>
```

---

### 9. PayPalButton.flin

Official PayPal button styling with loading states.

**Props:**
- `amount` (Number) - Payment amount
- `currency` (String) - Currency code (default: "USD")
- `onClick` (Function) - Click handler
- `disabled` (Boolean) - Disable button (default: false)
- `loading` (Boolean) - Show loading state (default: false)
- `size` (String) - Size: "sm", "md", "lg" (default: "md")
- `variant` (String) - Color: "gold", "blue", "silver", "white" (default: "gold")

**Features:**
- Official PayPal design
- 4 color variants
- PayPal logo
- 3 size variants
- Loading spinner
- Success/error feedback
- Amount display
- Secure notice

**Usage:**
```flin
<PayPalButton
    amount={299.99}
    currency="USD"
    onClick={handlePayPalPayment}
    variant="gold"
/>
```

---

### 10. StripeCheckout.flin

Modern Stripe-styled checkout form.

**Props:**
- `amount` (Number) - Payment amount
- `currency` (String) - Currency code (default: "USD")
- `onSubmit` (Function) - Form submission handler
- `showQuickPay` (Boolean) - Show Apple/Google Pay (default: true)
- `testMode` (Boolean) - Show test mode badge (default: false)
- `disabled` (Boolean) - Disable form (default: false)

**Features:**
- Stripe Elements design
- Apple Pay / Google Pay quick buttons
- Complete form (email, card, name, address)
- Email validation
- Card validation and formatting
- Test mode indicator
- "Powered by Stripe" footer
- Responsive layout

**Usage:**
```flin
<StripeCheckout
    amount={299.99}
    currency="USD"
    onSubmit={handleStripePayment}
    showQuickPay={true}
    testMode={true}
/>
```

---

## Component Sizes (Updated)

| Component | Lines of Code | File Size | Category |
|-----------|--------------|-----------|----------|
| CartBadge | 180 lines | 3.8 KB | Cart |
| CartItem | 320 lines | 8.5 KB | Cart |
| CartEmptyState | 280 lines | 8.0 KB | Cart |
| CartSummary | 450 lines | 13 KB | Cart |
| CartDrawer | 650 lines | 18 KB | Cart |
| PaymentForm | 379 lines | 10 KB | Payment |
| PaymentMethodSelector | 242 lines | 7.5 KB | Payment |
| CreditCardInput | 354 lines | 10 KB | Payment |
| PayPalButton | 243 lines | 7.5 KB | Payment |
| StripeCheckout | 493 lines | 14 KB | Payment |

**Cart Total**: ~1,880 lines | ~51 KB
**Payment Total**: ~1,711 lines | ~49 KB
**Combined Total**: ~3,591 lines | ~100 KB

---

## See Also

- [FlinUI Component Guide](/flinui/FLIN-COMPONENT-GUIDE.md)
- [E-commerce Demo](/examples/ecommerce-cart-demo.flin)
- [E-commerce Components Demo](/examples/ecommerce-components-demo.flin)
- [Payment Components Demo](/examples/payment-components-demo.flin)
- [Payment Components Documentation](/flinui/ecommerce/PAYMENT-COMPONENTS.md)
