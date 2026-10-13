---
name: setmore
description: >-
  Work with Setmore scheduling through the Setmore MCP server: check the agenda and
  available slots, book, reschedule and cancel appointments, manage services, customers,
  staff working hours and booking settings, and read Setmore Connect messages. Use whenever
  "Setmore", a Setmore booking page, or the user's Setmore calendar, customers or services
  come up.
---

# Setmore

Use the `setmore` MCP server bundled with this plugin.

- Look things up instead of asking: staff with `search_staff`, customers with `search_customers`, services with `list_services`, events with `get_agenda`.
- Check availability (`fetch_available_slots`) before booking.
- Confirm with the user before cancelling, rescheduling or deleting anything.
- Never guess ids, durations or time zones; tools answer in the signed-in user's time zone.
