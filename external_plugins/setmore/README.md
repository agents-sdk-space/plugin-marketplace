# Setmore plugin for Grok Build

Connect Grok Build to [Setmore](https://www.setmore.com) scheduling through the hosted Setmore MCP server.

## Installation

In Grok Build, open `/plugin`, search for **Setmore**, and install. On first connection Grok opens the Setmore sign-in in your browser; authorize with the account whose calendar you want Grok to use. Nothing needs to be pasted into chat.

## What you get

- **MCP server** `setmore` at `https://mcp.setmore.com/mcp` (Streamable HTTP, OAuth 2.1 authorization code with PKCE).
- **Skill** `setmore`: guidance on using the tools safely.

| Area | Tools |
|---|---|
| Agenda & availability | `get_agenda`, `fetch_available_slots`, `find_common_slots`, `create_sharable_slot` |
| Appointments | `create_appointment`, `book_service`, `update_appointment`, `reschedule_appointment`, `cancel_appointment`, `block_time` |
| Customers | `search_customers`, `get_customer`, `create_customer`, `update_customer` |
| Services & staff | `list_services`, `create_service`, `update_service`, `delete_service`, `assign_service_staff`, `search_staff`, `update_working_hours` |
| Settings & reports | `get_settings`, `update_booking_settings`, `update_notification_settings`, `booking_stats`, `get_billing_usage`, `list_integrations` |
| Connect (messaging) | `list_channels`, `read_messages`, `send_message`, `react_to_message`, `get_unread_messages`, `create_collab`, `get_collab_members`, `add_collab_members` |

## Authentication and network

The plugin connects only to Setmore endpoints:

- `https://mcp.setmore.com/mcp`: hosted MCP (Streamable HTTP)
- `https://mcp.setmore.com/.well-known/oauth-protected-resource/mcp`: discovery metadata
- `https://auth.setmore.com/o`: Setmore authorization server (sign-in and consent)

Credentials: a Setmore account. The plugin stores no API key and requests no filesystem or shell access. Tools act only on data the signed-in user can already access in Setmore.

## License

MIT for the files in this plugin. Use of the hosted MCP server is governed by the [Setmore terms](https://www.setmore.com/terms).
