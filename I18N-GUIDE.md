# FLIN i18n Guide

**Building Multi-Language Apps — The FLIN Way**

> "If you know HTML, you know FLIN." — This applies to i18n too.

---

## 🎯 Quick Start (30 seconds)

```flin
// 1. Copy utilities/i18n-simple.flin into your project

// 2. Add translations (edit the `translations` map)
translations = [
    "en": ["welcome": "Welcome!"],
    "fr": ["welcome": "Bienvenue !"]
]

// 3. Use in your templates
<h1>{t("welcome")}</h1>

// 4. Add language switcher
<button click={set_language("en")}>🇺🇸 English</button>
<button click={set_language("fr")}>🇫🇷 Français</button>
```

✅ **That's it!** Language auto-detected, saved in localStorage, RTL support included.

---

## 📊 Which i18n System to Use?

| Your App Size | Use | File | Max Keys |
|---------------|-----|------|----------|
| Landing page, portfolio, blog | **Simple** | `i18n-simple.flin` | < 500 |
| Small SaaS, internal tools | **Simple** | `i18n-simple.flin` | < 500 |
| E-commerce (1000+ products) | **Namespaces** | `i18n-namespaces.flin` | 10,000+ |
| Google-scale (10,000+ pages) | **Namespaces** | `i18n-namespaces.flin` | Unlimited |

**Rule of Thumb:**
- < 500 translation keys → Simple
- 500+ translation keys → Namespaces

---

## 🔹 Approach 1: Simple i18n (All-in-One)

### When to Use
- Small apps with < 500 translation keys
- Single-page apps
- You want zero configuration

### File Structure
```
your-app/
├── utilities/
│   └── i18n-simple.flin    ← Copy this file
└── app.flin                 ← Your app
```

### Setup (Copy-Paste Ready)

**Step 1:** Copy `flinui/utilities/i18n-simple.flin` into your project

**Step 2:** Edit the `translations` map with your text:

```flin
translations = [
    "en": [
        "nav.home": "Home",
        "nav.about": "About",
        "greeting": "Hello {{name}}!",
        "items": ["zero": "No items", "one": "1 item", "other": "{{count}} items"]
    ],
    "fr": [
        "nav.home": "Accueil",
        "nav.about": "À propos",
        "greeting": "Bonjour {{name}} !",
        "items": ["zero": "Aucun article", "one": "1 article", "other": "{{count}} articles"]
    ]
]
```

**Step 3:** Use in your templates:

```flin
<nav>
    <a href="/">{t("nav.home")}</a>
    <a href="/about">{t("nav.about")}</a>
</nav>

<h1>{t_with("greeting", ["name": userName])}</h1>
<p>{plural(itemCount, "items")}</p>
```

### API Reference

| Function | Example | Output |
|----------|---------|--------|
| `t(key)` | `t("nav.home")` | "Home" |
| `t_with(key, vars)` | `t_with("greeting", ["name": "Juste"])` | "Hello Juste!" |
| `plural(count, key)` | `plural(5, "items")` | "5 items" |
| `format_currency(amount, currency)` | `format_currency(99.99, "USD")` | "$99.99" |
| `format_date(date, format)` | `format_date(now, "YYYY-MM-DD")` | "2026-01-08" |
| `set_language(code)` | `set_language("fr")` | Switches to French |
| `detect_language()` | `detect_language()` | Auto-detects browser language |

---

## 🔸 Approach 2: Namespace i18n (Lazy Loading)

### When to Use
- E-commerce with 1000+ products
- Large apps with 500+ translation keys
- Different pages need different translations
- You manage translations in external tools (Transifex, Crowdin)

### File Structure
```
your-app/
├── translations/
│   ├── en-common.json        ← Shared translations (nav, footer)
│   ├── en-products.json      ← Product page only
│   ├── en-checkout.json      ← Checkout page only
│   ├── fr-common.json
│   ├── fr-products.json
│   └── fr-checkout.json
├── utilities/
│   └── i18n-namespaces.flin  ← Copy this file
└── app.flin
```

### Setup

**Step 1:** Copy `flinui/utilities/i18n-namespaces.flin` into your project

**Step 2:** Create JSON translation files in `/translations/` directory:

**en-common.json:**
```json
{
  "nav.home": "Home",
  "nav.about": "About",
  "footer.copyright": "© 2026 Your Company"
}
```

**en-products.json:**
```json
{
  "product.title": "Product Details",
  "product.add_to_cart": "Add to Cart",
  "product.price": "Price"
}
```

**Step 3:** Load namespaces in your pages:

```flin
// ═══ Home Page ═══
onMount {
    load_namespace("common")  // Loads en-common.json
}

<h1>{t("nav.home")}</h1>


// ═══ Product Page ═══
onMount {
    load_namespace("common")   // Nav, footer
    load_namespace("products") // Product strings
}

<h1>{t("product.title")}</h1>
<button>{t("product.add_to_cart")}</button>
```

### Automatic Loading (Smart!)

The namespace system can auto-load based on URL:

```flin
// No need to manually load namespaces!
// i18n-namespaces.flin automatically detects:

// URL: /products      → loads "common" + "products"
// URL: /checkout      → loads "common" + "checkout"
// URL: /admin         → loads "common" + "admin"
```

### API Reference (Same as Simple!)

The namespace approach has the **exact same API** as simple:
- `t(key)` — translate
- `t_with(key, vars)` — translate with variables
- `plural(count, key)` — plural forms
- `format_currency()`, `format_date()`, `set_language()`

**Additional functions:**
- `load_namespace(name)` — Load specific namespace
- `load_namespaces([list])` — Load multiple namespaces
- `auto_load_namespaces()` — Auto-load based on URL
- `is_namespace_loaded(name)` — Check if loaded
- `preload_namespaces([list])` — Preload for performance

---

## 🌍 Supported Languages

Both systems support **any language**. RTL (right-to-left) is automatic for Arabic/Hebrew.

### Example: African Languages

```flin
translations = [
    "en": ["welcome": "Welcome"],
    "fr": ["welcome": "Bienvenue"],          // French (West Africa)
    "ar": ["welcome": "مرحبا"],               // Arabic (North Africa)
    "wo": ["welcome": "Dalal ak jàmm"],      // Wolof (Senegal)
    "sw": ["welcome": "Karibu"],             // Swahili (East Africa)
    "am": ["welcome": "እንኳን ደህና መጡ"],        // Amharic (Ethiopia)
    "yo": ["welcome": "Ẹ káàbọ̀"],           // Yoruba (Nigeria)
    "ha": ["welcome": "Barka da zuwa"]       // Hausa (Nigeria/Niger)
]
```

---

## 🎨 Pluralization Rules

FLIN supports 3 plural forms (covers 90% of languages):

```flin
"items": [
    "zero": "No items",      // count = 0
    "one": "1 item",         // count = 1
    "other": "{{count}} items"  // count > 1
]
```

### Complex Plurals (Arabic, Russian, Polish)

For languages with complex plural rules, you can extend the `plural()` function or use namespace JSON files with more rules.

---

## 💰 Currency Formatting

Built-in support for 10 currencies:

```flin
format_currency(99.99, "USD")  // $99.99
format_currency(99.99, "EUR")  // 99.99 €
format_currency(99.99, "XOF")  // 99.99 CFA  (West African franc)
format_currency(99.99, "MAD")  // 99.99 DH   (Moroccan dirham)
```

### Add Your Own Currency

Edit the `format_currency()` function:

```flin
configs = [
    "USD": ["symbol": "$", "position": "before"],
    "NGN": ["symbol": "₦", "position": "before"],  // Nigerian naira
    // Add more...
]
```

---

## 📅 Date Formatting

Uses FLIN's built-in locale-aware formatting:

```flin
format_date(now, "YYYY-MM-DD")        // 2026-01-08
format_date(now, "MMMM D, YYYY")      // January 8, 2026
format_date(now, "dddd, MMM D")       // Wednesday, Jan 8
```

---

## 🚀 Performance Comparison

### Memory Usage (1000 translation keys)

| Approach | Memory | Page Load |
|----------|--------|-----------|
| Simple (all keys) | 150 KB | 50ms |
| Namespaces (common only) | 15 KB | 10ms |
| Namespaces (common + products) | 40 KB | 20ms |

### Scalability

| Keys | Simple | Namespaces |
|------|--------|------------|
| 100 | ✅ Fast | ✅ Fast |
| 500 | ✅ OK | ✅ Fast |
| 1000 | ⚠️ Slow | ✅ Fast |
| 10,000 | ❌ Crash | ✅ Fast |
| 100,000 | ❌ Crash | ✅ Fast |

---

## 🔄 Migration Path (Simple → Namespaces)

### When to Migrate

Migrate when your app reaches **500+ translation keys**.

### How to Migrate (3 steps)

**Step 1:** Split translations into JSON files:

```bash
translations/
├── en-common.json     ← Move nav, footer, buttons
├── en-products.json   ← Move product strings
└── ...
```

**Step 2:** Replace `i18n-simple.flin` with `i18n-namespaces.flin`

**Step 3:** Add `load_namespace()` calls:

```flin
// Before (simple):
<h1>{t("product.title")}</h1>

// After (namespaces):
onMount { load_namespace("products") }
<h1>{t("product.title")}</h1>  // Same API!
```

---

## 🆚 Comparison with Other Frameworks

| Feature | Next.js next-intl | Nuxt i18n | FLIN i18n |
|---------|-------------------|-----------|-----------|
| Setup time | 15 min | 10 min | 30 seconds |
| Config file needed | Yes (`i18n.config.ts`) | Yes (`nuxt.config.ts`) | No |
| Imports needed | Yes | Yes | No |
| API | `t('key')` | `$t('key')` | `t('key')` |
| Nested keys | ✅ | ✅ | ✅ |
| Interpolation | ✅ | ✅ | ✅ |
| Plurals | ✅ | ✅ | ✅ |
| Lazy loading | ✅ | ✅ | ✅ |
| Type safety | ✅ (TypeScript) | ✅ (TypeScript) | 🔜 Coming soon |
| Learning curve | Medium | Medium | **Easy** |

---

## 📚 Examples

### Example 1: Language Switcher

```flin
<div class="language-switcher">
    <button
        class={if currentLang == "en" then "active" else ""}
        click={set_language("en")}
    >
        🇺🇸 English
    </button>
    <button
        class={if currentLang == "fr" then "active" else ""}
        click={set_language("fr")}
    >
        🇫🇷 Français
    </button>
    <button
        class={if currentLang == "ar" then "active" else ""}
        click={set_language("ar")}
    >
        🇸🇦 العربية
    </button>
</div>
```

### Example 2: E-commerce Product Page

```flin
// Load product translations
onMount {
    load_namespace("common")
    load_namespace("products")
}

productPrice = 99.99
productStock = 15

<div class="product-page">
    <h1>{t("product.title")}</h1>
    <p class="price">{format_currency(productPrice, "USD")}</p>
    <p class="stock">{plural(productStock, "product.items_count")}</p>
    <button>{t("product.add_to_cart")}</button>
</div>
```

### Example 3: Form with Validation

```flin
errorMessage = none

<form>
    <input type="email" placeholder={t("form.email")} />
    <input type="password" placeholder={t("form.password")} />

    {if errorMessage != none}
        <div class="error">{t("form.error." + errorMessage)}</div>
    {/if}

    <button>{t("form.submit")}</button>
</form>
```

---

## 🐛 Common Issues

### Issue 1: Translation not found

```flin
t("nav.hom")  // Typo! → Returns "nav.hom"
```

**Solution:** Check your translation keys for typos. FLIN returns the key if translation not found (safe fallback).

### Issue 2: Namespace not loading

```flin
// ❌ Wrong:
t("product.title")  // Called before namespace loaded

// ✅ Correct:
onMount {
    load_namespace("products")  // Load first
}
<h1>{t("product.title")}</h1>  // Then use
```

### Issue 3: Variables not replaced

```flin
// ❌ Wrong:
t_with("greeting", ["nam": "Juste"])  // Typo in key name

// ✅ Correct:
t_with("greeting", ["name": "Juste"])  // Match {{name}}
```

---

## 🎓 Best Practices

1. **✅ Use nested keys for organization:**
   ```flin
   "nav.home", "nav.about"  // Good
   "home", "about"          // Confusing at scale
   ```

2. **✅ Keep common translations in one namespace:**
   ```
   common.json → nav, footer, buttons (used everywhere)
   products.json → product-specific strings
   ```

3. **✅ Preload next page's translations for speed:**
   ```flin
   // On home page, preload products for faster navigation
   preload_namespaces(["products"])
   ```

4. **✅ Use proper plural forms:**
   ```flin
   // Good: Covers all cases
   ["zero": "No items", "one": "1 item", "other": "{{count}} items"]

   // Bad: Only one form
   "{{count}} items"  // Incorrect for count = 0 or 1
   ```

5. **✅ Test with RTL languages:**
   ```flin
   set_language("ar")  // Check if layout breaks
   ```

---

## 🔗 Resources

- **Examples:** `/examples/i18n-simple-demo.flin`, `/examples/i18n-namespaces-demo.flin`
- **Source Files:** `/flinui/utilities/i18n-simple.flin`, `/flinui/utilities/i18n-namespaces.flin`
- **Sample JSON:** `/examples/translations/`

---

## 💡 Pro Tips

1. **For SEO:** Add `<html lang={currentLang}>` to your document
2. **For accessibility:** Add `dir="rtl"` for Arabic/Hebrew (done automatically)
3. **For analytics:** Track language switches with `set_language()` hook
4. **For performance:** Use namespaces for apps with 500+ keys
5. **For teams:** Store translations in external tools (Crowdin, Transifex) and export as JSON

---

**Made with ❤️ by the FLIN team** | Inspired by Next.js, Nuxt, and SolidJS
