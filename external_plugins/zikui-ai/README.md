# Zikui AI plugin for Grok Build

Connect Grok Build to [Zikui AI](https://zikui.ai), the Israeli service that checks
parking and traffic fines and files appeals for drivers. Check a fine with the city
that issued it, see the enforcement photos, follow your appeals and deadlines, and
prepare an appeal that you finish on zikui.ai.

## Installation

In Grok Build, open `/plugin`, search for **Zikui AI**, and install.

On first connection, Grok opens the Zikui AI sign-in in your browser. Sign in with your
Zikui AI account (free to create at zikui.ai) and approve the connection. No API key is
needed and nothing should be pasted into chat.

## What you get

- **MCP server** `zikui-ai` at `https://zikui.ai/api/mcp` (Streamable HTTP, OAuth 2.1).
- **Skill** `zikui-ai`: how to use the Zikui AI tools well (read the result status,
  never treat "unavailable" as "no fine", never ask for ID numbers or codes in chat).

### Tools

| Area | Tools |
|---|---|
| Your account | `get_my_overview`, `list_my_appeals`, `get_appeal`, `list_my_discovered_fines` |
| Check a fine | `verify_report`, `get_fine_photos`, `scan_report` |
| Appeal | `analyze_appeal`, `create_appeal`, `prepare_appeal`, `get_appeal_quote` |
| Sharing | `get_referral_link` |

Every tool carries MCP annotations (`readOnlyHint`, `destructiveHint`,
`idempotentHint`, `openWorldHint`). Three tools write, and only to the signed-in user's
own Zikui AI account: `create_appeal` (saves an unfiled appeal), `prepare_appeal`
(saves a fine) and `get_referral_link` (creates the user's invite link). Nothing is
filed with an authority, sent, deleted or charged through these tools; ID, signature
and payment happen only on zikui.ai.

## Example prompts

- "Using Zikui AI, give me an overview of my appeals and the nearest deadlines."
- "Which of my appeals need something from me?"
- "Check parking fine 1683629-9 in Jerusalem, plate 5905531, and show me the photos."
- "I want to appeal that fine. I paid for parking in the app but the inspector did not see it."

## Authentication and network

The plugin connects only to `https://zikui.ai`. Authentication is OAuth 2.1
authorization code with PKCE and dynamic client registration; Grok handles the flow.

Network endpoints:

- `https://zikui.ai/api/mcp`: hosted MCP (Streamable HTTP)
- `https://zikui.ai/.well-known/oauth-protected-resource`: discovery metadata
- `https://gfjcdfdwdqzykvrrhpfl.supabase.co/auth/v1`: the OAuth 2.1 authorization server (authorize, token, register)
- `https://zikui.ai/oauth/consent`: human sign-in and consent screen during authorization

Credentials: a Zikui AI account. Access tokens are scoped to that account and sent as
`Authorization: Bearer` on `/api/mcp`. Disconnect any time from Grok's connector
settings. Privacy policy: https://zikui.ai/privacy. Support: https://zikui.ai/contact.
