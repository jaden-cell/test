# AZ Networking Event Agent

Finds business networking events (chamber mixers, breakfasts, leads groups, etc.)
in Scottsdale and Tempe, AZ, and adds the ones you approve to your Google Calendar
(`jaden@addrivesolutions.com`, America/Phoenix).

This isn't a scraping codebase — chamber sites change layout often and most
social platforms (Facebook/LinkedIn events) actively block automated scraping.
Instead, it runs as a **weekly Claude Routine**: a scheduled agent run that
searches/fetches the sources in [`sources.md`](./sources.md), filters for
upcoming events, and sends you a shortlist for approval before anything
touches your calendar.

## How a run works

1. Search + fetch each source in `sources.md` for events in the next ~3 weeks.
2. Filter to Scottsdale/Tempe business networking events (mixers, breakfasts,
   ribbon cuttings, leads groups, young professional/industry meetups) —
   skip pure social, non-business, or outside-the-area results.
3. De-dupe against events already on the calendar.
4. Message a shortlist: event name, host, date/time, location, cost, link.
5. Wait for approval. On approval, create the corresponding Google Calendar
   event(s) with the source link in the description.

## Changing behavior

- Add/remove sources: edit `sources.md`.
- Change cadence, day/time, or switch to auto-add without review: update the
  Routine (`AZ Networking Events Scan`) via the trigger tools, or just ask
  Claude in a session to change it.
- Change target calendar or lookahead window: edit the routine prompt (see
  `sources.md` header) or ask Claude to adjust it.
