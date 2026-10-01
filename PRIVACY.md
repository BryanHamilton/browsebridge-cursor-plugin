# Privacy — Browse Bridge Cursor plugin

This repository is a **Cursor Plugin** that configures a remote MCP client. It does not ship binaries and does not collect telemetry by itself.

## What connects where

- Cursor talks to **`https://mcp.browsebridge.com/mcp`** using the API key you enter at install (`BROWSEBRIDGE_API_KEY`).
- The Chrome extension (installed separately from [browsebridge.com](https://browsebridge.com)) shares tabs you explicitly **Enable**.
- Page content, screenshots, and action results are processed to fulfill agent `browser_*` tools according to your Browse Bridge account plan and legal attestations.

## What this plugin does **not** do

- It does not embed or commit your API key.
- It does not train models on your data within this repo (configuration only).
- It does not access tabs you have not Enabled.

## Product privacy policy

**Status (2026-10-01):** No public Privacy Policy URL was found on browsebridge.com
(`/privacy`, `/privacy-policy`, `/legal/privacy` all returned 404). Related public
legal pages that *do* exist: [Terms](https://browsebridge.com/terms),
[Acceptable use](https://browsebridge.com/acceptable-use),
[Legal versions](https://browsebridge.com/legal/versions), [FAQ](https://browsebridge.com/faq).

When a product Privacy Policy is published (recommended path:
`https://browsebridge.com/privacy`), replace this paragraph with a direct link.

## Your responsibilities

- Keep API keys secret; rotate if exposed.
- Follow site terms of service for any site you Enable.
- Review Browse Bridge account terms and legal settings on [browsebridge.com](https://browsebridge.com).

For product privacy questions: **support@browsebridge.com**
