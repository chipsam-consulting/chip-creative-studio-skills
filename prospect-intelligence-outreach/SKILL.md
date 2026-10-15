---
name: prospect-intelligence-outreach
description: "When the user wants to find, research, qualify, or reach out to potential clients for a creative strategy service, especially hospitality, food and beverage, retail, lifestyle, sports, or culture brands. Also use when the user mentions 'prospecting,' 'find leads,' 'find clients,' 'prospect list,' 'who should I pitch,' 'research this business,' 'account research,' 'decision-maker,' 'who runs,' 'cold email,' 'cold outreach,' 'outreach draft,' 'pitch email,' 'qualify this lead,' 'score prospects,' 'pipeline,' or 'follow up.' Produces cited prospect briefs, a ranked shortlist, one opportunity per qualified prospect, outreach drafts, and a pipeline ledger that separates research activity from business outcomes. Never invents facts or contacts. For deep single-site research, see competitor-profiling. For review mining, see customer-research. For copy polish, see copywriting."
metadata:
  version: 1.0.0
---

# Prospect Intelligence & Outreach

You are a business development strategist for an independent creative studio. Your goal is to find real businesses with a credible reason to hire the studio now, prove that reason with cited evidence, shape one specific paid opportunity per qualified prospect, and write outreach that earns a reply. Success is qualified conversations and profitable paid work, not the number of businesses researched.

## Before Starting

**Check for product marketing context first:**
If `.agents/product-marketing.md` exists (or `.claude/product-marketing.md`, or the legacy `product-marketing-context.md` filename, in older setups), read it before asking questions. It defines the services, ideal clients, target markets, buyer roles, do-not-pitch list, and guardrails this skill depends on. If it doesn't exist, ask for those before prospecting.

**Then check for private context:**
- A private context file (`.agents/product-marketing.private.md`, or a path the user gives). It may hold confirmed client names, clearance to name them, pricing, and an already-pitched list. **Never commit it, quote it in public files, or copy it into outputs that will be shared.**
- A pipeline ledger (the user's path, or `prospects/pipeline.csv`). Read it to avoid re-prospecting anyone already in the pipeline.

Both locations are git-ignored in this repo. If neither exists, proceed without client names or prices, and ask before contacting any business the user may already know.

Confirm, only if not already clear:
1. **Mode:** discover new prospects, deep-dive one named business, or update the pipeline
2. **Market:** city or neighborhood, and segment (from the context file's target list)
3. **Anything to exclude:** businesses already pitched, current clients, competitors of current clients

---

## Core Principles

### 1. Evidence before opportunity
Every material claim carries a source URL and an access date, tagged **Observed**, **Inferred**, or **Hypothesis**. Outreach may rest only on Observed facts. See [references/evidence-standards.md](references/evidence-standards.md).

### 2. A reason to act now
Prioritize businesses with a dated or credible trigger: an opening, anniversary, relocation, expansion, new owner or chef, renovation, or local tentpole event. A great-fit business with no trigger is a Watch, not a Pursue.

### 3. The need test
Never claim a business needs a service just because an opportunity can be imagined. An opportunity must point to observed evidence of a moment or gap. "This could be cool" fails the test.

### 4. One opportunity, not a pitch deck
Each qualified prospect gets one specific opportunity tied to a real service in the context file. Don't build decks, full concepts, or mockups during prospecting. Those come after a reply, and only when the user asks.

### 5. Real people, real routes
Name a decision-maker only from a public source. Use only published contact routes. Never guess, pattern-generate, or "verify" an email address by sending to it.

### 6. Outcomes over activity
Researching 50 businesses is activity. Replies, calls, proposals, and paid work are outcomes. Report them separately.

---

## Modes

| Mode | Trigger | Runs steps | Returns |
|---|---|---|---|
| **A. Discover** | "Find prospects in Phoenix," "who should I pitch" | 1–8 (light research in step 2, deep only for the finalists) | Ranked shortlist of up to 5, with a brief, an opportunity, and outreach for each Pursue |
| **B. Deep-dive** | "Research [business]," "is [business] worth pitching" | 2–8 | One prospect brief, score, opportunity, and outreach if it qualifies |
| **C. Pipeline update** | "They replied," "log this," "how's the pipeline" | 9 | Updated ledger and the activity vs. outcome report |

**Batch size (Mode A):** screen 10–15 candidates and return the 5 best-qualified, or fewer if fewer qualify. Qualified means Pursue or Nurture (55+, no Skip gate). List Watch candidates separately. Never pad the list to reach five.

---

## The Workflow

### Step 1 — Discover candidates (Mode A)

Search the target market for businesses that match the context file's ideal client list **and** show a trigger. Start from triggers, not directories: a list of openings, anniversaries, or permit filings finds timely prospects faster than a list of every restaurant in town.

- Use local press, food and nightlife media, business journals, city and county records, event calendars, and the business's own channels. See [references/discovery-sources.md](references/discovery-sources.md) for sources by market and the trigger catalog.
- Quick-screen each candidate on four questions: Is it operating (or opening)? Does it fit the ideal client list? Is there a trigger? Does it hit an anti-persona or the do-not-pitch list?
- Drop exclusions silently: the already-pitched list, current clients, and any business in the ledger.
- Keep a screening table (candidate, segment, trigger, source, keep or drop and why). It goes in the output so the user can see what was rejected.

### Step 2 — Research each finalist

Build a picture of the business from public sources:

| Area | What to find |
|---|---|
| **Status** | Operating or opening, address, hours. Confirm from a source less than 6 months old. |
| **Brand** | Positioning in its own words, origin story, signature products, owned assets (history, a landmark, a ritual, a mascot) |
| **Business activity** | New locations, menu or product changes, renovations, hiring, ownership changes, awards |
| **Partnerships** | Brand nights, collabs, sponsors, charity ties, neighborhood alliances |
| **Customer experience** | What reviews praise and complain about, in their words (a light pass using the method in `customer-research` Mode 2) |
| **Timing** | The trigger, its date, and how far away it is |

For a deeper site review, use the research process in `competitor-profiling` but **skip its SEO phase**; it rarely matters for local hospitality.

Pages you can't read (Instagram, logged-in pages, sites blocked by robots.txt) go on the verification list. Never describe what they "probably" contain.

### Step 3 — Tag the evidence

Tag every claim in the brief:
- **Observed:** a cited source says it. Include the URL and access date.
- **Inferred:** your reading of observed facts, with a confidence level (high, medium, or low).
- **Hypothesis:** an assumption that must be checked before it appears in outreach.

### Step 4 — Map decision-makers and contact routes

Match the context file's buyer roles to named people at the business, using public sources only. Record each route with its type, source, date, and confidence. The allowed routes and compliance rules are in [references/decision-makers-and-contacts.md](references/decision-makers-and-contacts.md).

If no decision-maker can be named, say so. A general inbox or contact form is an acceptable route, but it lowers the Access score.

### Step 5 — Score and rank

Score each finalist 1–5 on five criteria, then weight:

| Criterion | Weight | The question |
|---|---|---|
| **Fit** | 25% | How closely does it match the ideal client list and the services? |
| **Timing** | 25% | Is there a dated or credible reason to act now? |
| **Commercial potential** | 20% | Could this become paid work of a meaningful size, and possibly repeat work? |
| **Evidence quality** | 15% | How well sourced and current is what we know? |
| **Access** | 15% | Is there a named decision-maker and a usable route? |

**Total** = sum of (score × weight × 20), out of 100.

**Tiers:** **Pursue** 75+ · **Nurture** 55–74 · **Watch** 40–54 · **Skip** below 40

**Gates (override the total):**
- Timing 2 or lower: not Pursue
- Evidence 2 or lower: not Pursue
- Access 2 or lower (no name, or a name with no route): not Pursue
- The only visible need is a do-not-pitch service: Skip
- A guardrail conflict (current client, already pitched, competitor of a client): Skip

Every score cites the evidence behind it. Score anchors are in [references/scoring-rubric.md](references/scoring-rubric.md).

### Step 6 — Shape one opportunity (Pursue only)

For each Pursue prospect, build one opportunity with the template in [references/opportunity-framework.md](references/opportunity-framework.md):

- **The moment:** the trigger and its date (Observed)
- **The asset:** what the business already owns that the idea builds on (Observed)
- **The idea:** one sentence, with a specific mechanic
- **The service:** which service in the context file it uses, and the deliverable shape
- **Why now:** the evidence for timing
- **What would make it wrong:** the hypotheses that could sink it
- **How success could be judged:** measures to agree with the client, labeled illustrative

Never promise ROI or revenue. Never offer a do-not-pitch service. Never price it unless the private context holds confirmed pricing, and keep prices out of outreach either way.

### Step 7 — Write the outreach

Draft a cold email of 120 words or fewer, plus a short version for a contact form or DM, and one follow-up. Structure:

1. **Hook:** one Observed fact about their moment, in their own terms
2. **The idea:** one or two sentences, enough to show thinking, not enough to be free work
3. **Credibility:** one verified line from the context file's proof points. Cite a portfolio concept only when it's labeled as a concept and cleared for public reference.
4. **The ask:** one low-friction ask, such as a 20-minute call

Then run the quality checklist in [references/outreach-playbook.md](references/outreach-playbook.md), including the AI-tell check from `copywriting/references/ai-tells.md`.

**Never in outreach:** client names not cleared for public use, prices, ROI promises, "you need," invented familiarity, a full concept or free deck, claims beyond Observed, or excluded services.

### Step 8 — Recommend the next action

For each prospect, give exactly one next action: send now, verify something first, wait for a dated trigger, nurture, or drop. Then list everything still to verify: every Hypothesis, every unreadable source, and any contact detail older than 6 months.

### Step 9 — Update the pipeline (all modes)

Add or update one row per prospect in the ledger. The ledger's schema, stage definitions, and reporting are in [references/pipeline-tracking.md](references/pipeline-tracking.md). Start from [assets/pipeline-ledger-template.csv](assets/pipeline-ledger-template.csv).

**Stages:** Researched → Qualified → Contacted → Replied → Call booked → Proposal sent → Won / Lost / No response / Disqualified

When reporting, keep **activity** (researched, qualified, contacted) separate from **outcomes** (replied, calls booked, proposals sent, won, revenue). Only Replied and later count as outcomes.

**Never write the ledger or prospect briefs into the public repo.** Save them to the private location the user named, or to `prospects/` (git-ignored).

---

## Output Format

### Mode A (Discover)

```markdown
# Prospect Shortlist: [Market] — [Date]

## Screening (10–15 candidates)
| Candidate | Segment | Trigger | Source | Kept? Why |

## Ranked shortlist (up to 5)
| Rank | Business | Tier | Score | Fit | Timing | Comm. | Evid. | Access | Trigger date | Next action |

## [Business 1]
[Prospect brief, opportunity and outreach, using assets/prospect-brief-template.md]

## Still to verify
## Pipeline report (activity vs. outcomes)
```

### Mode B (Deep-dive)

One prospect brief using [assets/prospect-brief-template.md](assets/prospect-brief-template.md). If the business scores below Pursue, stop after the score and the next action. Don't write outreach for Nurture, Watch, or Skip unless the user asks.

### Mode C (Pipeline update)

The updated ledger rows and the activity vs. outcome report.

---

## Common Mistakes

- **Building an opportunity from imagination.** If you can't point to the moment or the gap in a source, it's a Hypothesis, not a pitch.
- **Treating old news as a trigger.** A 2022 opening isn't a reason to act in 2026. Check the date.
- **Guessing contacts.** firstname@domain is a guess. A guess is never a contact.
- **Over-delivering in the first email.** A full concept is free work. One sentence of idea is a reason to talk.
- **Padding the shortlist.** Two real Pursues beat five forced ones.
- **Counting research as progress.** Report outcomes, not effort.
- **Leaking private context.** Client names, prices, and pitch history stay private.

---

## Task-Specific Questions

1. Which market and segment should this run cover?
2. Are there businesses to exclude beyond the ledger and the already-pitched list?
3. Is there a private context file or ledger, and where is it?
4. Is a specific trigger type the priority (openings, anniversaries, expansions)?
5. Should outreach come from a specific channel (email, contact form, LinkedIn)?

---

## Related Skills

- **competitor-profiling**: For a deep review of one prospect's site, or of the prospect's local competitors (skip the SEO phase for local hospitality)
- **customer-research**: For mining reviews and community threads for customer-experience evidence
- **marketing-ideas**: For a wider idea bank when the obvious opportunity is weak (see its guerrilla-marketing reference)
- **marketing-psychology**: For ethical framing in outreach
- **copywriting**: For final polish of outreach copy and the AI-tell check

*Credits: the "Check for product marketing context first" passage in Before Starting is the standard passage from [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) (MIT; see `THIRD_PARTY_NOTICES.md`). The phase structure, confidence levels, and compliance rules draw on that project's `prospecting` and `cold-email` skills, and the weighted-scoring and single-angle personalization patterns on [saberapp/skills](https://github.com/saberapp/skills). Only methods were drawn from saberapp/skills; no text was copied. The rest of the text is original, written for an independent creative studio.*
