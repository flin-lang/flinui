# FlinUI

**The Component Library for FLIN** - 94 production-ready components with zero dependencies.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Components](https://img.shields.io/badge/Components-94-green.svg)]()
[![Dependencies](https://img.shields.io/badge/Dependencies-0-brightgreen.svg)]()

## Overview

FlinUI is the official component library for the [FLIN programming language](https://github.com/flin-lang/flin). It provides everything you need to build modern, beautiful web applications - without the npm complexity.

**Live Demo:** [flinui.flin.dev](https://flinui.flin.dev)

## 🚨 CRITICAL: Zero-Import Philosophy

**FLIN HAS NO IMPORTS!** Components work like HTML tags - just use them!

```flin
// ❌ WRONG (JavaScript/React thinking)
import { Button, Card, Modal } from "flinui"

// ✅ CORRECT (FLIN way)
<Button label="Click me" />
<Card title="Welcome" />
<Modal open={true} />
```

**Why?** FLIN auto-discovers components from the `flinui/` directory. No configuration needed!

**📖 Full Guide:** Read [`FLIN-COMPONENT-GUIDE.md`](./FLIN-COMPONENT-GUIDE.md) for complete instructions and common mistakes to avoid.

## Features

- **94 Components** - From basic inputs to advanced data tables
- **Zero Dependencies** - No npm, no node_modules, no bundlers
- **Zero Imports** - Components auto-discovered (like HTML tags!)
- **Native Charts** - SVG-based charts without Chart.js
- **Dark Mode** - Built-in theme system with light/dark support
- **Accessible** - ARIA attributes and keyboard navigation
- **FLIN-Native** - Unique components only possible in FLIN

## Quick Start

Components are auto-discovered when you use them:

```flin
// No imports! Just use components directly:
<Button label="Click me" variant="primary" />

<Card>
    <CardHeader title="Welcome" />
    <CardBody>Your content here</CardBody>
</Card>

<Modal open={showModal} title="Confirm">
    <ModalBody>Are you sure?</ModalBody>
    <ModalFooter>
        <Button label="Cancel" variant="secondary" />
        <Button label="Confirm" variant="primary" />
    </ModalFooter>
</Modal>
```

**That's it!** No `import`, no `export`, no configuration. FLIN finds the components automatically.

## Component Categories

| Category | Count | Description |
|----------|-------|-------------|
| **Basic** | 15 | Button, Input, Select, Avatar, Badge, etc. |
| **Layout** | 11 | Container, Stack, Grid, Flex, Box, etc. |
| **Data Display** | 17 | Card, Table, DataTable, Calendar, etc. |
| **Forms** | 10 | Form, DatePicker, ColorPicker, etc. |
| **Feedback** | 11 | Alert, Toast, Modal, Drawer, etc. |
| **Navigation** | 14 | Navbar, Sidebar, Tabs, Pagination, etc. |
| **Charts** | 7 | BarChart, LineChart, PieChart, etc. |
| **FLIN-Native** | 2 | TimeTravel, MemoryInspector |

## FLIN-Native Components

These components are **only possible in FLIN** - they leverage FLIN's unique memory-native architecture:

### TimeTravel
Navigate through any variable's complete history:
```flin
counter = 0
counter = counter + 1  // History: [0, 1]
counter = counter + 1  // History: [0, 1, 2]

<TimeTravel variable={counter} showPlayback={true} />
```

### MemoryInspector
Visual debugger for FlinDB - see all persistent data at once:
```flin
<MemoryInspector database={flindb} showStats={true} />
```

**Why these can't exist in React/Vue/Angular:**
- React has no built-in value history (need Redux DevTools)
- Vue has no automatic persistence (need Vuex + plugins)
- Angular has no time travel (need NgRx + store devtools)
- **FLIN has ALL of this built into the language itself!**

## Comparison

| Feature | FlinUI | Chakra UI | shadcn/ui | MUI |
|---------|--------|-----------|-----------|-----|
| Components | **94** | ~50 | ~40 | ~50 |
| Native Charts | **Yes** | No | No | Paid addon |
| Time Travel | **Yes** | No | No | No |
| Memory Inspector | **Yes** | No | No | No |
| Zero Dependencies | **Yes** | No | No | No |
| Dark Mode | Yes | Yes | Yes | Yes |

## Theme System

FlinUI uses CSS variables for theming:

```flin
// Include theme tokens
@import "components/theme/tokens.flin"

// Use dark mode
<div data-theme="dark">
    <Button label="Dark mode!" />
</div>
```

## Directory Structure

```
flinui/
├── components/
│   ├── basic/         # 15 components
│   ├── layout/        # 11 components
│   ├── data/          # 17 components
│   ├── forms/         # 10 components
│   ├── feedback/      # 11 components
│   ├── navigation/    # 14 components
│   ├── charts/        # 7 components (Native SVG)
│   ├── flin-native/   # 2 components (Unique!)
│   └── theme/         # Theme utilities
├── site/              # Documentation site
├── examples/          # Example templates
└── public/            # Logos and icons
```

## Examples

### Dashboard
```flin
<Container>
    <Navbar>
        <NavbarBrand><img src="logo.png" /></NavbarBrand>
        <NavbarMenu>
            <NavbarItem active>Dashboard</NavbarItem>
            <NavbarItem>Analytics</NavbarItem>
        </NavbarMenu>
    </Navbar>

    <Grid columns={3} gap="lg">
        <Stat label="Users" value="12,345" change="+12%" />
        <Stat label="Revenue" value="$54,321" change="+8%" />
        <Stat label="Orders" value="1,234" change="+23%" />
    </Grid>

    <Card>
        <CardHeader title="Revenue Over Time" />
        <CardBody>
            <LineChart data={revenueData} />
        </CardBody>
    </Card>
</Container>
```

## Development

FlinUI is part of the FLIN language project. To contribute:

1. Clone the main FLIN repo: `git clone https://github.com/flin-lang/flin`
2. Components are in `flinui/` directory
3. Run examples: `flin dev examples/flinui-demo.flin`

## License

MIT License - see [LICENSE](LICENSE) for details.

## Links

- **FLIN Language:** [github.com/flin-lang/flin](https://github.com/flin-lang/flin)
- **Documentation:** [flinui.flin.dev](https://flinui.flin.dev)
- **Discord:** [discord.gg/7uxR6VfA](https://discord.gg/7uxR6VfA)
- **Twitter:** [@flinlang](https://x.com/flinlang)

<div align="center">

### **É flin nù — It Remembers Things**
<em>The memory-native language where nothing is forgotten.</em>

**One file · Zero config · Full stack**

> “Write apps like it’s 1995 — with the power of 2025.”

🐘 **Code that remembers.**  
One file. Full stack. Complete history.

---

**Proof**  
`1,847 dependencies → 0` · `15 config files → 1` · `2 hours → 2 minutes`

---

<a href="https://flin.dev">
  <img src="https://welcome.flin.dev/logo-flin-512.png" alt="FLIN logo" width="120" />
</a>

Created by **Juste A. Gnimavo**  
Built at **[ZeroSuite, Inc.](https://www.zerosuite.dev)**

---

**Community & Socials**

[X / Twitter](https://x.com/flinlang) ·
[Bluesky](https://bsky.app/profile/flinlang.bsky.social) ·
[Facebook](https://fb.me/FlinLang) ·
[Discord](https://discord.gg/7uxR6VfA) ·
[GitHub](https://github.com/flin-lang/flin) ·
[YouTube](https://www.youtube.com/@FlinLang)

---

<sub>Made with care in Abidjan × San Francisco</sub>

</div>

---

Built with FLIN by [ZeroSuite, Inc.](https://zerosuite.io)
