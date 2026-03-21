---
name: playwright-cli
description: Control a web browser from Claude Code. Use when the user wants to automate browser actions, scrape websites, take screenshots, fill forms, click buttons, or run web tests.
---

# Playwright CLI — Browser Automation for Claude Code

Microsoft's Playwright CLI as a Claude Code skill. Control Chrome, navigate pages, interact with elements, take screenshots, and automate any web task.

## When to Use This Skill

- User wants to scrape data from a website
- User wants to automate browser interactions
- User wants to take screenshots of web pages
- User wants to test a web application
- User says "go to X website and get Y data" or "automate this web task"

## Setup Requirement

```bash
npm install -g @playwright/mcp@latest
```

## Core Commands

```bash
playwright-cli open <url>          # Open a URL
playwright-cli snapshot            # Capture page to get element refs
playwright-cli click <ref>         # Click an element
playwright-cli type <text>         # Type into focused element
playwright-cli fill <ref> <text>   # Fill a form field
playwright-cli screenshot          # Take a screenshot
playwright-cli select <ref> <val>  # Select dropdown option
playwright-cli check <ref>         # Check a checkbox
playwright-cli go-back             # Navigate back
playwright-cli reload              # Reload page
playwright-cli pdf                 # Save page as PDF
```

## Sessions (Multiple Browsers)

```bash
playwright-cli open https://site1.com           # Default session
playwright-cli --session=work open https://...  # Named session
playwright-cli session-list                     # List sessions
playwright-cli session-stop-all                 # Close all
```

## DevTools

```bash
playwright-cli console              # Browser console messages
playwright-cli network              # Network requests log
playwright-cli tracing-start        # Record trace
playwright-cli tracing-stop         # Stop and save trace
```

## Trading Use Cases

- Scrape float data from Finviz or other sites without APIs
- Screenshot charts for analysis
- Automate form submissions for broker platforms
- Scrape earnings calendars not available via API
- Test your SaaS frontend during development

## Headed Mode (See the Browser)

```bash
playwright-cli open https://example.com --headed
```
