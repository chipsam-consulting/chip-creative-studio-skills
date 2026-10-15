# Pipeline Tracking

How to log prospects and report activity separately from outcomes.

**The ledger is private.** Store it outside the public repo (the user's chosen location) or in `prospects/`, which is git-ignored. Never commit it.

---

## Ledger Schema

One row per prospect. Start from [../assets/pipeline-ledger-template.csv](../assets/pipeline-ledger-template.csv).

| Column | Meaning |
|---|---|
| `prospect_id` | Short slug (for example, `lv-business-name`) |
| `business` | Business name |
| `market` | City |
| `segment` | From the context file's ideal client list |
| `trigger` | The reason to act now |
| `trigger_date` | Date of the trigger (YYYY-MM-DD or YYYY-MM) |
| `score` | Total out of 100 |
| `tier` | Pursue, Nurture, Watch, or Skip |
| `decision_maker` | Name and role, or "unnamed" |
| `contact_route` | Route type (published email, form, LinkedIn, warm intro) |
| `contact_source` | URL where the route was found |
| `stage` | See stages below |
| `stage_date` | Date the current stage began |
| `first_contact_date` | Date of the first outreach |
| `next_action` | One action |
| `next_action_date` | When |
| `outcome` | For closed rows: won, lost, no response, or disqualified, with the reason |
| `fee_won` | Fee for won work; leave blank otherwise. Private. |
| `brief_path` | Path to the private prospect brief |
| `notes` | Short notes |

---

## Stages

| Stage | Counts as | Enters when |
|---|---|---|
| Researched | Activity | A brief exists |
| Qualified | Activity | Scored Pursue (Nurture rows stay at Researched, with a `next_action_date`) |
| Contacted | Activity | First outreach sent by the user (only once the prospect is Ready to Contact) |
| Replied | **Outcome** | The prospect responded (any response except an automated reply) |
| Call booked | **Outcome** | A conversation is scheduled |
| Proposal sent | **Outcome** | A written scope or proposal went out |
| Won | **Outcome** | Signed or paid |
| Lost | Closed | Declined, chose someone else, or went quiet after a proposal |
| No response | Closed | No reply after the follow-up sequence |
| Disqualified | Closed | Opt-out, closed business, or a guardrail conflict found later |

Only the user moves a row to Contacted or later; the skill never sends anything.

---

## Reporting

Report two blocks, never merged:

```
## Activity (this period)
- Researched: N
- Qualified (Pursue): N
- Contacted: N

## Outcomes (this period)
- Replied: N  (reply rate = Replied ÷ Contacted)
- Calls booked: N
- Proposals sent: N
- Won: N  (fees won: private)
- Stage conversion: Contacted → Replied X% · Replied → Call Y% · Call → Proposal Z% · Proposal → Won W%
```

Add one line on what the numbers suggest (for example, "Replies come mostly from anniversary triggers; openings haven't converted yet"). With fewer than 10 contacts, say the sample is too small to draw conclusions.

---

## Hygiene

- Re-check contact routes older than 6 months before sending.
- Revisit Nurture rows on their `next_action_date`.
- Never re-prospect a Lost or Disqualified business without the user's say-so.
