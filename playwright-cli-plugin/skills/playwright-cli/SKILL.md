---
name: playwright-cli
description: Use when the user wants to control a web browser, scrape website data, take page screenshots, fill forms, click buttons, run web tests, or automate any live web interaction. Triggers on "go to this site and get X", "scrape float data", "automate this form", "screenshot this page", "test my frontend", or "click the button on this site".
---

# Playwright CLI — Browser Automation

Microsoft's official Playwright CLI as a Claude Code skill. Control Chrome — navigate,
interact, screenshot, scrape, test — headless or visible.

**Requires:** `npm install -g @playwright/mcp@latest`

## When to Use

- Scraping sites without public APIs (Finviz, earnings calendars, short interest)
- Taking screenshots of charts or web pages
- Automating form submissions or UI interactions
- Testing your SaaS frontend during development

**Skip when:** A public API already covers the data. Skip for static pages — `web_fetch` is faster. Use `opencli` for structured data from the 17 supported sites.

## Standard Workflow

1. Open URL: `playwright-cli open <url>`
2. Get element refs: `playwright-cli snapshot`
3. Interact using refs: `playwright-cli click e12`
4. Verify: `playwright-cli screenshot`

## Core Commands

```bash
# Navigation
playwright-cli open <url>              # Open URL
playwright-cli open <url> --headed     # See the browser
playwright-cli close                   # Close page
playwright-cli go-back
playwright-cli reload

# Page
playwright-cli snapshot                # Get element refs (do this before clicking)
playwright-cli screenshot              # Full page screenshot
playwright-cli pdf                     # Save as PDF
playwright-cli eval <js>               # Execute JavaScript

# Interaction
playwright-cli click <ref>             # Click element (ref from snapshot)
playwright-cli dblclick <ref>
playwright-cli type <text>             # Type into focused element
playwright-cli fill <ref> <text>       # Fill a specific field
playwright-cli select <ref> <value>    # Dropdown
playwright-cli check <ref>             # Checkbox on
playwright-cli uncheck <ref>           # Checkbox off
playwright-cli hover <ref>
playwright-cli press <key>             # e.g. Enter, Tab, Escape, ArrowDown

# DevTools
playwright-cli console                 # Browser console messages
playwright-cli network                 # Network requests log

# Tabs
playwright-cli tab-new [url]
playwright-cli tab-list
playwright-cli tab-select <index>
playwright-cli tab-close [index]
```

## Sessions (Multiple Browsers)

```bash
playwright-cli open https://site-a.com              # Default session
playwright-cli --session=work open https://site-b.com
playwright-cli session-list
playwright-cli session-stop-all
```

Sessions persist cookies and storage between calls.

## Trading Use Cases

```bash
# Scrape Finviz for float data
playwright-cli open "https://finviz.com/quote.ashx?t=NVDA" --headed
playwright-cli snapshot
playwright-cli screenshot

# Grab earnings calendar
playwright-cli open "https://earningswhispers.com/calendar"
playwright-cli snapshot

# Test SaaS dashboard
playwright-cli open "http://localhost:3000"
playwright-cli click e5    # Login button ref from snapshot
playwright-cli screenshot
```

## Common Mistakes

- Clicking before taking a snapshot — always `snapshot` first to get element refs
- Using `type` when `fill` is needed — `type` simulates keystrokes on whatever is focused; `fill` sets a field directly
- Not using `--headed` when debugging — add it to see what's happening
- Using this for static page reading — `web_fetch` is faster and lighter
