---
name: playwright-cli
description: Controls a web browser to navigate pages, click elements, fill forms, take screenshots, and scrape data. Use when the user wants to interact with a live website, automate browser actions, or extract data from a page that requires JavaScript or login.
---

# Playwright CLI

Browser automation via CLI. Navigate pages, interact with elements, take screenshots,
and extract data from any website.

**Before running any `playwright-cli` command, ensure the package is installed:**
```bash
npm install -g @playwright/mcp@latest
```

## Workflow

### Standard scraping or automation workflow

1. Open the target page:
   ```bash
   playwright-cli open <url>
   ```

2. Snapshot the page to get element references:
   ```bash
   playwright-cli snapshot
   ```
   This returns a structured representation of the page with element refs (e1, e2, etc.)

3. Interact using refs from the snapshot:
   ```bash
   playwright-cli click <ref>
   playwright-cli fill <ref> "search term"
   playwright-cli press Enter
   ```

4. Snapshot again to see the updated page, then extract data or screenshot:
   ```bash
   playwright-cli snapshot
   playwright-cli screenshot
   ```

5. Close when done:
   ```bash
   playwright-cli close
   ```

### Taking a screenshot

```bash
playwright-cli open <url>
playwright-cli screenshot
```

### Saving a page as PDF

```bash
playwright-cli open <url>
playwright-cli pdf
```

### Reading browser console or network logs

```bash
playwright-cli open <url>
playwright-cli console
playwright-cli network
```

## All commands

**Navigation**
```bash
playwright-cli open <url>          # Open URL
playwright-cli close               # Close page
playwright-cli go-back             # Navigate back
playwright-cli go-forward          # Navigate forward
playwright-cli reload              # Reload page
playwright-cli resize <w> <h>      # Resize window
```

**Analysis**
```bash
playwright-cli snapshot            # Capture page structure + element refs
playwright-cli screenshot          # Take screenshot
playwright-cli screenshot <ref>    # Screenshot specific element
playwright-cli pdf                 # Save as PDF
playwright-cli console             # Browser console output
playwright-cli network             # Network requests
```

**Interaction** (requires element ref from snapshot)
```bash
playwright-cli click <ref>         # Click element
playwright-cli dblclick <ref>      # Double-click
playwright-cli fill <ref> <text>   # Fill form field
playwright-cli type <text>         # Type into focused element
playwright-cli press <key>         # Press key (Enter, Tab, Escape, etc.)
playwright-cli select <ref> <val>  # Select dropdown value
playwright-cli check <ref>         # Check checkbox
playwright-cli uncheck <ref>       # Uncheck checkbox
playwright-cli hover <ref>         # Hover over element
playwright-cli drag <from> <to>    # Drag and drop
```

**JavaScript**
```bash
playwright-cli eval "<function>"           # Execute JS on page
playwright-cli eval "<function>" <ref>     # Execute JS on element
```

**Tabs**
```bash
playwright-cli tab-new [url]       # Open new tab
playwright-cli tab-list            # List all tabs
playwright-cli tab-select <index>  # Switch to tab
playwright-cli tab-close [index]   # Close tab
```

## Sessions

Named sessions maintain separate browser profiles with independent cookies:

```bash
playwright-cli open <url>                       # Default session
playwright-cli --session=work open <url>        # Named session
playwright-cli session-list                     # List sessions
playwright-cli session-stop <name>              # Stop session
playwright-cli session-stop-all                 # Stop all
```

Set session via environment variable for a whole Claude Code run:
```bash
PLAYWRIGHT_CLI_SESSION=trading-app claude .
```

## Headed mode (see the browser)

```bash
playwright-cli open <url> --headed
```
