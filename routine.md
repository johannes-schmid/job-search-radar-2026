# Live Routine Definition

- **Trigger ID**: `trig_01WCcAfVhohppFRXxSoNDhRV`
- **Name**: Weekly Job Radar — Monday
- **Schedule**: `0 6 * * 1` (06:00 UTC every Monday → ~08:00 Europe/Madrid in
  summer, ~07:00 in winter, since cron runs in UTC and doesn't shift for DST)
- **Binding**: fires into the Claude Code session it was created from (so it
  inherits that session's Gmail/Google Drive/web-search access without
  needing separate connector grants on the trigger itself)

## Prompt sent on each firing

```
Weekly job-search digest time. Run this now, end-to-end, without asking questions:

CANDIDATE PROFILE
- Johannes Schmid, Senior Product Manager, 8+ years B2B/B2C SaaS. Based in Barcelona, Spain.
- Contact: schmid.johannes90@gmail.com
- Target roles: Senior Product Manager, Principal Product Manager, Head of Product, PM - AI/Platform/Growth.
- Target locations (priority order): Remote (global/int'l), Barcelona, Stockholm, Munich, Amsterdam, New Zealand (Auckland/Wellington), Canada (Toronto/Vancouver), Sydney, Bangkok, Singapore.
- Strong preference for AI product management roles - multi-agent orchestration, LLM evals, RAG, agentic AI. Built a production multi-agent LLM platform at Settly (relocation tech): ~30% of host messages AI-drafted, 20-30% manual-effort reduction, full eval/annotation infrastructure. Also drove 80% revenue growth via a 2-year product vision at Rentman, 40% revenue increase via pricing/licensing overhaul, 50% faster vendor response / +40% retention.
- Sector priority: Health Tech (wearables, digital health, longevity) > Climate/Energy Tech (B.Eng. Energy Systems) > AI-native SaaS > other.
- Watchlist companies (star these if seen): WHOOP, Oura, Polar, Garmin, Hinge Health, Kaia Health, Ada Health, Humanoo, Enpal, sonnen, Tibber, Baywa r.e., Sympower, Vandebron, Voltaware, Climeworks, Personio, Factorial HR, Leapsome, Greenhouse, Miro, Typeform, Contentful.
- Non-negotiables: remote or hybrid flexibility, no pure early-stage (<Series A) startups. Pension/retirement benefits and parental-leave policy are a strong plus (baby on the way).
- Languages: German (native), English (fluent), Dutch (fluent), Spanish (working).
- Certifications: PSPO I, PSM, Certified AI Product Manager, AI Evals for Engineers & PMs (Maven), Agentic AI Applications (Maven), RAG (DeepLearning.AI).

STEPS:

1. JOB SEARCH: Use WebSearch (and WebFetch to open promising listings) to find currently-open roles matching the target roles above, across the target locations and remote. Run multiple targeted searches, e.g. "Senior Product Manager remote [current month/year]", "AI Product Manager remote", "Principal Product Manager Barcelona", "Product Manager Stockholm/Munich/Amsterdam/Singapore/Sydney/Toronto/Bangkok/Auckland", "Head of Product health tech remote", "Product Manager climate tech energy remote". Aim for 15-25 unique, currently-live listings. For each, capture: title, company, location/remote policy, salary if listed, source URL, 1-line company description.

2. SCORE each job 0-100% fit, weighing: seniority match, AI/PM specialization overlap, location/remote match, sector match, company stage (favor Series B+/established over early-stage), watchlist-company bonus. Mark AI/ML product roles with an "AI PM" badge. Mark watchlist companies with a star. Sort by fit score descending.

3. EMAIL DIGGING: Use Gmail search_threads with a query like "(from:linkedin.com OR from:indeed.com OR subject:\"job alert\" OR subject:application OR subject:assessment) newer_than:8d" to find the last week's job-related emails. Read relevant ones with get_message. Summarize into a short "Needs Your Attention" list: pending assessments/deadlines, recruiter replies awaiting response, new inbound recruiter messages, notably strong LinkedIn alert listings. Do not reply/label/modify anything - just summarize.

4. CAREER COACH CORNER: Use WebSearch to find 2-4 recent (last ~4-6 weeks) articles/podcasts/reports on where product management (esp. AI-native PM) is heading. Summarize takeaways in 3-5 bullets. Suggest 2-3 specific, currently-available courses/certifications (Maven, Reforge, DeepLearning.AI, Product School, etc.) for the NEXT level beyond his existing Certified AI Product Manager / Maven AI Evals / Agentic AI Applications certs - not repeats.

5. COMPOSE one self-contained HTML email (inline CSS only, no external assets/CDNs): header with today's date + summary line (X jobs found, avg fit, top match); ranked job cards (title, company, location, color-coded fit % badge — green >=70/yellow 40-69/red <40, AI PM star, watchlist star, salary if known, link); "Needs Your Attention" section; "Career Coach Corner" section. Clean and scannable.

6. SEND via Gmail send_message to schmid.johannes90@gmail.com, subject "Job Radar - [date] - X new matches", HTML body. Always actually send the email - that's the deliverable, even if some sections turn up thin.
```

## Known limitations / follow-ups

- Web search doesn't cover the Asia-Pacific/Americas locations as deeply as
  Europe yet — early runs should be checked for whether those regions are
  actually turning up results, and the query list in the prompt tuned if not.
- If the session this is bound to is ever deleted, the routine breaks
  silently (fires into a session that no longer exists). Worth an occasional
  check that Monday emails are still arriving.
- A same-day test run (see `sample-report.html` in this repo, if present)
  validated the full pipeline end-to-end on 2026-09-18.
