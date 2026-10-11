# CueEdit plugin for Grok Build

Connect Grok Build to [CueEdit](https://www.cueedit.io): Instagram and Facebook
Page engagement. Reply to comments, set up comment-to-DM auto-reply rules, and
check scheduled posts for the accounts you have connected in CueEdit.

## Installation

In Grok Build, open `/plugin`, search for **CueEdit**, and install.

On first connection, Grok opens CueEdit sign-in in the browser. Sign in with
your CueEdit account and approve access. Do not paste an API key into chat.

## Authentication

The plugin connects only to `https://www.cueedit.io/api/mcp/mcp`.
Authentication is OAuth 2.1 (authorization code + PKCE, dynamic client
registration) against `www.cueedit.io`.

Network endpoints:

- `https://www.cueedit.io/api/mcp/mcp`: hosted MCP (streamable HTTP)
- `https://www.cueedit.io/mcp/authorize`: sign-in and consent
- `https://www.cueedit.io/api/mcp/oauth/token`, `/api/mcp/oauth/register`: OAuth 2.1 token + DCR

Credentials: a CueEdit account. No API key is stored in the plugin. Tools are
scoped to the Instagram and Facebook accounts the signed-in user has connected
in CueEdit. Instagram/Facebook access uses Meta's official Graph API
permissions granted inside CueEdit.

## License

Proprietary. Use of the hosted MCP is governed by CueEdit's terms
(https://www.cueedit.io/terms) and privacy policy (https://www.cueedit.io/privacy).
