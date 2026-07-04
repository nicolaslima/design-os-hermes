---
name: design-os
description: "Design OS — Product planning and design tool adapted for Hermes Agent. Guides you through a structured discovery process: product vision, data shape, design system, section design, and export. The missing step between your idea and your codebase."
version: 1.0.0
author: Hermes adaptation by Nicolas Lima
license: MIT (original by Brian Casel / Builder Methods)
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [design, product, wireframe, discovery, react, tailwind]
    source: https://github.com/buildermethods/design-os
---

# Design OS for Hermes Agent

Design OS is the missing step between your product idea and your codebase. It's a product planning and design tool that helps you define your product vision, sketch out your data shape, design your UI, and export production-ready components for implementation — **before any code is written**.

## The Problem This Solves

AI coding tools build fast. But results often miss the mark. You describe what you want, the agent builds *something*, but it's not what you envisioned. The UI looks generic. Features get half-implemented.

**The core issue:** we're asking coding agents to figure out what to build *and* build it simultaneously. Design OS separates these concerns — you plan first, then build.

## The Design OS Process

Design OS follows a structured sequence. Each step builds on the previous one.

### Phase 1: Product Planning

1. **Product Vision** — Define your product, break it into sections, and sketch the data shape — all in one flow
2. **Design Tokens** — Choose your color palette and typography
3. **Application Shell** — Design navigation and layout

### Phase 2: Section Design (repeat for each section)

1. **Shape the Section** — Define scope, requirements, and generate sample data + types
2. **Design the Screen** — Build the actual React components
3. **Capture Screenshots** — Document the design (optional)

### Phase 3: Export

1. **Export** — Generate the complete handoff package for implementation

## How to Use

### Starting Fresh

1. **Start the dev server** in the Design OS project directory:
   ```bash
   cd ~/Projects/design-os-hermes
   npm run dev
   ```
   Open http://localhost:5173 in your browser.

2. **Load the umbrella skill** in your Hermes session:
   ```
   /skill design-os
   ```

3. **Follow the guided flow** — each step is a conversation. The AI asks questions, you provide direction, and together you shape a product that matches your vision — before any implementation begins.

### Step-by-Step Skill Invocation

| Step | Skill to load | Purpose |
|------|---------------|---------|
| 1 | `/skill design-os-product-vision` | Define product overview, roadmap sections, and data shape |
| 2 | `/skill design-os-design-tokens` | Choose colors and typography |
| 3 | `/skill design-os-design-shell` | Design navigation and layout |
| 4 | `/skill design-os-shape-section` | Define a section's scope, requirements, sample data + types |
| 5 | `/skill design-os-design-screen` | Create screen design components |
| 6 | `/skill design-os-screenshot-design` | Capture screenshots |
| 7 | `/skill design-os-export-product` | Generate the complete handoff package |

**Auxiliary (update existing files):**
| Skill | Purpose |
|-------|---------|
| `/skill design-os-product-roadmap` | Update product sections (after initial creation) |
| `/skill design-os-data-shape` | Update data entities (after initial creation) |
| `/skill design-os-sample-data` | Update sample data and types (after initial creation) |

## Key Principles

- **Follow the sequence** — Each step builds on the previous. Don't skip ahead.
- **Be specific** — The more detail you provide, the better the output.
- **Iterate** — Each skill is a conversation. Refine until you're happy.
- **Restart the dev server** — After creating new components, restart to see changes.
- **Auto-proceed without approval** — After gathering enough info, skills write files immediately. You review *after*, not before.
- **Files as source of truth** — Everything is markdown/JSON in `product/`. The React app parses these files at build time.

## File Structure

```
product/                           # Product definition (portable)
├── product-overview.md            # Product description, problems/solutions, features
├── product-roadmap.md             # List of sections with titles and descriptions
│
├── data-shape/                    # Product data shape
│   └── data-shape.md              # Entity names, descriptions, and relationships
│
├── design-system/                 # Design tokens
│   ├── colors.json                # { primary, secondary, neutral }
│   └── typography.json            # { heading, body, mono }
│
├── shell/                         # Application shell
│   └── spec.md                    # Shell specification
│
└── sections/
    └── [section-name]/
        ├── spec.md                # Section specification
        ├── data.json              # Sample data for screen designs
        ├── types.ts               # TypeScript interfaces
        └── *.png                  # Screenshots

src/
├── shell/                         # Shell design components
│   ├── components/
│   │   ├── AppShell.tsx
│   │   ├── MainNav.tsx
│   │   ├── UserMenu.tsx
│   │   └── index.ts
│   └── ShellPreview.tsx
│
└── sections/
    └── [section-name]/
        ├── components/            # Exportable components
        │   ├── [Component].tsx
        │   └── index.ts
        └── [ViewName].tsx         # Preview wrapper

product-plan/                      # Export package (generated)
├── README.md                      # Quick start guide
├── product-overview.md            # Product summary
├── prompts/                       # Ready-to-use prompts for coding agents
├── instructions/                  # Implementation instructions
├── design-system/                 # Tokens, colors, fonts
├── data-shapes/                   # UI data contracts
├── shell/                         # Shell components
└── sections/                      # Section components (with tests.md each)
```

## Design Requirements (applies to all screen designs)

- **Tailwind CSS v4** (not v3) — no `tailwind.config.js`
- **Mobile responsive** — Use Tailwind's responsive prefixes (`sm:`, `md:`, `lg:`, `xl:`)
- **Light & dark mode** — Use `dark:` variants for all colors
- **Design tokens** — Apply the product's color palette and typography when available
- **Props-based components** — All screen design components must accept data and callbacks via props. Never import data directly in exportable components.
- **No navigation in section screen designs** — The shell handles all navigation.
- **Use built-in Tailwind colors** — Avoid defining custom colors. Use Tailwind's built-in color utility classes.

## Frontend Design Skill

When designing screens, always load the `design-os-frontend-design` skill for high-quality, distinctive design output. It prevents generic "AI slop" aesthetics and ensures creative, polished interfaces.

## Compatibility

- **Works with any AI coding agent** for implementation: Claude Code, Cursor, Copilot, Codex, or anything that can implement from a handoff
- **Your frontend needs** React and Tailwind CSS
- **Your backend can be anything** — Rails, Laravel, Next.js, Python, Go, whatever

## Attribution

Originally created by [Brian Casel](https://buildermethods.com) at [Builder Methods](https://buildermethods.com). This is an adaptation for Hermes Agent, preserving the same process, file formats, and design principles while replacing Claude Code slash commands with Hermes skills.