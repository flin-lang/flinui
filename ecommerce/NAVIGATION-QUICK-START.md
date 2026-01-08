# 🚀 Store Navigation - Quick Start Guide

**Get started in 5 minutes** with FlinUI PRO Store Navigation components.

---

## 📦 What You Get

5 production-ready components (NO IMPORTS NEEDED):

1. **SearchBar** - Search with autocomplete
2. **Breadcrumbs** - Navigation trail
3. **CategoryMenu** - Category navigation
4. **ProductFilters** - Filter sidebar
5. **Pagination** - Page navigation

---

## ⚡ Instant Usage

```flin
// Just use them! No imports needed.

<SearchBar
    placeholder="Search products..."
    onSearch={fn(query) { print("Searching: " + query) }}
/>

<Breadcrumbs
    items={[
        ["label": "Electronics", "url": "/electronics"],
        ["label": "Laptops", "url": "/laptops"]
    ]}
/>

<CategoryMenu
    categories={[
        ["id": "electronics", "label": "Electronics", "icon": "💻"]
    ]}
/>

<ProductFilters
    filters={[
        [
            "id": "price",
            "label": "Price",
            "options": [
                ["id": "under-100", "label": "Under $100"]
            ]
        ]
    ]}
/>

<Pagination
    currentPage={1}
    totalPages={10}
    totalItems={240}
/>
```

---

## 🎯 Complete Store Template

```flin
// Complete navigation system - Copy & Paste!

// State
searchQuery = ""
categories = [
    ["id": "electronics", "label": "Electronics", "icon": "💻", "count": 245]
]
breadcrumbs = [
    ["label": "Electronics", "url": "/electronics"]
]
filters = [
    [
        "id": "brand",
        "label": "Brand",
        "options": [
            ["id": "apple", "label": "Apple", "count": 89]
        ]
    ]
]
selectedFilters = []
currentPage = 1
totalPages = 10
totalItems = 240

// Handlers
function handleSearch(query) {
    searchQuery = query
    print("Search: " + query)
}

function handleFilter(filterId) {
    if selectedFilters.includes(filterId) {
        selectedFilters = selectedFilters.filter(fn(id) { id != filterId })
    } else {
        selectedFilters = [...selectedFilters, filterId]
    }
}

function handlePage(page) {
    currentPage = page
}

// Layout
<div class="store">
    <!-- Header -->
    <SearchBar
        placeholder="Search..."
        onSearch={handleSearch}
    />

    <!-- Breadcrumbs -->
    <Breadcrumbs items={breadcrumbs} />

    <div style="display: grid; grid-template-columns: 280px 1fr; gap: 24px;">
        <!-- Sidebar -->
        <aside>
            <CategoryMenu categories={categories} />
            <ProductFilters
                filters={filters}
                selectedFilters={selectedFilters}
                onFilterChange={handleFilter}
            />
        </aside>

        <!-- Main Content -->
        <main>
            <!-- Your products here -->
            <div>Products grid...</div>

            <!-- Pagination -->
            <Pagination
                currentPage={currentPage}
                totalPages={totalPages}
                totalItems={totalItems}
                onPageChange={handlePage}
            />
        </main>
    </div>
</div>
```

---

## 🎨 Common Customizations

### SearchBar Sizes
```flin
<SearchBar size="sm" />  <!-- Small -->
<SearchBar size="md" />  <!-- Medium (default) -->
<SearchBar size="lg" />  <!-- Large -->
```

### Breadcrumb Separators
```flin
<Breadcrumbs separator="/" />  <!-- Slash -->
<Breadcrumbs separator="›" />  <!-- Arrow -->
<Breadcrumbs separator=">" />  <!-- Greater than -->
```

### Category Menu Variants
```flin
<CategoryMenu variant="sidebar" />     <!-- Vertical (default) -->
<CategoryMenu variant="horizontal" />  <!-- Horizontal -->
```

### Filter Types
```flin
filters = [
    [
        "type": "checkbox",  // Regular checkboxes
        "options": [...]
    ],
    [
        "type": "color",     // Color swatches
        "options": [
            ["color": "#000000", "label": "Black"]
        ]
    ]
]
```

### Pagination Variants
```flin
<Pagination variant="default" />  <!-- Full version -->
<Pagination variant="compact" />  <!-- Compact version -->
```

---

## 📊 Data Structures

### Categories
```flin
[
    "id": "unique-id",
    "label": "Display Name",
    "icon": "📱",           // Optional emoji
    "count": 123,           // Optional count
    "subcategories": [...]  // Optional nested
]
```

### Breadcrumbs
```flin
[
    "label": "Category Name",
    "url": "/category/path",
    "icon": "📱"  // Optional
]
```

### Filters
```flin
[
    "id": "filter-group-id",
    "label": "Filter Name",
    "type": "checkbox",     // or "color"
    "options": [
        [
            "id": "option-id",
            "label": "Option Name",
            "color": "#000000",  // For color type
            "count": 42          // Optional
        ]
    ]
]
```

### Search Suggestions
```flin
[
    "text": "Search term",
    "category": "Category name"  // Optional
]
```

---

## 🎬 Run the Demo

```bash
flin dev examples/store-navigation-demo.flin
```

See all 5 components working together with:
- ✅ Real-time search
- ✅ Category navigation
- ✅ Interactive filters
- ✅ Breadcrumb trail
- ✅ Working pagination
- ✅ Responsive layout

---

## 📱 Mobile Responsive

All components automatically adapt:
- **Mobile (<640px)**: Stacked layout, full width
- **Tablet (640-1024px)**: Side-by-side with narrow sidebar
- **Desktop (>1024px)**: Full layout with wide sidebar

No media queries needed in your code!

---

## ♿ Accessibility Built-in

- ✅ ARIA labels on all controls
- ✅ Keyboard navigation (Tab, Enter, Space)
- ✅ Focus indicators
- ✅ Screen reader support
- ✅ Semantic HTML

---

## 🔧 Props Quick Reference

### SearchBar
```flin
placeholder, value, onSearch, onInput, suggestions,
recentSearches, loading, disabled, size, variant
```

### Breadcrumbs
```flin
items, separator, maxItems, onItemClick,
showHomeIcon, homeLabel, homeUrl
```

### CategoryMenu
```flin
categories, activeCategory, onCategoryClick,
variant, showIcons, collapsible, expandedCategories
```

### ProductFilters
```flin
filters, selectedFilters, onFilterChange,
onClearAll, showClearAll, collapsible
```

### Pagination
```flin
currentPage, totalPages, pageSize, pageSizeOptions,
totalItems, onPageChange, onPageSizeChange,
showPageSize, showFirstLast, maxVisible, variant
```

---

## 💡 Tips & Tricks

### 1. Combine with State Management
```flin
// Use reactive state for seamless updates
searchQuery = ""
<SearchBar value={searchQuery} onInput={fn(v) { searchQuery = v }} />
```

### 2. Sync URL with State
```flin
// Update URL when filters change
function handleFilter(filterId) {
    // Update state
    selectedFilters = [...selectedFilters, filterId]
    // Update URL
    window.location.hash = "filters=" + selectedFilters.join(",")
}
```

### 3. Persist Recent Searches
```flin
// Save to localStorage
recentSearches = JSON.parse(localStorage.getItem("searches") || "[]")

function handleSearch(query) {
    recentSearches = [query, ...recentSearches].slice(0, 5)
    localStorage.setItem("searches", JSON.stringify(recentSearches))
}
```

### 4. Dynamic Filter Counts
```flin
// Update counts based on current selection
function updateFilterCounts() {
    // Recalculate available items per filter
    // Update filter.options[].count
}
```

### 5. Keyboard Shortcuts
```flin
// Add "/" key to focus search
onMount {
    window.addEventListener("keydown", fn(e) {
        if e.key == "/" {
            document.querySelector(".search-input").focus()
            e.preventDefault()
        }
    })
}
```

---

## 🚨 Common Issues

### Component not found?
```flin
// ❌ Don't import
import { SearchBar } from "./SearchBar.flin"

// ✅ Just use it
<SearchBar />
```

### Props not working?
```flin
// ❌ Wrong syntax
<SearchBar onSearch=handleSearch />

// ✅ Correct syntax
<SearchBar onSearch={handleSearch} />
```

### State not updating?
```flin
// ❌ Direct mutation
selectedFilters.push(newId)

// ✅ Create new array
selectedFilters = [...selectedFilters, newId]
```

---

## 📚 More Resources

- **Full Docs**: `NAVIGATION-COMPONENTS.md` (complete API reference)
- **Overview**: `STORE-NAVIGATION-OVERVIEW.md` (detailed guide)
- **Demo**: `examples/store-navigation-demo.flin` (working example)
- **Website**: https://welcome.flin.dev

---

## ✨ That's It!

You now have everything needed for production-ready e-commerce navigation.

**Remember**: NO IMPORTS needed. Just use the components like HTML tags!

---

**Next Steps**:
1. Copy the template above
2. Customize with your data
3. Run `flin dev yourfile.flin`
4. Start building!

🐘 **É flîn nù** - It Remembers Things

---

**Created**: January 8, 2026
**License**: MIT
**Status**: ✅ Production Ready
