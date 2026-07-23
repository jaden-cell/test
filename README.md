# AZ Networking Event Agent

Finds business networking events (chamber mixers, breakfasts, leads groups, etc.)
in Scottsdale and Tempe, AZ, and adds them to Jaden's Google Calendar
(`jaden@addrivesolutions.com`, America/Phoenix). Jaden runs a local ad agency
in Tempe, so events are weighted toward ones likely to put him in front of
local small-business owners — see [`sources.md`](./sources.md) for the full
targeting notes.

This isn't a scraping codebase — chamber sites change layout often and most
social platforms (Facebook/LinkedIn events) actively block automated scraping.
Instead, it runs as a **weekly Claude Routine**: a scheduled agent run that
searches/fetches the sources in `sources.md`, filters for upcoming events,
and adds new ones straight to the calendar.

## How a run works

1. Search + fetch each source in `sources.md` for events in the next ~3 weeks.
2. Filter to Scottsdale/Tempe business networking events (mixers, breakfasts,
   ribbon cuttings, leads groups, young professional/industry meetups) —
   skip pure social, non-business, or outside-the-area results. Prioritize
   events likely to draw Jaden's target audience (local business
   owners/decision-makers) when the list is long.
3. Check `jaden@addrivesolutions.com` and skip anything already on the
   calendar (including recurring series already added).
4. Add new qualifying events directly to the calendar — **no approval step**
   — with the source link and a one-line relevance note in the description.
5. Send a short summary of what was added, plus anything skipped because the
   date/venue couldn't be confirmed (see the known-limitation note in
   `sources.md`).

## Changing behavior

- Add/remove sources: just tell Claude a site/Meetup group/social handle to
  track, or edit `sources.md` directly. The routine re-reads it every run.
- Switch back to review-before-adding, change cadence/day/time, or change
  the target calendar/lookahead window: ask Claude to update the Routine
  (`AZ Networking Events Scan`), or use the trigger tools directly.
