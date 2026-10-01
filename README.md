# Browse Bridge for Cursor

Cursor Plugin that wires **Browse Bridge** remote MCP into Cursor so agents can observe and control browser tabs you have Explicitly Enabled in the Chrome extension.

- **MCP:** `https://mcp.browsebridge.com/mcp`
- **Site:** [https://browsebridge.com](https://browsebridge.com)
- **License:** MIT

## Prerequisites

1. A Browse Bridge account and API key from **Dashboard → Connections** (key prefix `bbk_`).
2. The **Browse Bridge Chrome extension** installed and signed in (same account).
3. Cursor with Plugins / MCP support.

## Install (Marketplace / local)

### Official Marketplace (after listing)

Install **browse-bridge** from the Cursor Marketplace and paste your API key when prompted (`BROWSEBRIDGE_API_KEY`).

### Local test (before / without Marketplace)

```bash
# Copy (do not symlink outside this folder)
cp -R /path/to/browsebridge-cursor-plugin ~/.cursor/plugins/local/browse-bridge
```

Restart Cursor, open Plugins, configure `BROWSEBRIDGE_API_KEY`, confirm MCP tools appear (`browser_observe`, `browser_click`, etc.).

### Manual `mcp.json` snippet

```json
{
  "mcpServers": {
    "browse-bridge": {
      "url": "https://mcp.browsebridge.com/mcp",
      "headers": {
        "Authorization": "Bearer ${BROWSEBRIDGE_API_KEY}"
      }
    }
  }
}
```

## Usage

1. Open a normal website tab (not `chrome://`).
2. Open the Browse Bridge extension popup → **Enable Agent** → Agree to the enable confirmation.
3. In Cursor, use MCP tools such as `browser_list_sessions`, `browser_observe`, `browser_click`, `browser_screenshot`.
4. Challenges / sensitive sites may pause the agent for human Take over or Approve.

## Configuration

| Variable | Required | Description |
| --- | --- | --- |
| `BROWSEBRIDGE_API_KEY` | Yes | API key from the Browse Bridge dashboard |

Declared in `.cursor-plugin/plugin.json` → `variables` and referenced only as `${BROWSEBRIDGE_API_KEY}` in `mcp.json`.

## Privacy & security

See [PRIVACY.md](./PRIVACY.md) and [SECURITY.md](./SECURITY.md).

## Publish checklist (maintainers)

- [ ] Repository set to BryanHamilton/browsebridge-cursor-plugin — create the empty public repo on GitHub then push
- [x] Support email confirmed as `support@browsebridge.com` (also `abuse@browsebridge.com` on site)
- [ ] Public GitHub repo on `main` with this layout
- [ ] Local plugin smoke test
- [ ] Submit at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish)
- [ ] Optional: also list on [cursor.directory](https://cursor.directory)

## Repo layout

```
.cursor-plugin/plugin.json
mcp.json
assets/logo.svg
README.md
LICENSE
PRIVACY.md
SECURITY.md
SUPPORT.md
```
