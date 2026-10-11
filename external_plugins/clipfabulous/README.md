# ClipFabulous plugin for Grok Build

Connect Grok Build to [ClipFabulous](https://clipfabulous.com) to create and edit
JPEG images, inspect image options and credit costs, check your account, and
retrieve existing saved creations.

This package contains one remote MCP connection. It has no local runtime,
installation scripts, hooks, skills, agents, or shell tools.

## Local evaluation

From a checkout of this marketplace repository:

```bash
grok --plugin-dir ./external_plugins/clipfabulous
```

Authorize the ClipFabulous connection in the browser using your ClipFabulous
account. Credentials are entered on ClipFabulous, not in the chat. The package
contains no API key, OAuth client secret, access token, or account identifier.

The remote MCP uses Streamable HTTP; Grok Build's configuration identifies this
transport with `"type": "http"`.

## Available tools

| Tool | Purpose | Credit behavior |
| --- | --- | --- |
| `get_profile` | Identify the connected creator account. | Read only. |
| `check_credit_balance` | Read available account credits. | Read only. |
| `list_image_models` | Inspect image qualities, aspect ratios, and current credit prices. | Read only. |
| `list_creations` | Retrieve existing images and saved motion-card videos from the connected account. | Read only. |
| `generate_image` | Quote and generate a JPEG. | A confirmed generation consumes ClipFabulous credits. |
| `edit_saved_image` | Quote and edit a JPEG already saved in the connected account. | A confirmed edit consumes ClipFabulous credits. |

Tool schemas and available image options are provided by the hosted server.
The selected ClipFabulous account controls access to private creations and the
credit balance used for generation. Grok usage and ClipFabulous credits are
separate.

## Generation and editing approvals

`generate_image` uses a two-step cost confirmation flow: the first request uses
`confirm_cost=false` to obtain a credit quote. After the user explicitly approves
that quoted cost, the same settings can be submitted with `confirm_cost=true`.

`edit_saved_image` also requires a cost quote and explicit cost approval. Editing
additionally requires the user's permission to edit the source image, represented
by `confirmed_rights=true`. Quoting a request does not itself authorize a paid
generation or edit.

The connector does not create or export new MP4 videos, cancel subscriptions, or
issue cash refunds. Retrieving an existing saved video does not add video
generation or export capability.

## Authentication and network access

The connection uses the ClipFabulous account authorization flow with OAuth
discovery, dynamic client registration, and PKCE using S256. An unauthenticated
MCP request is challenged before account tools can be used.

Public service endpoints:

| Endpoint | Purpose |
| --- | --- |
| `https://clipfabulous.com/mcp` | Remote MCP discovery and tool calls. |
| `https://clipfabulous.com/oauth/authorize` | Browser authorization by the account holder. |
| `https://clipfabulous.com/oauth/token` | OAuth token exchange. |
| `https://clipfabulous.com/oauth/register` | Dynamic OAuth client registration. |

The OAuth issuer is `https://clipfabulous.com`. The client manages authorization
tokens for the connection; the plugin does not read local files, environment
variables, or credentials. This package adds no telemetry. Image prompts and
tool parameters are processed by the hosted ClipFabulous service under its
privacy policy. The service can return media URLs for the user's creations;
opening a returned media URL is separate from the package's MCP configuration.

## Verification scope

The package reuses the public MCP endpoint and supported capability set from
ClipFabulous's existing publisher package. Metadata extraction and catalog
validation check the packaging. They do not demonstrate successful Grok Build
sign-in, tool execution, credit deduction, or media rendering; those require a
separate authenticated compatibility test.

## Support and policies

- [Support](https://clipfabulous.com/support/)
- [Privacy policy](https://clipfabulous.com/privacy/)
- [Terms of service](https://clipfabulous.com/terms/)
- [Existing connector reviewer demonstration](https://clipfabulous-review.rocket-launcher.io/)

The linked demonstration documents the existing connector workflow. It is not a
claim of Grok Build marketplace approval or a Grok Build compatibility test.

## License

The new connector packaging files in this directory are available under the
[MIT license](LICENSE). This license does not cover the hosted ClipFabulous
service, its backend, generated media, pre-existing code, logos, or trademarks.
Use of the hosted service remains governed by ClipFabulous's terms and privacy
policy.
