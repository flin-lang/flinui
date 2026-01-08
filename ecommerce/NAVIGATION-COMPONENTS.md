# FlinUI PRO Store Navigation Components

**Status**: Production Ready ✅
**Created**: January 8, 2026
**Components**: 5 navigation components for e-commerce stores

---

## 📦 Components Overview

This collection provides comprehensive navigation solutions for e-commerce applications:

| Component | Purpose | Lines | Features |
|-----------|---------|-------|----------|
| **CategoryMenu** | Multi-level category navigation | ~100 | Expandable, icons, counts, active state |
| **Breadcrumbs** | Hierarchical page trail | ~80 | Home icon, separators, click navigation |
| **ProductFilters** | Complete filter sidebar | ~120 | Price, brand, color, size filters |
| **SearchBar** | Search with autocomplete | ~110 | Suggestions, recent searches, loading |
| **Pagination** | Page navigation controls | ~90 | Page numbers, size selector, range |

---

## 🚀 Quick Start

```flin
// NO IMPORTS NEEDED! Just use them:

<SearchBar
    placeholder="Search products..."
    onSearch={handleSearch}
    suggestions={suggestions}
/>

<Breadcrumbs
    items={breadcrumbItems}
    onItemClick={handleBreadcrumbClick}
/>

<CategoryMenu
    categories={categories}
    activeCategory={activeCategory}
    onCategoryClick={handleCategoryClick}
/>

<ProductFilters
    filters={filters}
    selectedFilters={selectedFilters}
    onFilterChange={handleFilterChange}
/>

<Pagination
    currentPage={currentPage}
    totalPages={totalPages}
    onPageChange={handlePageChange}
/>
```

---

## 1️⃣ CategoryMenu Component

### Purpose
Multi-level category navigation with expandable subcategories and active state indication.

### Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `categories` | Array | `[]` | Category data with subcategories |
| `activeCategory` | String | `""` | Currently active category ID |
| `onCategoryClick` | Function | - | Callback when category is clicked |
| `variant` | String | `"sidebar"` | Style variant: "sidebar", "horizontal" |
| `showIcons` | Boolean | `true` | Show category icons |
| `collapsible` | Boolean | `true` | Allow expanding/collapsing |
| `expandedCategories` | Array | `[]` | Initially expanded category IDs |

### Category Data Structure

```flin
categories = [
    [
        "id": "electronics",
        "label": "Electronics",
        "icon": "💻",
        "count": 245,
        "subcategories": [
            ["id": "laptops", "label": "Laptops", "count": 45],
            ["id": "phones", "label": "Phones", "count": 89]
        ]
    ]
]
```

### Example

```flin
categories = [
    ["id": "clothing", "label": "Clothing", "icon": "👔", "count": 432],
    ["id": "electronics", "label": "Electronics", "icon": "💻", "count": 245]
]

activeCategory = "clothing"

function handleCategoryClick(category) {
    activeCategory = category.id
    print("Navigate to: " + category.label)
}

<CategoryMenu
    categories={categories}
    activeCategory={activeCategory}
    onCategoryClick={handleCategoryClick}
    showIcons={true}
/>
```

### Features
- ✅ Multi-level hierarchy (categories + subcategories)
- ✅ Expandable/collapsible subcategories
- ✅ Active state highlighting
- ✅ Optional icons and item counts
- ✅ Keyboard navigation support
- ✅ Mobile responsive
- ✅ Sidebar and horizontal variants

---

## 2️⃣ Breadcrumbs Component

### Purpose
Navigation breadcrumb trail showing hierarchical page location (Home > Category > Product).

### Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `items` | Array | `[]` | Breadcrumb trail items |
| `separator` | String | `"/"` | Separator between items |
| `maxItems` | Number | `0` | Max items to show (0 = all) |
| `onItemClick` | Function | - | Callback when item is clicked |
| `showHomeIcon` | Boolean | `true` | Show home icon instead of text |
| `homeLabel` | String | `"Home"` | Home link label |
| `homeUrl` | String | `"/"` | Home link URL |

### Item Data Structure

```flin
items = [
    ["label": "Electronics", "url": "/electronics"],
    ["label": "Laptops", "url": "/electronics/laptops"],
    ["label": "Gaming", "url": "/electronics/laptops/gaming"]
]
```

### Example

```flin
breadcrumbItems = [
    ["label": "Women", "url": "/women"],
    ["label": "Shoes", "url": "/women/shoes"],
    ["label": "Sneakers", "url": "/women/shoes/sneakers"]
]

function handleBreadcrumbClick(item, index) {
    print("Navigate to: " + item.url)
}

<Breadcrumbs
    items={breadcrumbItems}
    separator="›"
    onItemClick={handleBreadcrumbClick}
    showHomeIcon={true}
/>
```

### Features
- ✅ Hierarchical navigation trail
- ✅ Customizable separators
- ✅ Home icon or text
- ✅ Click navigation
- ✅ Automatic truncation with ellipsis
- ✅ Responsive collapse on mobile
- ✅ Aria labels for accessibility

---

## 3️⃣ ProductFilters Component

### Purpose
Complete filter sidebar with multiple filter types: price ranges, brands, colors, sizes, etc.

### Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `filters` | Array | `[]` | Filter group configuration |
| `selectedFilters` | Array | `[]` | Selected filter IDs |
| `onFilterChange` | Function | - | Callback when filter toggled |
| `onClearAll` | Function | - | Callback for clear all |
| `showClearAll` | Boolean | `true` | Show clear all button |
| `collapsible` | Boolean | `true` | Allow collapsing groups |
| `priceRange` | Map | `["min": 0, "max": 1000]` | Price range |
| `currency` | String | `"$"` | Currency symbol |

### Filter Data Structure

```flin
filters = [
    [
        "id": "brand",
        "label": "Brand",
        "type": "checkbox",
        "options": [
            ["id": "apple", "label": "Apple", "count": 89],
            ["id": "dell", "label": "Dell", "count": 123]
        ]
    ],
    [
        "id": "color",
        "label": "Color",
        "type": "color",
        "options": [
            ["id": "black", "label": "Black", "color": "#000000", "count": 234],
            ["id": "silver", "label": "Silver", "color": "#C0C0C0", "count": 178]
        ]
    ]
]
```

### Example

```flin
filters = [
    [
        "id": "price",
        "label": "Price Range",
        "options": [
            ["id": "under-100", "label": "Under $100", "count": 234],
            ["id": "100-500", "label": "$100 - $500", "count": 456]
        ]
    ]
]

selectedFilters = ["under-100", "apple"]

function handleFilterChange(filterId) {
    if selectedFilters.includes(filterId) {
        selectedFilters = selectedFilters.filter(fn (id) { id != filterId })
    } else {
        selectedFilters = [...selectedFilters, filterId]
    }
}

<ProductFilters
    filters={filters}
    selectedFilters={selectedFilters}
    onFilterChange={handleFilterChange}
/>
```

### Features
- ✅ Multiple filter types (checkbox, color swatch, range)
- ✅ Color swatches with visual selection
- ✅ Active filter count badge
- ✅ Clear all filters button
- ✅ Collapsible filter groups
- ✅ Item count per option
- ✅ Scrollable with custom scrollbar
- ✅ Mobile responsive

---

## 4️⃣ SearchBar Component

### Purpose
Advanced search input with autocomplete suggestions, recent searches, and loading states.

### Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `placeholder` | String | `"Search products..."` | Input placeholder |
| `value` | String | `""` | Current search value |
| `onSearch` | Function | - | Callback when search submitted |
| `onInput` | Function | - | Callback on input change |
| `onFocus` | Function | - | Callback on focus |
| `onBlur` | Function | - | Callback on blur |
| `suggestions` | Array | `[]` | Autocomplete suggestions |
| `recentSearches` | Array | `[]` | Recent search history |
| `showSuggestions` | Boolean | `true` | Show suggestions dropdown |
| `showRecentSearches` | Boolean | `true` | Show recent searches |
| `loading` | Boolean | `false` | Show loading spinner |
| `disabled` | Boolean | `false` | Disable input |
| `size` | String | `"md"` | Size: "sm", "md", "lg" |
| `variant` | String | `"default"` | Variant: "default", "hero" |

### Suggestion Data Structure

```flin
suggestions = [
    ["text": "gaming laptop", "category": "Electronics"],
    ["text": "wireless mouse", "category": "Accessories"]
]

recentSearches = ["macbook", "keyboard", "monitor"]
```

### Example

```flin
searchQuery = ""
suggestions = [
    ["text": "wireless headphones", "category": "Audio"],
    ["text": "bluetooth speaker", "category": "Audio"]
]

function handleSearch(query) {
    print("Searching for: " + query)
}

<SearchBar
    placeholder="What are you looking for?"
    value={searchQuery}
    onSearch={handleSearch}
    suggestions={suggestions}
    size="lg"
/>
```

### Features
- ✅ Autocomplete suggestions dropdown
- ✅ Recent searches history
- ✅ Loading state with spinner
- ✅ Clear button
- ✅ Search icon
- ✅ Keyboard navigation (Enter to search)
- ✅ Focus/blur handling
- ✅ Size variants (sm, md, lg)
- ✅ Mobile responsive

---

## 5️⃣ Pagination Component

### Purpose
Page navigation with previous/next buttons, page numbers, and page size selector.

### Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `currentPage` | Number | `1` | Current page number |
| `totalPages` | Number | `1` | Total number of pages |
| `pageSize` | Number | `12` | Items per page |
| `pageSizeOptions` | Array | `[12, 24, 48]` | Page size options |
| `totalItems` | Number | `0` | Total number of items |
| `onPageChange` | Function | - | Callback when page changes |
| `onPageSizeChange` | Function | - | Callback when page size changes |
| `showPageSize` | Boolean | `true` | Show page size selector |
| `showFirstLast` | Boolean | `true` | Show first/last buttons |
| `maxVisible` | Number | `7` | Max visible page numbers |
| `variant` | String | `"default"` | Variant: "default", "compact" |

### Example

```flin
currentPage = 1
totalPages = 24
totalItems = 567
pageSize = 24

function handlePageChange(page) {
    currentPage = page
    print("Load page: " + page)
}

function handlePageSizeChange(size) {
    pageSize = size
    currentPage = 1
    totalPages = Math.ceil(totalItems / size)
}

<Pagination
    currentPage={currentPage}
    totalPages={totalPages}
    pageSize={pageSize}
    totalItems={totalItems}
    onPageChange={handlePageChange}
    onPageSizeChange={handlePageSizeChange}
/>
```

### Features
- ✅ Page number buttons with active state
- ✅ Previous/Next navigation
- ✅ First/Last page buttons
- ✅ Page size selector dropdown
- ✅ Item range display (1-24 of 567)
- ✅ Ellipsis for large page counts
- ✅ Keyboard navigation support
- ✅ Mobile responsive layout
- ✅ Disabled state handling

---

## 🎨 Design System Integration

All components use FLIN design tokens:

### Colors
```css
--flin-primary          /* Primary brand color */
--flin-text-primary     /* Primary text */
--flin-text-secondary   /* Secondary text */
--flin-text-muted       /* Muted text */
--flin-bg-surface       /* Surface background */
--flin-bg-hover         /* Hover state */
--flin-border-light     /* Light borders */
```

### Spacing
```css
--flin-space-1 to --flin-space-12  /* 4px to 48px */
```

### Typography
```css
--flin-text-xs to --flin-text-4xl  /* Font sizes */
--flin-font-medium                  /* Font weight */
--flin-font-bold                    /* Font weight */
```

---

## 🔧 Complete Store Example

```flin
// Complete navigation system for e-commerce store

categories = [/* ... */]
breadcrumbs = [/* ... */]
filters = [/* ... */]
selectedFilters = []
searchQuery = ""
currentPage = 1

<div class="store">
    <!-- Top Search Bar -->
    <SearchBar
        placeholder="Search products..."
        onSearch={handleSearch}
    />

    <!-- Breadcrumb Trail -->
    <Breadcrumbs items={breadcrumbs} />

    <div class="store-layout">
        <!-- Left Sidebar -->
        <aside class="sidebar">
            <CategoryMenu
                categories={categories}
                activeCategory={activeCategory}
            />

            <ProductFilters
                filters={filters}
                selectedFilters={selectedFilters}
            />
        </aside>

        <!-- Main Content -->
        <main class="main-content">
            <!-- Product Grid Here -->
            <ProductGrid products={products} />

            <!-- Bottom Pagination -->
            <Pagination
                currentPage={currentPage}
                totalPages={totalPages}
                totalItems={totalItems}
            />
        </main>
    </div>
</div>
```

---

## 📱 Responsive Behavior

### Mobile (<640px)
- Search bar scales down
- Breadcrumbs collapse to essential items
- Category menu becomes full width
- Filters become modal/drawer
- Pagination becomes vertical layout

### Tablet (640px-1024px)
- Side-by-side layout maintained
- Filters slightly narrower
- Page numbers visible

### Desktop (>1024px)
- Full navigation experience
- Sticky filters (optional)
- All features visible

---

## ♿ Accessibility Features

- ✅ ARIA labels on all interactive elements
- ✅ Keyboard navigation support
- ✅ Focus indicators
- ✅ Screen reader friendly
- ✅ Semantic HTML structure
- ✅ Color contrast compliance
- ✅ Disabled state handling

---

## 🚀 Performance

- **Zero imports** - Components discovered automatically
- **Lightweight** - ~500 lines total
- **Design tokens** - Consistent theming
- **Scoped styles** - No CSS conflicts
- **Lazy rendering** - Only visible items
- **Efficient updates** - Minimal re-renders

---

## 📝 Demo

Run the complete demo:

```bash
flin dev examples/store-navigation-demo.flin
```

Features demonstrated:
- All 5 components working together
- Real-time state management
- Interactive filtering
- Search with autocomplete
- Category navigation
- Pagination controls

---

## 🎯 Best Practices

### 1. Category Menu
```flin
// ✅ Good: Clear hierarchy
categories = [
    ["id": "electronics", "label": "Electronics", "subcategories": [...]]
]

// ❌ Bad: Deep nesting (>2 levels)
// Keep it simple - max 2 levels
```

### 2. Breadcrumbs
```flin
// ✅ Good: Meaningful labels
["label": "Gaming Laptops", "url": "/electronics/laptops/gaming"]

// ❌ Bad: Technical IDs
["label": "cat-123", "url": "/c/123"]
```

### 3. Filters
```flin
// ✅ Good: Show counts
["id": "apple", "label": "Apple", "count": 89]

// ❌ Bad: No feedback
["id": "apple", "label": "Apple"]
```

### 4. Search
```flin
// ✅ Good: Relevant suggestions
suggestions = [
    ["text": "wireless mouse", "category": "Accessories"]
]

// ❌ Bad: Generic results
suggestions = ["mouse", "mice", "mouses"]
```

### 5. Pagination
```flin
// ✅ Good: Show total items
totalItems = 567  // User knows total results

// ❌ Bad: Unknown total
// User doesn't know how many results exist
```

---

## 🐘 É flîn nù - It Remembers Things

These navigation components are part of the FLIN language ecosystem - where simplicity meets power.

**Built with**: Zero imports, Design tokens, Pure FLIN
**Created by**: ZeroSuite, Inc.
**License**: MIT
**Website**: https://welcome.flin.dev

---

**Last Updated**: January 8, 2026
**Version**: 1.0.0
**Status**: Production Ready ✅
