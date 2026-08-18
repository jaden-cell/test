# Sources

Target area: Scottsdale, AZ and Tempe, AZ (business networking events only).
Lookahead window per run: next ~21 days.

## Who this is for

Jaden runs a local ad agency based in Tempe, targeting local/small Scottsdale
and Tempe businesses. Events that put him in a room with local business
owners and decision-makers (chamber mixers, small-business/entrepreneur
networking, referral/leads groups, young professional councils) are higher
value than generic community events — prioritize those when the list is long.

## Adding new sources

Just tell Claude a site, Meetup group, or social handle to track and it'll
get added below — no need to edit this file by hand. The weekly routine
re-reads this file from the repo each run, so new sources are picked up
automatically on the next Monday scan.

## Chambers of Commerce

- **Scottsdale Area Chamber of Commerce**
  - Events: https://business.scottsdalechamber.com/events/calendar
  - Also check: https://scottsdalechamber.chambermaster.com/events/
  - Known recurring: PM Connect (1st Wed, 5-7pm), AM Connect (3rd Thu, 7:30-9am)
- **Tempe Chamber of Commerce**
  - Events: https://business.tempechamber.org/calendar
  - Also: https://business.tempechamber.org/memberevents
  - Known recurring: Networking @ Noon (monthly), Business After Hours Mixer
- **Greater Phoenix Chamber**
  - Events: https://www.phoenixchamber.com/events/ (filter for Scottsdale/Tempe-area listings)

## Other business networking groups

- **BNI Arizona** (leads groups w/ Scottsdale/Tempe chapters) — https://bniaz.com/events/
- **Meetup.com** — search "business networking Scottsdale AZ" and "business networking Tempe AZ"
- **ASU SkySong** (Scottsdale innovation center, hosts startup/business events) — https://skysong.asu.edu/events
- **Tempe/Scottsdale Young Professionals or industry-specific groups** — search each run,
  since these rotate (chamber "young professionals council" pages, local Rotary/Kiwanis
  business mixers, coworking-space hosted events e.g. WeWork/Galvanize Phoenix)
- **Eliances @ MAC6 Conscious Workspace** (1430 W Broadway Rd #201, Tempe) — recurring
  entrepreneur/startup/investor networking series, strong ICP fit (startup founders =
  ad agency prospects), found via Eventbrite listing "Tempe AZ Business Networking Event
  & Beyond for Entrepreneurs & Startups." Eventbrite itself is unreachable (see limitation
  below), so confirm specific dates via web search snippets only.

## Notes for the agent

- Facebook and LinkedIn event pages should be checked via web search snippets only
  (do not attempt login-gated scraping) — treat as a supplementary source, not primary.
- Prefer events explicitly labeled networking/mixer/chamber/leads-group/breakfast over
  generic community events.
- Always include the source URL in the calendar event description for verification.
- **Known limitation, corrected 2026-08-17 (was misdiagnosed 2026-07-23 /
  2026-08-10 as per-site bot protection):** this environment's network policy
  blocks direct page fetches (WebFetch and even raw curl) to essentially all
  general websites — chambers, BNI, Eventbrite, AllEvents.in, Meetup, 1 Million
  Cups, SCORE, Local First AZ, Downtown Tempe Authority, city .gov sites,
  LinkedIn, Facebook, even example.com all fail at the network layer, not the
  site layer. Only a narrow dev-tooling allowlist works directly (github.com,
  npm/pypi registries, anthropic.com). This is a property of the Claude Code
  Remote *environment's* network access setting (chosen when the environment
  was created — see
  https://code.claude.com/docs/en/claude-code-on-the-web), not something a
  "more crawlable" source will fix. **WebSearch still works** (it doesn't go
  through this proxy) and is the only reliable discovery method under the
  current environment settings — rely on search snippets and known
  recurrence patterns, flag uncertain dates/venues rather than inventing
  them, and note anything unconfirmed in the run summary. If Jaden wants true
  live page crawling, the fix is changing this environment's network access
  policy to a more permissive setting, not swapping sources.
