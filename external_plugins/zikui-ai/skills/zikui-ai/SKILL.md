---
name: zikui-ai
description: >-
  Work with Zikui AI through the Zikui AI MCP server: check an Israeli parking fine
  with the issuing city and see its enforcement photos, read a photo or PDF of a fine,
  follow the user's appeals, statuses and deadlines, and prepare an appeal that the
  user finishes on zikui.ai. Use whenever "Zikui", "Zikui AI", "zikui.ai", or the
  user's own Zikui appeals or fines come up.
---

# Zikui AI

Zikui AI checks Israeli parking and traffic fines and files appeals for drivers. The
`zikui-ai` MCP server bundled with this plugin acts as the signed-in Zikui AI user and
only sees that user's own account.

## Reading results

Every tool returns a `status`:

- `found` / `ok` / `read`: the data is real.
- `not_found`: the source answered and has nothing.
- `unavailable`: Zikui could not complete the check. This is never evidence that a
  fine or appeal does not exist. Say the check did not finish, not that there is
  nothing.

## Choosing a tool

| The user wants to | Use |
|---|---|
| Know where their appeals stand, what needs them, the next deadline | `get_my_overview`, then `list_my_appeals` / `get_appeal` for detail |
| See fines Zikui already found on their vehicles | `list_my_discovered_fines` |
| Check one parking fine they are holding | `verify_report` (report number, plate, city in Hebrew or as a slug) |
| See the city's enforcement photos | photos come with `verify_report`; if not yet, `get_fine_photos` a minute later |
| Read a paper fine | `scan_report` with the photo or PDF |
| Appeal | ask what happened, `analyze_appeal`, ask its questions, then `create_appeal`; give the user the returned zikui.ai link. `prepare_appeal` is the lighter option when they prefer to tell their story on the website |
| Know the price | `get_appeal_quote`, only when they ask |

Police traffic fines cannot be checked with the city: do not call `verify_report` for
them.

## Rules

- Never ask for a national ID number, passwords or SMS codes in the chat. ID, signature
  and payment are collected only on zikui.ai.
- Nothing is filed with an authority from the chat. `create_appeal` saves an unfiled
  appeal on the user's account; the user finishes and Zikui files it on zikui.ai.
- Never promise that an appeal will succeed and never promise or suggest a refund. The
  case strength from `analyze_appeal` is an assessment, not a prediction.
