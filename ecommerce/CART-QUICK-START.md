# Shopping Cart Components - Quick Start Guide

Get started with FlinUI PRO cart components in 5 minutes.

---

## 🚀 Quick Example

```flin
// Minimal working cart
cartItems = [
    { id: "1", name: "Product", price: 99, quantity: 1 }
]

<div>
    <!-- Badge in header -->
    <CartBadge itemCount={1} />

    <!-- Cart page -->
    <CartItem
        name="Product"
        price={99}
        quantity={1}
    />

    <CartSummary
        subtotal={99}
        onCheckout={() => print("Checkout!")}
    />
</div>
```

---

## 📦 The 5 Components

### 1. CartBadge - Header Icon
```flin
<CartBadge itemCount={5} onClick={openCart} />
```

### 2. CartItem - Product Card
```flin
<CartItem
    name="Headphones"
    price={299}
    quantity={1}
    onRemove={handleRemove}
/>
```

### 3. CartEmptyState - No Items
```flin
<CartEmptyState
    onCtaClick={browseProducts}
/>
```

### 4. CartSummary - Totals & Checkout
```flin
<CartSummary
    subtotal={299}
    tax={23.92}
    onCheckout={checkout}
/>
```

### 5. CartDrawer - Slide-in Cart
```flin
<CartDrawer
    isOpen={true}
    items={cartItems}
    onClose={closeDrawer}
/>
```

---

## 🎯 Common Patterns

### Pattern 1: Basic Cart Page
```flin
cartItems = [/* items */]
subtotal = 299

<div>
    {if cartItems.length > 0}
        {for item in cartItems}
            <CartItem {...item} />
        {/for}
        <CartSummary subtotal={subtotal} />
    {else}
        <CartEmptyState />
    {/if}
</div>
```

### Pattern 2: Header with Badge
```flin
itemCount = 3
drawerOpen = false

<header>
    <CartBadge
        itemCount={itemCount}
        onClick={() => drawerOpen = true}
    />

    <CartDrawer
        isOpen={drawerOpen}
        items={cartItems}
        onClose={() => drawerOpen = false}
    />
</header>
```

### Pattern 3: Add to Cart Flow
```flin
fn addToCart(product) {
    cartItems.push({
        id: product.id,
        name: product.name,
        price: product.price,
        quantity: 1
    })
    showPulse = true  // Animate badge
    drawerOpen = true  // Open drawer
}

<CartBadge
    itemCount={cartItems.length}
    showPulse={showPulse}
/>
```

---

## 🔧 Essential Props

### CartBadge
- `itemCount` - Number to display
- `onClick` - What to do on click

### CartItem
- `name`, `price`, `quantity` - Product info
- `onRemove` - Delete handler
- `onQuantityChange` - Update quantity

### CartSummary
- `subtotal`, `tax`, `shipping` - Money
- `onCheckout` - Checkout button

### CartDrawer
- `isOpen` - Show/hide drawer
- `items` - Cart items array
- `onClose` - Close handler

---

## 💡 Pro Tips

1. **Calculate totals in one place**
   ```flin
   fn updateCart() {
       subtotal = 0
       for item in cartItems {
           subtotal = subtotal + (item.price * item.quantity)
       }
   }
   ```

2. **Use pulse animation sparingly**
   ```flin
   fn addToCart(product) {
       cartItems.push(product)
       showPulse = true
       // Reset after animation
       setTimeout(() => showPulse = false, 800)
   }
   ```

3. **Promo codes return objects**
   ```flin
   fn applyPromo(code) {
       if code == "SAVE10" {
           { success: true }
       } else {
           { error: "Invalid code" }
       }
   }
   ```

4. **Free shipping threshold**
   ```flin
   <CartSummary
       shippingThreshold={50}  // Show progress bar
       shipping={subtotal > 50 ? 0 : 10}
   />
   ```

---

## ⚠️ Common Mistakes

❌ **Don't do this:**
```flin
// Missing quantity in calculation
total = item.price  // WRONG
```

✅ **Do this:**
```flin
total = item.price * item.quantity  // CORRECT
```

---

❌ **Don't do this:**
```flin
// Hardcoded currency
<span>${price}</span>  // WRONG - not flexible
```

✅ **Do this:**
```flin
currency = "$"  // or "€", "£", etc.
<CartSummary currency={currency} />  // CORRECT
```

---

❌ **Don't do this:**
```flin
// Mutating items directly
item.quantity = item.quantity + 1  // WRONG - won't trigger updates
```

✅ **Do this:**
```flin
// Use handler functions
onQuantityChange={(newQty) => handleUpdate(id, newQty)}
```

---

## 📱 Responsive Tips

```flin
<!-- Desktop: 2 columns -->
<div style="display: grid; grid-template-columns: 1fr 400px; gap: 24px;">
    <div>
        <!-- Cart items here -->
    </div>
    <CartSummary />
</div>

<!-- Mobile: Stack -->
@media (max-width: 768px) {
    div { grid-template-columns: 1fr !important; }
}
```

---

## 🎨 Customization

### Change primary color
All components use `--flin-primary` token:
```css
:root {
    --flin-primary: #3B82F6;  /* Default blue */
    --flin-primary-hover: #2563EB;
}
```

### Adjust spacing
```css
:root {
    --flin-space-4: 16px;  /* Default */
    --flin-space-6: 24px;  /* Default */
}
```

---

## 🐛 Debugging

### Badge not showing count?
```flin
<!-- Check: itemCount must be > 0 -->
<CartBadge itemCount={cartItems.length} />
```

### Drawer not opening?
```flin
<!-- Check: isOpen prop -->
<CartDrawer isOpen={drawerOpen} />
<!-- drawerOpen must be true -->
```

### Promo code not working?
```flin
<!-- Must return object with success or error -->
fn handlePromo(code) {
    { success: true }  // or { error: "message" }
}
```

---

## 📚 Next Steps

1. ✅ Read full docs: `README.md`
2. ✅ Try demo: `examples/ecommerce-cart-demo.flin`
3. ✅ Explore checkout components
4. ✅ Check design tokens in FlinUI theme

---

**Need help?** Check `flinui/ecommerce/README.md` for complete API reference.

**Author**: Claude (AI CTO, ZeroSuite Inc.)
**Date**: January 8, 2026
