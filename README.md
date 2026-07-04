<img width="1280" height="640" alt="Design OS" src="https://github.com/user-attachments/assets/a9c04258-7b9a-45b6-8475-3431cdf5dbe9" />

## The missing design process between your idea and your codebase — now for Hermes Agent.

[Design OS](https://buildermethods.com/design-os) is a product planning and design tool that helps you define your product vision, sketch out your data shape, design your UI, and export production-ready components for implementation. Rather than jumping straight into code, you work through a guided process that captures what you're building and why—then hands off everything your coding agent needs to build it right.

This is a **Hermes Agent adaptation** of the original Design OS by Brian Casel. It preserves the same process, file formats, and design principles while replacing Claude Code slash commands with Hermes skills.

## The Problem

AI coding tools are incredible at building fast. But the results often miss the mark. You describe what you want, the agent builds *something*, but it's not what you envisioned. The UI looks generic. Features get half-implemented. You spend as much time fixing and redirecting as you would have spent building.

**The core issue:** we're asking coding agents to figure out what to build *and* build it simultaneously. Design decisions get made on the fly, buried in code, impossible to adjust without starting over. There's no spec. No shared understanding. No source of truth for what "done" looks like.

## The Design OS Process

Design OS powers a guided design and architecture process. You + AI, working together through structured steps:

1. **Product Planning** — Define your vision, break down your roadmap, and model your data
2. **Design System** — Choose colors, typography, and design your application shell
3. **Section Design** — For each feature area: specify requirements, generate sample data, and design the screens
4. **Export** — Generate a complete handoff package for implementation

Each step is a conversation. The AI asks questions, you provide direction, and together you shape a product that matches your vision—before any implementation begins.

---

## Getting Started with Hermes Agent

### Prerequisites

- **[Hermes Agent](https://hermes-agent.nousresearch.com)** installed (`curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash`)
- **Node.js** (v18 or higher)
- **npm** (comes with Node.js)

### Clone and Setup

```bash
git clone https://github.com/buildermethods/design-os.git my-project-design
cd my-project-design
git remote remove origin
npm install
```

### Start the Dev Server

```bash
npm run dev
```

Open http://localhost:5173 in your browser.

### Start Designing with Hermes

In your Hermes session, load the umbrella skill:

```
/skill design-os
```

Follow the guided flow. Each step is a conversation — the AI asks questions, you provide direction, and together you shape your product.

### Quick Reference — Skills

| Step | Skill | Purpose |
|------|-------|---------|
| 1 | `/skill design-os-product-vision` | Define product overview, roadmap sections, and data shape |
| 2 | `/skill design-os-design-tokens` | Choose colors and typography |
| 3 | `/skill design-os-design-shell` | Design navigation and layout |
| 4 | `/skill design-os-shape-section` | Define a section's scope, requirements, sample data + types |
| 5 | `/skill design-os-design-screen` | Create screen design components |
| 6 | `/skill design-os-screenshot-design` | Capture screenshots |
| 7 | `/skill design-os-export-product` | Generate the complete handoff package |

**Auxiliary:**
| Skill | Purpose |
|-------|---------|
| `/skill design-os-product-roadmap` | Update product sections (after initial creation) |
| `/skill design-os-data-shape` | Update data entities (after initial creation) |
| `/skill design-os-sample-data` | Update sample data and types (after initial creation) |

---

## Documentation & Installation

Full docs, installation, usage, & best practices in the [`docs/`](docs/) directory:
- [Getting Started](docs/getting-started.md)
- [Usage](docs/usage.md)
- [Product Planning](docs/product-planning.md)
- [Designing Sections](docs/design-section.md)
- [Export](docs/export.md)
- [Codebase Implementation](docs/codebase-implementation.md)
- [Requirements](docs/requirements.md)

---

## Compatibility

- **Works with Hermes Agent** (this adaptation) or any AI coding agent for implementation: Claude Code, Cursor, Copilot, Codex, or anything that can implement from a handoff
- Your frontend needs **React** and **Tailwind CSS v4**
- Your backend can be anything — Rails, Laravel, Next.js, Python, Go, whatever

## Open Source

Design OS is free, open source, and runs locally.

---

## Differences from the Original

This Hermes adaptation makes the following changes:

| Aspect | Original (Claude Code) | Hermes Edition |
|--------|------------------------|----------------|
| Slash commands | `.claude/commands/design-os/*.md` | `.hermes/skills/design-os-*/SKILL.md` |
| Agent instructions | `agents.md` / `claude.md` | `AGENTS.md` (Hermes convention) |
| Interactive questions | `AskUserQuestion` tool | `clarify` tool |
| Screenshot capture | Playwright MCP server | Hermes native browser tools |
| Frontend design skill | `.claude/skills/frontend-design/` | `.hermes/skills/design-os-frontend-design/` |
| Invocation | `/product-vision` | `/skill design-os-product-vision` |

All file formats, design principles, and the overall process remain **identical** — the Design OS React app works unchanged because it parses the same `product/` directory structure.

---

## Created by

Originally created by [Brian Casel](https://buildermethods.com) at [Builder Methods](https://buildermethods.com).

Hermes Agent adaptation by Nicolas Lima.

Get Brian's free resources on building with AI:
- [Builder Briefing newsletter](https://buildermethods.com)
- [YouTube](https://youtube.com/@briancasel)