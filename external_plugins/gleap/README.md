# Gleap plugin for Grok Build

Connect Grok Build to [Gleap](https://www.gleap.ai), the customer support and feedback platform
for AI support, live chat, bug reporting, feature requests, roadmaps, help center and surveys.
Work with your Gleap tickets, customers and feedback through the hosted Gleap MCP server.

## Installation

In Grok Build, open `/plugin`, search for **Gleap**, and install.

On first connection, Grok opens the Gleap sign-in in your browser. Sign in, pick the Gleap
project you want Grok to work with, and approve. No API key is needed and nothing should be
pasted into chat.

## What you get

- **MCP server** `gleap` at `https://mcp.gleap.io/mcp` (Streamable HTTP, OAuth 2.1).
- **Skill** `gleap`: how to use the Gleap tools well (find IDs before acting, read a ticket
  before answering, only message customers when asked, confirm destructive and publishing
  actions, prefer staging replies for human review).

### Tools

| Area | Examples |
|---|---|
| Tickets | `search_tickets`, `find_tickets`, `get_ticket`, `get_ticket_messages`, `update_ticket`, `assign_ticket`, `add_ticket_tags`, `close_ticket`, `merge_tickets`, `search_similar_tickets` |
| Conversations | `send_message` (customer reply or internal note), `draft_reply_to_composer` (stage a reply for review, sends nothing) |
| Workflows | `get_workflows_available_for_ticket`, `run_ticket_workflow` |
| Feature requests | `search_feature_requests`, `get_feature_request`, `create_feature_request` |
| Contacts and CRM | `search_contacts`, `get_contact`, `get_contact_tickets`, `get_company`, `get_pipelines`, `get_pipeline_stats`, `move_pipeline_entry` |
| Knowledge | `search_knowledgebase`, `get_help_center_article`, `create_help_center_article`, `update_help_center_article` |
| Surveys | `list_surveys`, `get_survey_results`, `get_survey_insights`, `search_survey_responses` |
| Statistics | `get_statistics_facts`, `get_statistics_list`, `get_statistics_bar_chart` |

Every tool carries MCP annotations (`readOnlyHint`, `destructiveHint`), so Grok can tell a
lookup from a customer-facing or destructive action before calling it.

## Example prompts

- "Summarize the open Gleap tickets tagged billing from this week."
- "Which feature requests have the most upvotes right now?"
- "Read ticket #4821 and stage a reply in the composer for me to review."
- "What was our median first response time last month?"
- "Find tickets similar to this bug report and link them."

## Authentication and network

The plugin connects only to Gleap. Authentication is OAuth 2.1 authorization code with PKCE
and dynamic client registration; Grok handles the flow.

Network endpoints:

- `https://mcp.gleap.io/mcp`: hosted MCP (Streamable HTTP)
- `https://mcp.gleap.io/.well-known/oauth-protected-resource`: protected resource metadata
- `https://dashapi.gleap.io/oauth/authorize`, `/oauth/token`, `/oauth/register`, `/oauth/revoke`: OAuth 2.1 + DCR
- `https://dashapi.gleap.io/.well-known/oauth-authorization-server`: authorization server metadata
- `https://app.gleap.io`: human sign-in and consent screen during authorization

Credentials: a Gleap account. During consent the user picks one Gleap project; the issued
token can only access that project. Access tokens expire after 1 hour and refresh tokens after
30 days. The plugin stores no API key and requests no filesystem or shell access.

US-hosted Gleap projects use `https://mcp.us.gleap.ai/mcp` (authorization server
`https://dashapi.us.gleap.ai`); change the URL in `.mcp.json` if your project is hosted in the US.

## License

MIT for the files in this plugin. Use of Gleap is governed by the
[Gleap terms](https://www.gleap.ai/legal/terms-of-service) and [privacy policy](https://www.gleap.ai/legal/privacy-policy).
