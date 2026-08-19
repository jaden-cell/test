# AZ Networking Event Agent

Finds business networking events (chamber mixers, breakfasts, leads groups, etc.)
in Scottsdale and Tempe, AZ, and adds them to Jaden's Google Calendar
(`jaden@addrivesolutions.com`, America/Phoenix). Jaden runs a local ad agency
in Tempe, so events are weighted toward ones likely to put him in front of
local small-business owners — see [`sources.md`](./sources.md) for the full
targeting notes.

This isn't a scraping codebase, and as of 2026-08-19 it isn't primarily a
web-search one either. This environment's network policy blocks direct page
fetches (WebFetch/curl) to nearly every external site — chambers, BNI,
Eventbrite, Meetup, even example.com — at the connection level, so live
page-crawling isn't currently possible (see `sources.md` for the full
diagnosis; this was originally misdiagnosed as per-site bot protection).
It runs as a **weekly Claude Routine** with two discovery channels instead:

## How a run works

1. **Web/search:** search (not fetch) each site source in `sources.md` for
   Scottsdale/Tempe business networking events in the next ~3 weeks, relying
   on search snippets and known recurrence patterns since pages can't be
   fetched directly.
2. **Email:** search Jaden's inbox for event-newsletter invites (Gmail
   access works fine — it doesn't go through the blocked network path) and
   pull date/time/cost/location straight from the plain-text body. This is
   the more reliable channel, and can include virtual/Greater-Phoenix-wide
   events, not just Scottsdale/Tempe, since the goal is exposure to local
   business owners generally. See `sources.md` for recommended newsletter
   signups, including following Eventbrite/Meetup organizers by email to
   sidestep the fact those sites can't be crawled directly.
3. Filter both channels to events likely to draw Jaden's target audience
   (local business owners/decision-makers) — skip pure social/non-business
   results — and check `jaden@addrivesolutions.com` to skip anything already
   on the calendar (including recurring series already added).
4. Add new qualifying events directly to the calendar — **no approval step**
   — with the source (URL, or which email/sender) and a one-line relevance
   note in the description.
5. Email a summary to jaden@addrivesolutions.com via Gmail `send_message`
   (falls back to a **draft** if send access or Gmail auth isn't available
   that run — connector access has flickered between runs), and post the
   same summary in-session.

## Changing behavior

- Add/remove sources: just tell Claude a site/Meetup group/social handle to
  track, or edit `sources.md` directly. The routine re-reads it every run.
- Switch back to review-before-adding, change cadence/day/time, or change
  the target calendar/lookahead window: ask Claude to update the Routine
  (`AZ Networking Events Scan`), or use the trigger tools directly.
