# Browse Bridge for Cursor

Cursor Plugin that wires **Browse Bridge** remote MCP into Cursor so agents can observe and control browser tabs you have Explicitly Enabled in the Chrome extension.

- **MCP:** `https://mcp.browsebridge.com/mcp`
- **Site:** [https://browsebridge.com](https://browsebridge.com)
- **Chrome extension:** listed on the [Chrome Web Store](https://chromewebstore.google.com/detail/browse-bridge/fbnpefbmmljjgnlagkcbnnfknpomhidb)
- **License:** MIT

## Prerequisites

1. Create an account at [https://browsebridge.com/sign-up](https://browsebridge.com/sign-up) (plans: [https://browsebridge.com/plans](https://browsebridge.com/plans)).
2. Install the Browse Bridge Chrome extension from the [Chrome Web Store](https://chromewebstore.google.com/detail/browse-bridge/fbnpefbmmljjgnlagkcbnnfknpomhidb) and sign in with the same account.
3. Sign in and open [Connections](https://browsebridge.com/sign-in?next=/dashboard/connections) to create an API key (starts with `bbk_`). Keep it secret.
4. Cursor with plugin/MCP support.

## Install (Marketplace / local)

### Official Marketplace (after listing)

Install **browse-bridge** from the Cursor Marketplace and paste your API key when prompted (`BROWSEBRIDGE_API_KEY`).

### Local test (before / without Marketplace)

```bash
# Copy (do not symlink outside this folder)
cp -R /path/to/browsebridge-cursor-plugin ~/.cursor/plugins/local/browse-bridge
```

Restart Cursor, open Customize, configure `BROWSEBRIDGE_API_KEY`, confirm MCP tools appear (`browser_observe`, `browser_click`, etc.).

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

Plugin variables only fill in inside the plugin, so for a manual config use your real key or `${env:BROWSEBRIDGE_API_KEY}`.

## Usage

1. Open a normal website tab (not `chrome://`).
2. Click the Browse Bridge toolbar icon, then Enable on the tab you want to share. Accept the confirmation and any Chrome permission prompt. Use Take control (or Ctrl+Shift+Period) to take the tab back at any time.
3. In Cursor, use MCP tools such as `browser_list_sessions`, `browser_observe`, `browser_click`, `browser_screenshot`.
4. Challenges / sensitive sites may pause the agent for human Take over or Approve.

## Tools (17)

| Tool | What it does |
| --- | --- |
| `browser_list_sessions` | List Enabled shared tabs. |
| `browser_get_status` | Control mode, URL, `deviceOnline`, pending approvals. |
| `browser_observe` | Semantic page tree + `observationId` / `elementId`s. |
| `browser_screenshot` | Visible-tab JPEG as MCP image content. |
| `browser_click` | Click an observed element. Optional `button`: `"left"` (default), `"right"`, or `"middle"`. |
| `browser_type` | Set a control's value (not a password). |
| `browser_select` | Choose a listed `<option>`. |
| `browser_press_key` | Key in the focused (or named) element. |
| `browser_hover` | `mouseover` / `mouseenter` on an observed element. |
| `browser_scroll` | Scroll the page or an element into view. |
| `browser_navigate` | Go to an allowed http(s) URL. |
| `browser_back` | History back. |
| `browser_forward` | History forward. |
| `browser_reload` | Reload the tab. |
| `browser_wait` | Pause 0–30000 ms. |
| `browser_release_control` | Give the tab back to the human (`controlMode: "human"`). |
| `browser_cancel_approval` | Withdraw a pending agent approval (`approvalId`). |

### Approvals

Sensitive-site clicks/types/navigations and cross-origin navigations (and cross-origin link clicks) return **`APPROVAL_REQUIRED`**. The human Approves or Denies in the Chrome side panel. The agent can withdraw its own request with **`browser_cancel_approval`** (`APPROVAL_CANCELLED` — that is not a human Deny). While an approval is pending, observe/screenshot/wait/get_status/list_sessions/release_control still run.

## Configuration

| Variable | Required | Description |
| --- | --- | --- |
| `BROWSEBRIDGE_API_KEY` | Yes | API key from the Browse Bridge dashboard |

Declared in `.cursor-plugin/plugin.json` → `variables` and referenced only as `${BROWSEBRIDGE_API_KEY}` in `mcp.json`.

## Privacy & security

See [PRIVACY.md](./PRIVACY.md) and [SECURITY.md](./SECURITY.md).

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
