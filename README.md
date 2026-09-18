# Job Search Radar

Automated weekly job-search digest for Johannes Schmid — Senior Product Manager,
Barcelona, targeting Senior/Principal PM and AI Product Manager roles.

This project is **not a code pipeline** — it's a scheduled Claude Code Routine
that runs live, every Monday, inside a Claude Code session that already holds
Gmail and Google Drive access. This repo just documents what it does and why,
so the setup is reproducible and editable.

## What it does, every Monday ~08:00 Europe/Madrid

1. **Job search** — web search across target roles (Senior/Principal PM, Head
   of Product, AI/Platform/Growth PM) and target locations: Remote,
   Barcelona, Stockholm, Munich, Amsterdam, New Zealand, Canada, Sydney,
   Bangkok, Singapore.
2. **Scoring** — each role gets a 0–100% fit score (seniority, AI/PM overlap,
   location/remote match, sector match, company stage, watchlist bonus). See
   `profile.md` for the full rubric and candidate profile it scores against.
3. **Email digging** — searches Gmail for the last week's job alerts,
   recruiter messages, and pending application steps (read-only — no replies
   or label changes).
4. **Career Coach Corner** — recent commentary on where product management
   (especially AI-native PM) is heading, plus 2–3 concrete next-level
   courses/certifications.
5. **Delivery** — one self-contained HTML email sent to
   schmid.johannes90@gmail.com.

## Why no Apify / LinkedIn scraper

An earlier personal skill (`job-scout`) used Apify actors to scrape LinkedIn
and Indeed directly. This routine intentionally uses web search + the
account's own Gmail job alerts instead:

- No new API token/credential to manage per environment.
- Avoids automating scraping of LinkedIn/Indeed, which sits against their
  ToS — the Gmail alerts already deliver that data legitimately.

## Files

- `profile.md` — candidate profile, target locations/sectors, watchlist
  companies, and the scoring rubric the routine uses.
- `routine.md` — the exact prompt text the Monday routine runs, for editing
  or re-creating the trigger if it's ever lost.

## Changing the schedule or prompt

The routine is a Claude Code Routine (`trig_...`) bound to a specific Claude
Code session, not a cron job in this repo. To change it, ask Claude (in the
session it's bound to) to update the trigger, or edit `routine.md` here and
ask Claude to sync the change to the live trigger.
