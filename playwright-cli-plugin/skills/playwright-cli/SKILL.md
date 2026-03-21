---
name: playwright-cli
description: >
  Use this skill whenever the user wants to control a web browser, automate browser actions,
  scrape website data, take screenshots of web pages, fill forms, click buttons, or run web
  tests. Trigger for requests like "go to this website and get X data", "take a screenshot of
  this page", "scrape the float data from Finviz", "automate this form submission", "check
  what's on this page", "click the button on this site", or "test my web app". Also trigger
  for any trading-related web automation — scraping stock screeners, pulling short interest
  data, grabbing earnings calendars from sites without APIs, or testing a SaaS frontend.
  Skip when a public API already exists for the data the user wants — use that instead.
  Skip for static page reading where web_fetch is sufficient. Use this skill when the user
  needs actual browser interaction: JavaScript execution, login sessions, dynamic content,
  or clicking/typing on a live page.
---

# Playwright CLI — Browser Automation for Claude Code

Microsoft's official Playwright CLI as a Claude Code skill. Control Chrome headlessly or
visually — navigate pages, interact with elements, take screenshots, run web tests.

## Prerequisites

```bash
npm install -g @playwright/mcp@latest
```

## Core Commands

```bash
# Navigation
playwright-cli open <url>              # Open a URL in the browser
playwright-cli close                   # Close the current page
playwright-cli go-back                 # Navigate back
playwright-cli go-forward              # Navigate forward
playwright-cli reload                  # Reload current page

# Page Analysis
playwright-cli snapshot                # Capture page snapshot — gets element refs
playwright-cli screenshot              # Take a screenshot
playwright-cli screenshot <ref>        # Screenshot of a specific element
playwright-cli pdf                     # Save page as PDF

# Interaction
playwright-cli click <ref>             # Click an element (get ref from snapshot)
playwright-cli dblclick <ref>          # Double-click
playwright-cli type <text>             # Type text into focused element
playwright-cli fill <ref> <text>       # Fill a specific form field
playwright-cli select <ref> <value>    # Select dropdown option
playwright-cli check <ref>             # Check a checkbox
playwright-cli uncheck <ref>           # Uncheck a checkbox
playwright-cli hover <ref>             # Hover over element
playwright-cli drag <startRef> <endRef># Drag and drop

# Keyboard
playwright-cli press <key>             # Press a key (e.g. Enter, Tab, Escape)
playwright-cli keydown <key>           # Hold a key down
playwright-cli keyup <key>             # Release a key

# JavaScript
playwright-cli eval <function>         # Execute JavaScript on the page
playwright-cli eval <function> <ref>   # Execute JS on a specific element

# Dialogs
playwright-cli dialog-accept           # Accept a browser dialog/alert
playwright-cli dialog-dismiss          # Dismiss a dialog

# Window
playwright-cli resize <w> <h>          # Resize browser window

# Tabs
playwright-cli tab-new [url]           # Open a new tab
playwright-cli tab-list                # List all open tabs
playwright-cli tab-select <index>      # Switch to a tab
playwright-cli tab-close [index]       # Close a tab

# DevTools
playwright-cli console                 # Read browser console messages
playwright-cli network                 # List network requests
playwright-cli tracing-start           # Start recording a trace
playwright-cli tracing-stop            # Stop and save trace
playwright-cli run-code <code>         # Run arbitrary Playwright code
```

## Standard Workflow

1. Open the page: `playwright-cli open https://finviz.com/screener.ashx`
2. Snapshot for element refs: `playwright-cli snapshot`
3. Interact using refs from snapshot: `playwright-cli click e12`
4. Type/fill: `playwright-cli fill e23 "NVDA"`
5. Screenshot to verify: `playwright-cli screenshot`

## Sessions (Multiple Browsers)

```bash
playwright-cli open https://site-a.com              # Default session
playwright-cli --session=work open https://site-b.com  # Named session
playwright-cli session-list                         # List all sessions
playwright-cli session-stop work                    # Stop a session
playwright-cli session-stop-all                     # Close all sessions
```

Sessions are persistent — cookies and storage are preserved between calls.

## Headed Mode (See the Browser)

```bash
playwright-cli open https://example.com --headed
```

## Trading Use Cases

```bash
# Scrape float data from Finviz
playwright-cli open "https://finviz.com/quote.ashx?t=NVDA" --headed
playwright-cli snapshot
playwright-cli screenshot

# Grab earnings calendar
playwright-cli open "https://earningswhispers.com/calendar"
playwright-cli snapshot

# Test your SaaS trading dashboard
playwright-cli open "http://localhost:3000"
playwright-cli screenshot
playwright-cli click e5    # Click login button (ref from snapshot)
```

## Environment Variable for Session

```bash
PLAYWRIGHT_CLI_SESSION=trading-app claude .
```
Sets the session automatically for all playwright-cli calls in that Claude session.
