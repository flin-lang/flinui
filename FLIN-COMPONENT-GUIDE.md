# FLIN Component System Explained

**Date**: January 8, 2026
**Status**: Architecture Documentation

---

## 🎯 Core Philosophy

> **"If you know HTML, you know FLIN."**

**FLIN eliminates `import` statements entirely.**

Components work like HTML tags — just use them!

```flin
// ❌ WRONG (JavaScript thinking)
import { Button } from "./Button.flin"
<Button label="Click" />

// ✅ CORRECT (FLIN way)
<Button label="Click" />
```

**That's it.** FLIN finds `Button.flin` automatically.

---

## 🏗️ How It Works (Architecture)

### 1. **Component Detection** (Parser)

When parsing `<Button />`:

```rust
// src/parser/ast.rs
pub struct ViewElement {
    pub name: String,           // "Button"
    pub is_component: bool,     // true (PascalCase detected)
    // ...
}
```

**Rule**: Any tag starting with uppercase = component
- `<button>` → HTML element
- `<Button>` → FLIN component
- `<AIChatbot>` → FLIN component

### 2. **Component Registry** (Discovery)

```rust
// src/components/registry.rs
pub struct ComponentRegistry {
    components: HashMap<String, CompiledComponent>,
    search_paths: Vec<PathBuf>,
}
```

**What it does:**
1. Maintains a cache of compiled components
2. Searches configured paths for `.flin` files
3. Hot-reloads when files change

**Search algorithm:**
```rust
// For <Button />, searches:
search_paths = [
    "./",
    "./components/",
    "./icons/",
    "./flinui/basic/",
    "./flinui/pro/ai/",
    // ... all configured paths
]

filenames = [
    "Button.flin",      // Exact match
    "button.flin",      // Lowercase
]

// Returns first match found
```

### 3. **Component Rendering** (Runtime)

```rust
// src/vm/renderer.rs
pub fn render_element_with_context(element, vm, ctx) {
    if element.is_component {
        // 1. Look up component in registry
        let component = ctx.registry.find_component(&element.name)?;

        // 2. Extract props from attributes
        let props = extract_props(element.attributes);

        // 3. Render component with props
        return render_component(component, props, vm);
    }

    // Regular HTML element
    render_html_element(element)
}
```

### 4. **Component Context** (Props Access)

Inside `Button.flin`:

```flin
// Automatically available:
props.label       // From <Button label="Click" />
props.onClick     // From <Button onClick={handler} />
props.variant     // From <Button variant="primary" />

// Use them:
<button click={props.onClick} class="btn-{props.variant}">
    {props.label}
</button>
```

**No import, no export, no boilerplate.**

---

## 📂 Directory Structure

### Example Project

```
myapp/
├── app.flin                 # Main app
├── components/              # Custom components
│   ├── Button.flin
│   ├── Card.flin
│   └── Header.flin
└── flinui/                  # FlinUI library
    ├── basic/
    │   ├── Button.flin
    │   ├── Avatar.flin
    │   └── Alert.flin
    └── pro/
        └── ai/
            ├── AIChatbot.flin
            ├── ChatInput.flin
            └── ChatMessages.flin
```

### Configuration (Auto)

```bash
# When you run:
flin dev myapp/app.flin

# FLIN automatically configures search paths:
search_paths = [
    "myapp/",                    # App directory
    "myapp/components/",         # Components subdirectory
    "flinui/",                   # FlinUI root
    "flinui/basic/",             # FlinUI categories
    "flinui/pro/ai/",
    # ... all discovered directories
]
```

**Result**: All components are available everywhere!

---

## 🎨 FlinUI Usage Examples

### Using Basic Components

```flin
// app.flin
name = ""
showAlert = false

<div>
    <!-- No imports! Just use them: -->
    <Input value={name} placeholder="Your name" />

    <Button
        label="Submit"
        variant="primary"
        click={showAlert = true}
    />

    {if showAlert}
        <Alert type="success" message="Hello {name}!" />
    {/if}
</div>
```

**FLIN automatically finds:**
- `flinui/forms/Input.flin`
- `flinui/basic/Button.flin`
- `flinui/feedback/Alert.flin`

### Using PRO Components

```flin
// chat.flin
messages = []
model = "claude-sonnet-4-5"

fn handleSend(text) {
    messages.push(["role": "user", "content": text])
}

<div>
    <!-- Zero imports needed! -->
    <AIChatbot
        title="FLIN Assistant"
        model={model}
        showReasoningPanel={true}
    />

    <ChatMessages
        messages={messages}
        showAvatars={true}
    />

    <ChatInput onSend={handleSend} />
</div>
```

**FLIN automatically finds:**
- `flinui/pro/ai/AIChatbot.flin`
- `flinui/pro/ai/ChatMessages.flin`
- `flinui/pro/ai/ChatInput.flin`

---

## 🚀 Why This Is Revolutionary

### Comparison

| Framework | Component Usage | Lines of Boilerplate |
|-----------|----------------|----------------------|
| **React** | `import { Button } from './Button'`<br>`export default App` | 2+ per file |
| **Vue** | `import Button from './Button.vue'`<br>`export default { components: { Button } }` | 3+ per file |
| **Svelte** | `import Button from './Button.svelte'` | 1+ per file |
| **FLIN** | `<Button />` | **0** ✨ |

### Benefits

1. **Zero Boilerplate**
   No imports, no exports, no module system to learn

2. **HTML-Like Simplicity**
   If you know HTML, you know FLIN components

3. **No Build Step Required**
   Components are discovered at runtime

4. **Instant Hot Reload**
   Change component → refresh → updated (no rebuild)

5. **No Dependency Hell**
   No `node_modules`, no version conflicts

6. **Auto-Discovery**
   Add `Button.flin` → immediately available everywhere

---

## 🔧 Implementation Status

### ✅ Currently Implemented

- [x] Component detection (PascalCase check)
- [x] ComponentRegistry with caching
- [x] Auto-discovery from search paths
- [x] Props extraction and validation
- [x] Component rendering with context
- [x] Hot reload support (file change detection)
- [x] Nested component support
- [x] Scoped styles in components

### 📋 Planned Enhancements

- [ ] **Search path configuration** (if needed - auto-discovery works well)
  ```flin
  // Could be configured via CLI flags:
  // flin dev app.flin --components ./components --components ../flinui
  ```

- [ ] **Component slots** (like Vue/Svelte)
  ```flin
  // Card.flin
  <div class="card">
      <slot />  <!-- Children go here -->
  </div>

  // Usage:
  <Card>
      <h1>Title</h1>
      <p>Content</p>
  </Card>
  ```

- [ ] **Named slots**
  ```flin
  // Layout.flin
  <div>
      <header><slot name="header" /></header>
      <main><slot /></main>
      <footer><slot name="footer" /></footer>
  </div>
  ```

- [ ] **Default slot content**
  ```flin
  <slot>Default content if no children</slot>
  ```

- [ ] **Component lifecycle hooks**
  ```flin
  // Already supported! No arrow functions needed
  onMount {
      print("Component mounted!")
  }

  onUnmount {
      print("Component destroyed!")
  }
  ```

- [ ] **Async components**
  ```flin
  <AsyncComponent loading={<Spinner />}>
      <!-- Loaded content -->
  </AsyncComponent>
  ```

---

## 💡 Advanced Patterns

### Component Composition

```flin
// Card.flin
<div class="card">
    <div class="card-header">
        {props.title}
    </div>
    <div class="card-body">
        {props.children}  <!-- Children passed from parent -->
    </div>
</div>

// App.flin
<Card title="My Card">
    <!-- Children content: -->
    <p>This is the content</p>
    <Button label="Action" />
</Card>
```

**Note**: Children support already works! Slots feature will add named slots and defaults.

### Conditional Components

```flin
view = "list"  // or "grid"

{if view == "list"}
    <ListView items={items} />
{else}
    <GridView items={items} />
{/if}
```

### Dynamic Components

```flin
componentName = "Button"  // Could be from user input

<!-- NOT YET SUPPORTED, but planned: -->
<{componentName} label="Dynamic" />
```

---

## 🎓 For Developers Coming From...

### From React

```jsx
// ❌ React way
import React, { useState } from 'react';
import Button from './components/Button';

export default function Counter() {
    const [count, setCount] = useState(0);
    return <Button onClick={() => setCount(count + 1)}>{count}</Button>;
}
```

```flin
// ✅ FLIN way
count = 0
<Button click={count++}>{count}</Button>
```

### From Vue

```vue
<!-- ❌ Vue way -->
<script setup>
import { ref } from 'vue'
import Button from './components/Button.vue'

const count = ref(0)
</script>

<template>
  <Button @click="count++">{{ count }}</Button>
</template>
```

```flin
// ✅ FLIN way
count = 0
<Button click={count++}>{count}</Button>
```

### From Svelte

```svelte
<!-- ❌ Svelte way -->
<script>
import Button from './Button.svelte';
let count = 0;
</script>

<Button on:click={() => count++}>{count}</Button>
```

```flin
// ✅ FLIN way
count = 0
<Button click={count++}>{count}</Button>
```

**Notice the pattern? FLIN is always simpler.**

---

## 🐘 The FLIN Motto

> **"Write apps like 1995. With the power of 2025."**

Components in FLIN work like `<img>` and `<button>` in HTML.
You don't import HTML tags. You just use them.

Same with FLIN components.

---

## 📚 See Also

- `_private/docs/02-FLIN-LANGUAGE-SPEC.md` — Section 8.9 (Components)
- `_private/docs/16-FLIN-UI-LIBRARY-SPEC.md` — FlinUI architecture
- `src/components/registry.rs` — Component registry implementation
- `src/vm/renderer.rs` — Component rendering logic

---

**Last Updated**: January 8, 2026
**Author**: Claude (AI CTO, ZeroSuite Inc.)
