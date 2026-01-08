# 🚨 CRITICAL INSTRUCTIONS: FLIN Component System

**READ THIS FIRST** before writing ANY FLIN code or FlinUI components!

---

## ⚡ THE CORE RULE

```
╔═══════════════════════════════════════════════════════════════════════════╗
║                                                                           ║
║  FLIN HAS NO IMPORTS. COMPONENTS WORK LIKE HTML TAGS.                    ║
║                                                                           ║
║  Just use <Button /> — No import statements needed!                      ║
║                                                                           ║
╚═══════════════════════════════════════════════════════════════════════════╝
```

---

## ❌ COMMON MISTAKES (That AI/Claude Often Makes)

### 1. **NEVER Use Import Statements**

```flin
// ❌ WRONG — This does NOT exist in FLIN!
import { Button } from "./Button.flin"
import Button from "../components/Button.flin"
import { AIChatbot, ChatInput } from "../flinui/pro/ai/index.flin"

// ✅ CORRECT — Just use the component!
<Button label="Click me" />
<AIChatbot title="Assistant" />
<ChatInput placeholder="Type..." />
```

**Why?** FLIN eliminates `import` statements entirely. Components are auto-discovered.

---

### 2. **NEVER Use Export Statements**

```flin
// ❌ WRONG — This does NOT exist in FLIN!
export default function Button() { ... }
export { Button, Card, Alert }
export const MyComponent = ...

// ✅ CORRECT — The file IS the component!
// Button.flin:
<button class="btn">{props.label}</button>

// That's it! The file exports itself automatically.
```

**Why?** The `.flin` file itself is the component. No export keyword needed.

---

### 3. **NEVER Use Arrow Functions (Yet)**

```flin
// ❌ WRONG — Arrow functions not implemented!
onClick={(e) => { count++ }}
messages.map((msg) => msg.content)
items.filter((x) => x > 0)

// ✅ CORRECT — Use function declarations or inline expressions
fn handleClick(e) {
    count++
}

// Or for simple cases:
click={count++}

// For mapping/filtering, use for loops:
{for msg in messages}
    <div>{msg.content}</div>
{/for}
```

**Status**: Arrow functions are on the roadmap but NOT implemented yet.

---

### 4. **NEVER Use Svelte-Style Syntax**

```flin
// ❌ WRONG — Svelte directives don't work!
{#if condition}          // Use {if condition}
{#each items as item}    // Use {for item in items}
{@html content}          // Not implemented yet
bind:value={name}        // Use value={name}
on:click={handler}       // Use click={handler}
class:active={isActive}  // Pre-compute: class={if isActive then "active" else ""}

// ✅ CORRECT — FLIN syntax
{if condition}
    <div>Content</div>
{/if}

{for item in items}
    <li>{item}</li>
{/for}

<input value={name} />
<button click={handleClick}>Click</button>
```

---

### 5. **NEVER Use Optional Chaining (Yet)**

```flin
// ❌ WRONG — Optional chaining not implemented!
obj?.field
obj?.method?.()
arr?.[0]

// ✅ CORRECT — Use explicit checks
{if obj and obj.field}
    {obj.field}
{/if}

// Or use default values
field = if obj then obj.field else "default"
```

**Status**: Optional chaining (`?.`) is on the roadmap.

---

### 6. **NEVER Use Nullish Coalescing (Yet)**

```flin
// ❌ WRONG — Nullish coalescing not implemented!
value = input ?? default
title = props.title ?? "Untitled"

// ✅ CORRECT — Use OR operator
value = input or default
title = props.title or "Untitled"

// Note: 'or' returns the first truthy value
```

**Status**: Nullish coalescing (`??`) is on the roadmap.

---

### 7. **NEVER Use Destructuring (Yet)**

```flin
// ❌ WRONG — Destructuring not fully implemented!
[x, y] = point
["name": name, "age": age] = user
[first, ...rest] = list

// ✅ CORRECT — Access properties directly
x = point[0]
y = point[1]
name = user.name
age = user.age
```

**Status**: Basic array assignment works, but not object destructuring or rest patterns.

---

### 8. **NEVER Hardcode Colors/Values**

```flin
// ❌ WRONG — Use design tokens!
<button style="color: #3b82f6; padding: 16px;">

// ✅ CORRECT — Use CSS variables
<button style="color: var(--flin-primary); padding: var(--flin-space-4);">

// Or use classes with tokens:
<button class="btn">

<style>
.btn {
    color: var(--flin-primary);
    padding: var(--flin-space-4);
}
</style>
```

**Why?** All FlinUI components use design tokens for consistency and themability.

---

### 9. **NEVER Use Complex Type Annotations**

```flin
// ❌ WRONG — Complex types not implemented!
fn process(data: Array<Map<string, int>>) -> Promise<Result<T, E>>

// ✅ CORRECT — Use simple types
fn process(data: [any]) -> any

// FLIN has:
// - int, float, bool, text
// - [type] for lists
// - [key: value] for maps
// - Custom entity types
```

**Status**: Generic types, unions, and advanced types are on the roadmap.

---

### 10. **NEVER Use Module System Thinking**

```flin
// ❌ WRONG — No module system!
import * as Utils from "./utils"
const { helper1, helper2 } = require("./helpers")

// ✅ CORRECT — Everything is global or scoped
// Just define functions in your file:
fn helper1() { ... }
fn helper2() { ... }

// Or use components:
<UtilityComponent />
```

**Why?** FLIN has no module system. All code in a file is in the file's scope.

---

## ✅ WHAT WORKS RIGHT NOW

### Core Language Features

- ✅ Variables: `x = 10`
- ✅ Types: `name: text = "John"`
- ✅ Functions: `fn add(a, b) { return a + b }`
- ✅ If/else: `if condition { } else { }`
- ✅ For loops: `for item in items { }`
- ✅ While loops: `while condition { }`
- ✅ Match: `match value { 1 -> "one", _ -> "other" }`
- ✅ Entities: `entity User { name: text }`
- ✅ Operators: `+`, `-`, `*`, `/`, `%`, `**`, `==`, `!=`, `<`, `>`, `and`, `or`, `not`
- ✅ Lists: `[1, 2, 3]`
- ✅ Maps: `["key": value]`
- ✅ String interpolation: `` `Hello ${name}` ``
- ✅ Template literals: `` `Count: ${count}` ``

### View Features

- ✅ HTML-like syntax: `<div class="container">`
- ✅ Components: `<Button label="Click" />`
- ✅ Props access: `props.label`, `props.onClick`
- ✅ Event handlers: `click={handleClick}`, `click={count++}`
- ✅ Interpolation: `{variable}`, `{expression}`
- ✅ Conditionals: `{if}...{else}...{/if}`
- ✅ Loops: `{for item in items}...{/for}`
- ✅ Loops with index: `{for item, idx in items}`
- ✅ Scoped styles: `<style scoped>`
- ✅ CSS variables: `var(--flin-primary)`

### Entity/Database Features

- ✅ Entity declarations: `entity Todo { ... }`
- ✅ CRUD operations: `Todo.create()`, `Todo.all`, `Todo.find()`, `Todo.where()`
- ✅ Temporal queries: Time-travel, history, soft deletes
- ✅ Relationships: Foreign keys, cascading deletes
- ✅ Reactivity: Auto-update on entity changes

---

## 📂 How Component Discovery Works

### File Structure Example

```
myapp/
├── app.flin              # Your app
├── components/           # Your custom components
│   ├── Button.flin
│   └── Card.flin
└── flinui/               # FlinUI library
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

### Auto-Discovery Rules

When you write `<Button />`, FLIN searches in this order:

1. `./Button.flin` (current directory)
2. `./components/Button.flin` (components subdirectory)
3. `./flinui/basic/Button.flin` (FlinUI categories)
4. `./flinui/layout/Button.flin`
5. `./flinui/data/Button.flin`
6. ... (all configured search paths)

**First match wins!**

### Naming Rules

- Component files MUST use PascalCase: `Button.flin`, `AIChatbot.flin`
- Component tags MUST start with uppercase: `<Button>`, `<AIChatbot>`
- HTML elements are lowercase: `<button>`, `<div>`

---

## 🎨 FlinUI Component Usage

### Basic Example

```flin
// app.flin
name = ""
count = 0

<div>
    <!-- All components auto-discovered from flinui/ -->
    <Input value={name} placeholder="Your name" />

    <Button
        label="Increment"
        variant="primary"
        size="lg"
        click={count++}
    />

    {if count > 0}
        <Alert type="success" message="Count: {count}" />
    {/if}
</div>
```

### PRO Components Example

```flin
// chat.flin
messages = []

<div>
    <!-- Zero imports! Auto-discovered from flinui/pro/ai/ -->
    <AIChatbot
        title="FLIN Assistant"
        model="claude-sonnet-4-5"
        showReasoningPanel={true}
    />

    <ChatMessages
        messages={messages}
        showAvatars={true}
        showTimestamps={true}
    />

    <ChatInput
        placeholder="Ask about FLIN..."
        showFileUpload={true}
    />
</div>
```

---

## 🔧 Writing FlinUI Components

### Component Structure

```flin
// components/Card.flin

// 1. Extract props (with defaults)
title = props.title or "Untitled"
content = props.content or ""
variant = props.variant or "default"

// 2. Compute derived values
cardClass = "card card-" + variant

// 3. Render view
<div class={cardClass}>
    <div class="card-header">
        <h3>{title}</h3>
    </div>
    <div class="card-body">
        {content}
    </div>
</div>

// 4. Add scoped styles
<style>
.card {
    border: 1px solid var(--flin-border-subtle);
    border-radius: var(--flin-radius-lg);
    padding: var(--flin-space-4);
    background: var(--flin-bg-surface);
}

.card-header h3 {
    margin: 0;
    color: var(--flin-text-primary);
    font-size: var(--flin-text-lg);
}

.card-body {
    margin-top: var(--flin-space-3);
    color: var(--flin-text-secondary);
}

/* Variants */
.card-default {
    border-color: var(--flin-border-subtle);
}

.card-primary {
    border-color: var(--flin-primary);
    background: var(--flin-primary-light);
}

.card-danger {
    border-color: var(--flin-danger);
    background: var(--flin-danger-light);
}
</style>
```

### Component Props Best Practices

1. **Always provide defaults**:
   ```flin
   label = props.label or "Click"
   variant = props.variant or "primary"
   size = props.size or "md"
   ```

2. **Use design tokens**:
   ```flin
   color: var(--flin-primary)
   padding: var(--flin-space-4)
   font-size: var(--flin-text-base)
   ```

3. **Pre-compute classes**:
   ```flin
   // ❌ WRONG
   <div class={if variant == "primary" then "btn-primary" else "btn-default"}>

   // ✅ CORRECT
   btnClass = if variant == "primary" then "btn-primary" else "btn-default"
   <div class={btnClass}>
   ```

4. **Keep it simple**:
   - Avoid complex logic in views
   - Extract calculations to variables
   - Use clear, descriptive names

---

## 🚨 Error Messages You'll See (And How to Fix Them)

### 1. "Component not found: Button"

**Cause**: FLIN can't find `Button.flin` in search paths.

**Fix**:
- Check file exists: `flinui/basic/Button.flin`
- Check naming: Must be PascalCase
- Check location: Must be in a discovered directory

### 2. "Expected expression, found ','"

**Cause**: Using syntax that's not implemented (like arrow functions).

```flin
// ❌ WRONG
onChange={(value) => { currentValue = value }}

// ✅ CORRECT
fn handleChange(value) {
    currentValue = value
}
onChange={handleChange}
```

### 3. "Expected '{' after if condition"

**Cause**: Using Svelte syntax instead of FLIN syntax.

```flin
// ❌ WRONG
{#if condition}

// ✅ CORRECT
{if condition}
```

### 4. "Parse error at 'import'"

**Cause**: Using import statements.

```flin
// ❌ WRONG
import { Button } from "./Button.flin"

// ✅ CORRECT
// Delete the import line!
<Button label="Click" />
```

### 5. "Optional chaining not supported"

**Cause**: Using `?.` operator.

```flin
// ❌ WRONG
value = obj?.field

// ✅ CORRECT
value = if obj then obj.field else none
```

---

## 📚 Philosophy: Why FLIN Is Different

### The 1995 + 2025 Principle

**FLIN = "Write apps like 1995. With the power of 2025."**

```html
<!-- 1995: HTML -->
<button>Click me</button>
```

```flin
<!-- 2025: FLIN -->
<Button label="Click me" />
```

**Same simplicity. More power.**

### Zero Boilerplate

| Framework | Boilerplate per File |
|-----------|---------------------|
| React | `import React`, `import Button`, `export default` (3 lines) |
| Vue | `import`, `export default`, `components: {}` (4+ lines) |
| Svelte | `import Button` (1 line) |
| **FLIN** | **0 lines** ✨ |

### No Configuration

- ❌ No `package.json`
- ❌ No `node_modules/`
- ❌ No webpack/vite config
- ❌ No babel/typescript config
- ❌ No build step
- ✅ Just write `.flin` files and run!

---

## 🎓 Learning Resources

### For Developers Coming From...

#### React

```jsx
// React
import { useState } from 'react';
import Button from './Button';

export default function Counter() {
    const [count, setCount] = useState(0);
    return <Button onClick={() => setCount(count + 1)}>{count}</Button>;
}
```

```flin
// FLIN
count = 0
<Button click={count++}>{count}</Button>
```

#### Vue

```vue
<!-- Vue -->
<script setup>
import { ref } from 'vue'
import Button from './Button.vue'
const count = ref(0)
</script>
<template>
  <Button @click="count++">{{ count }}</Button>
</template>
```

```flin
// FLIN
count = 0
<Button click={count++}>{count}</Button>
```

#### Svelte

```svelte
<!-- Svelte -->
<script>
import Button from './Button.svelte';
let count = 0;
</script>
<Button on:click={() => count++}>{count}</Button>
```

```flin
// FLIN
count = 0
<Button click={count++}>{count}</Button>
```

**Notice the pattern? FLIN is always simpler.**

---

## 🔗 See Also

- **CLAUDE.md** — Main developer instructions
- **_private/FLIN-COMPONENT-SYSTEM-EXPLAINED.md** — Deep dive on architecture
- **_private/FLIN-SYNTAX-ROADMAP.md** — Complete feature roadmap (820 features)
- **_private/docs/02-FLIN-LANGUAGE-SPEC.md** — Language specification
- **README.md** — Project overview

---

## 🐘 The FLIN Motto

> **É flîn nù** — It Remembers Things (Fongbé, Benin 🇧🇯)

Components in FLIN work like `<img>` and `<button>` in HTML.
You don't import HTML tags. You just use them.

**Same with FLIN components.**

---

**Last Updated**: January 8, 2026
**Author**: Claude Opus 4.5 (AI CTO, ZeroSuite Inc.)
**For**: All developers and AI assistants working with FLIN/FlinUI
