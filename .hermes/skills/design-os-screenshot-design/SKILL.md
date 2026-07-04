---
name: design-os-screenshot-design
description: "Design OS Phase 2: Capture screenshots of screen designs for documentation. Uses Hermes native browser tools (no Playwright MCP needed)."
version: 1.0.0
parent: design-os
---

# Screenshot Screen Design

You are helping the user capture a screenshot of a screen design they've created. The screenshot will be saved to the product folder for documentation purposes.

## Prerequisites: Hermes Browser Tools

This skill uses Hermes Agent's **native browser tools** — no external MCP server installation needed.

Required tools (all built into Hermes):
- `browser_navigate` — Navigate to a URL
- `browser_vision` — Take a screenshot and inspect the page visually
- `browser_click` — Click on elements (e.g., to hide the nav bar before screenshotting)
- `terminal` — To start the dev server and copy screenshot files

If browser tools are not enabled, inform the user:

"To capture screenshots, I need the browser toolset enabled. You can enable it with:
```bash
hermes tools enable browser
```
Then start a new session (or `/reset`) and load this skill again."

Do not proceed if browser tools are not available.

## Step 1: Identify the Screen Design

First, determine which screen design to screenshot.

Read `product/product-roadmap.md` to get the list of available sections, then check `src/sections/` to see what screen designs exist.

If only one screen design exists across all sections, auto-select it.

If multiple screen designs exist, use the `clarify` tool to ask which one to screenshot:

"Which screen design would you like to screenshot?"

Present the available screen designs as options, grouped by section:
- [Section Name] / [ScreenDesignName]
- [Section Name] / [ScreenDesignName]

## Step 2: Start the Dev Server

Start the dev server yourself using the `terminal` tool. Run `npm run dev` in the background so you can continue with the screenshot capture.

Do NOT ask the user if the server is running or tell them to start it. You must start it yourself.

After starting the server, wait a few seconds for it to be ready before navigating to the screen design URL.

```bash
# Start dev server in background
cd ~/Projects/design-os-hermes && npm run dev &
```

Wait for the "ready" signal in the output (Vite typically prints "VITE v7.x.x  ready in XXX ms").

## Step 3: Capture the Screenshot

Use Hermes browser tools to navigate to the screen design and capture a screenshot.

The screen design URL pattern is: `http://localhost:5173/sections/[section-id]/screen-designs/[screen-design-name]`

1. **Navigate to the screen design URL** using `browser_navigate`:
   ```
   browser_navigate(url="http://localhost:5173/sections/[section-id]/screen-designs/[screen-design-name]")
   ```

2. **Wait for the page to fully load** — take a snapshot to verify content rendered:
   ```
   browser_snapshot()
   ```

3. **Hide the navigation bar** — look for a "Hide" link/button with attribute `data-hide-header`. Click it using `browser_click`:
   ```
   browser_click(ref="@eN")  # where N is the ref ID of the Hide button
   ```

4. **Capture the screenshot** using `browser_vision`:
   ```
   browser_vision(question="Capture the full page content of this screen design for documentation purposes")
   ```

**Screenshot specifications:**
- Capture at desktop viewport width (1280px recommended)
- Capture the full page content (not just the viewport)
- PNG format for best quality

## Step 4: Save the Screenshot

The `browser_vision` tool returns a screenshot path. Save the screenshot to the product folder:

1. **Get the screenshot path** from the `browser_vision` result (it includes a `screenshot_path` field)

2. **Copy the file to the product folder** using the `terminal` tool:
   ```bash
   cp "[screenshot_path]" "product/sections/[section-id]/[filename].png"
   ```

**Naming convention:** `[screen-design-name]-[variant].png`

Examples:
- `invoice-list.png` (main view)
- `invoice-list-dark.png` (dark mode variant)
- `invoice-detail.png`
- `invoice-form-empty.png` (empty state)

If the user wants both light and dark mode screenshots, capture both.

## Step 5: Confirm Completion

Let the user know:

"I've saved the screenshot to `product/sections/[section-id]/[filename].png`.

The screenshot captures the **[ScreenDesignName]** screen design for the **[Section Title]** section."

If they want additional screenshots (e.g., dark mode, different states):

"Would you like me to capture any additional screenshots? For example:
- Dark mode version
- Mobile viewport
- Different states (empty, loading, etc.)"

## Important Notes

- Start the dev server yourself — do not ask the user to do it
- Use Hermes native browser tools (`browser_navigate`, `browser_vision`, `browser_click`) — no Playwright MCP needed
- Screenshots are saved to `product/sections/[section-id]/` alongside spec.md and data.json
- Use descriptive filenames that indicate the screen design and any variant (dark mode, mobile, etc.)
- Capture at a consistent viewport width for documentation consistency
- Always capture full page screenshots to include all scrollable content
- After you're done, you may kill the dev server if you started it
- The `browser_vision` tool returns a `screenshot_path` — use that to copy the file to the product folder