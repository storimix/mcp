# Storimix Style & Character Consistency (MCP Server)

[![MCP Standard](https://img.shields.io/badge/MCP-Standard-purple.svg)](https://modelcontextprotocol.io/)
[![OAuth 2.0 PKCE](https://img.shields.io/badge/Auth-OAuth_2.0_PKCE-blue.svg)](https://oauth.net/2/pkce/)
[![License](https://img.shields.io/badge/License-Apache_2.0-green.svg)](LICENSE)

The official **Remote Model Context Protocol (MCP)** server for [Storimix](https://storimix.com).

Connect external AI assistants (Claude, Gemini, Cursor, Antigravity) and design platforms directly to your Storimix account. Storimix serves as the **authoritative visual reference and consistency infrastructure**, providing clean turnaround sheets, facial portraits, and style anchors to maintain character likeness across any generative AI platform.

---

## Key Capabilities

* 🎨 **Style & Character Consistency Authority**: Feeds exact character turnaround sheets and face crops directly into external image generation prompts.
* ⚡ **Model-Specific Conditioning**: Automatically structures visual references for:
  * **Gemini & NanoBanana**: Injects multi-image reference arrays and style-first prompt prefixes.
  * **Midjourney**: Generates calibrated `--cref <url> --cw 70` and `--sref <url>` flags.
  * **Adobe Firefly**: Supplies high-resolution Structure and Style reference image assets.
  * **Flux & SDXL**: Formats IP-Adapter and ControlNet image reference weights.
* 🔒 **Secure OAuth 2.0 & Read-Only**: Authenticates via user single-sign-on. Connected apps cannot modify your stories, alter characters, or spend credits.

---

## Available MCP Tools

| Tool | Description |
| :--- | :--- |
| `list_worlds` | Lists all worlds accessible to your Storimix account, including genres and art style summaries. |
| `list_characters` | Lists characters (optionally filtered by `world_id`) with thumbnails and physical descriptions. |
| `get_character_conditioning` | Returns the **complete visual reference bundle** (turnaround URL, portrait URL, style prompt, and ready-to-inject flags for Gemini, Midjourney, Firefly, and Flux). |
| `get_world_style` | Retrieves world art medium, composition guidelines, and master style reference images. |

---

## 1-Click Installation

### Option 1: Install via Smithery (Recommended)
Visit the [Storimix listing on Smithery.ai](https://smithery.ai) and click **"Install into Claude / Cursor"**.

### Option 2: Claude Desktop (Manual Config)
Add the following to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "storimix": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://aygvhavchenfpwqzgkue.supabase.co/functions/v1/mcp"
      ]
    }
  }
}
```

When you start Claude Desktop, a browser window will open prompting you to log into Storimix and approve access.

---

## Example Usage in AI Assistants

Once connected, simply ask your assistant naturally:

> *"What characters do I have in my Woodland Tales world in Storimix?"*

> *"Generate an image in NanoBanana of Barnaby the Badger baking sourdough bread. Use his Storimix character reference and world style."*

The model will call `get_character_conditioning`, attach Barnaby's turnaround sheet URL, and inject the exact prompt parameters automatically.

---

## Privacy & Permissions

* **Read-Only**: The MCP server is strictly read-only.
* **RLS Enforced**: All queries run within your personal account permissions via Row Level Security (RLS).
* **Revocable**: You can view active connections and revoke access at any time from your Storimix Settings.

---

## Links

* [Storimix Web App](https://storimix.com)
* [Model Context Protocol Documentation](https://modelcontextprotocol.io/)
* [Support & Inquiries](mailto:support@storimix.com)
