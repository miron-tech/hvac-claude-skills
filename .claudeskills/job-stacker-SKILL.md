---
name: job-stacker
description: "Weekly pipeline review — rank all open estimates and active leads by close probability so the contractor knows exactly who to call today and in what order. Scores deals with the HEAT system across 4 dimensions, classifies by job type, flags stale estimates and seasonal risks, and builds a day-by-day action plan. Uses Perplexity for seasonal demand context and local market conditions."
---

# Job Stacker / Pipeline Prioritizer Skill

> **Purpose:** Stop working 15 estimates equally. Stack-rank your pipeline so you spend this week on the 3 jobs most likely to close and pay you.

---

## PREREQUISITES
- **Perplexity MCP** — seasonal demand context, local market conditions (optional but recommended)

---

## WHAT THIS SKILL DOES

- Takes your entire pipeline (3, 10, or 50 leads/estimates) and ranks them by close probability
- Scores each job across 4 dimensions using the **HEAT Score** (0-20)
- Classifies into 4 priority buckets: **Emergency / Hot / Warm / Cold**
- Identifies your **TOP 3 jobs to close this week**
- Flags stale estimates, expiring quotes, seasonal risks, and pipeline problems
- Recommends the **ONE next action per job** that moves it forward
- Estimates **revenue at risk** from stale or expiring estimates
- Builds a **day-by-day action plan starting from TODAY**
- Calculates pipeline health metrics

## WHAT THIS SKILL DOES NOT DO

- Does not manage your pipeline for you (you update the data)
- Does not pull data from your CRM automatically
- Does not guarantee which jobs will close — it's a prioritization framework, not a crystal ball

---

## SKILL CHAIN INTEGRATION

Job Stacker is Skill #4 in the chain. If previous skills ran on a lead, USE THAT DATA.

| If This Skill Was Run | Data Available | How to Use It |
|-----------------------|---------------|---------------|
| Lead Recon | Property data, system age, lead classification | Pre-populates job details, uses lead bucket for scoring |
| Quote Builder | 3-tier estimate, rebates, financing, anchor tier | Use for job value scoring. Know which tier was presented. |
| Sales Coach | Customer type, follow-up history, objection status | Use for readiness scoring. Know where the conversation stands. |

```
IF Lead Recon was run → Use its lead classification for initial HEAT scoring
IF Quote Builder was run → Use the anchored tier for job value, know the pricing
IF Sales Coach was run → Use its customer type + follow-up status for readiness
IF no previous skills were run → Score with available data, note gaps
```

---

## INPUTS NEEDED

| Input | Required | Example |
|-------|----------|---------|
| Open estimates / leads | Yes | See format below |
| Your goal this month | Helpful | "Need to close $40K in revenue" or "Close 5 jobs" |
| Hours available this week | Helpful | "I can do 30 hours of sales this week" |
| Previous skill data | Helpful | "I already ran Quote Builder on Lead #1" |

**Job format (per job):**
```
Customer: Sarah M.
Address: 3847 Oakwood Dr, Memphis TN 38128
Job type: Replacement / Repair / Maintenance plan / Tune-up
Estimate: $9,200 (Better tier quoted)
Lead source: Google / LSA / Angi / Referral / Repeat customer
Urgency: System down / Aging / Shopping / Planning
Last contact: 3 days ago — "let me look it over"
Days in pipeline: 5
Notes: Getting 2 other quotes. Quote shopper.
```

Provide as much or as little as you have. More data = better ranking.

---

## FRAMEWORK: The HEAT Score

Each job gets a score from 0-20 across 4 dimensions (0-5 each).

### HOT (Urgency) — 0 to 5

| Urgency Signal | Score |
|---------------|-------|
| System is down / no heat / no AC / safety issue | 5 |
| System struggling, customer uncomfortable | 4 |
| System aging, customer actively getting quotes | 3 |
| Customer wants to replace "sometime" / exploring | 2 |
| Maintenance / tune-up only | 1 |
| Unknown urgency | 2 (neutral) |

### EQUITY (Job Value) — 0 to 5

| Estimated Revenue | Score |
|------------------|-------|
| $10,000+ replacement | 5 |
| $7,000-$9,999 replacement | 4 |
| $4,000-$6,999 replacement or major repair | 3 |
| $1,000-$3,999 repair | 2 |
| Under $1,000 (tune-up, minor repair, maintenance plan) | 1 |

### APPETITE (Customer Readiness) — 0 to 5

| Customer Signal | Score |
|----------------|-------|
| Verbal yes / ready to schedule / "let's do it" | 5 |
| Asking about financing, scheduling, or next steps | 4 |
| Engaged, asking good questions, responding quickly | 3 |
| Comparing quotes, slow responses, "thinking about it" | 2 |
| Cold lead, no engagement, "not now" | 1 |
| New lead, haven't spoken yet | 2 (neutral) |

### TIMING (Speed to Close) — 0 to 5

| Timeline | Score |
|----------|-------|
| Can close today / this weekend | 5 |
| Can close within 7 days | 4 |
| Can close within 14 days | 3 |
| 2-4 weeks | 2 |
| 30+ days or no clear timeline | 1 |

### HEAT Score Calculation

```
HEAT Score = HOT + EQUITY + APPETITE + TIMING
Maximum: 20 points
```

### Score → Priority Bucket

| HEAT Score | Bucket | Action |
|-----------|--------|--------|
| 16-20 | **EMERGENCY** | Drop everything. Close this today/tomorrow. |
| 11-15 | **HOT** | Daily attention. Active follow-up. |
| 6-10 | **WARM** | Scheduled follow-up. Weekly touchpoints. |
| 0-5 | **COLD** | Monthly drip or remove. Don't spend time here. |

---

## PIPELINE HEALTH FLAGS

After scoring all jobs, flag these conditions:

```
🔥 EMERGENCY:       System-down lead with no response from you in 4+ hours
⚠️ EXPIRING:        Estimate sent 14+ days ago with no follow-up
⚠️ STALE:           No contact in 7+ days on active lead
⚠️ SEASONAL RISK:   Heating estimate sent in spring (customer may wait until fall)
⚠️ QUOTE SHOPPER:   Customer mentioned getting other estimates
⚠️ NO FOLLOW-UP:    Estimate sent with zero follow-up touches
⚠️ MAINTENANCE OPP: Repair customer not pitched on maintenance plan
⚠️ TOP HEAVY:       Too many big replacements, not enough quick wins
⚠️ PIPELINE EMPTY:  Fewer than 5 active leads
⚠️ DEAD WEIGHT:     Multiple leads scoring 0-5 clogging the pipeline
⚠️ NO REVIEWS:      Completed jobs in last 30 days with no review request sent
💰 REVENUE AT RISK:  Total value of estimates going stale or expiring
```

---

## TOOL ROUTING

| Data Needed | Tool | Query |
|-------------|------|-------|
| Seasonal demand context | Perplexity | "Current HVAC demand in [city] [state] — is this peak season for AC or heating? Average wait times for installation appointments." |
| Local market competitiveness | Perplexity | "How competitive is the HVAC market in [city]? Average number of contractors, typical close rates, common pricing for [job type]." |
| Weather driving demand | Perplexity | "Current and 2-week weather forecast for [city] [state]. Any extreme heat or cold driving HVAC demand?" |

### Parallel Execution

**Batch 1 — Perplexity enrichment (if seasonal/market context needed):**
- One query for seasonal demand + weather context for the metro area

**Batch 2 — Score all jobs with available data**

**Batch 3 — Build ranked pipeline, flags, and weekly schedule**

---

## DECISION LOGIC

```
IF all jobs score under 6 →
  Pipeline is cold. Say it directly: "None of these are likely to close this week.
  Spend 80% of your time on lead generation — you need more at-bats."

IF 1-2 jobs score 16+ →
  These are the ONLY priority. Everything else can wait.

IF 3+ jobs score 11+ →
  Contractor needs to focus. Recommend top 3 only — the rest get scheduled follow-ups.

IF a job has been in pipeline 21+ days with no progress →
  Flag for one final re-engagement attempt or removal.

IF emergency lead has no response in 4+ hours →
  FLAG IMMEDIATELY. This lead is probably lost.

IF estimate sent with no follow-up →
  This is the #1 problem. Surface it prominently.

IF repair completed but no maintenance plan pitched →
  Lost recurring revenue. Flag it.

IF seasonal risk (heating estimate in spring, AC estimate in fall) →
  Note: "Customer may wait. Set a reminder for [season] to re-engage."

IF pipeline has fewer than 5 active jobs →
  "You need more leads. At a 40% close rate, 5 active estimates = 2 closed jobs.
  Below 5, you're gambling on every single one."

DEFAULT → Rank by HEAT score, present top 3, recommend one action per job.
```

---

## CONSTRAINTS

- [ ] Never rank more than 3 jobs as "top priority" — the whole point is focus
- [ ] Always include the ONE next action per job
- [ ] Flag jobs that should be dropped or moved to drip — contractors hold dead leads too long
- [ ] If a job is emergency (system down), it's always #1 regardless of score
- [ ] Present the full ranked list but make the top 3 visually obvious
- [ ] If data is missing, score it neutral (2-3) and note the gap
- [ ] Build the weekly schedule starting from TODAY — not a generic Monday
- [ ] Include total pipeline value and revenue at risk
- [ ] If pipeline has <5 jobs, lead gen warning must be prominent

---

## COMPLETE EXAMPLE

### Example Input:
> Goal: $40K in revenue this month. 30 hrs/week available for sales.
>
> 1. Sarah M — 3847 Oakwood Dr, Memphis 38128. Replacement estimate $9,200 (Better tier). Google lead. Quote shopper, getting 2 other quotes. Sent estimate 5 days ago. Last message: "let me look it over."
>
> 2. James R — 1205 Poplar Ave, Memphis 38104. Emergency — furnace died last night. Called this morning from Google LSA. Haven't responded yet. Probably $3,500-$8,000 depending on repair vs replace.
>
> 3. Linda W — 892 Kirby Pkwy, Memphis 38119. Referred by a neighbor. 20-year-old system, wants to replace before summer. Came in 3 days ago. Quoted $12,500 (Best tier). She said "this looks great, let me talk to my husband."
>
> 4. Tom D — 2510 Bartlett Blvd, Memphis 38134. Tune-up request from Angi. Booked for next Tuesday. $149. System is 14 years old.
>
> 5. Maria G — 4200 Summer Ave, Memphis 38122. Called 2 weeks ago about AC making noise. Sent repair estimate for $1,200. No response since.

### Example Output:

---

## JOB STACK: Week of March 4, 2026 (Starting Tuesday)
**Goal:** $40K revenue this month | **Available:** 30 hrs/week

---

### RANKED PIPELINE

| Rank | Customer | HEAT | H | E | A | T | Job | Bucket |
|------|----------|------|---|---|---|---|-----|--------|
| **1** | **James R (Poplar Ave)** | **18** | 5 | 4 | 4 | 5 | Emergency → Repair or Replace | **EMERGENCY** |
| **2** | **Linda W (Kirby Pkwy)** | **15** | 3 | 5 | 4 | 3 | Replacement $12,500 | **HOT** |
| **3** | **Sarah M (Oakwood Dr)** | **12** | 4 | 4 | 2 | 2 | Replacement $9,200 | **HOT** |
| 4 | Tom D (Bartlett Blvd) | 7 | 1 | 1 | 3 | 4 | Tune-up $149 | WARM |
| 5 | Maria G (Summer Ave) | 4 | 2 | 2 | 0 | 0 | Repair $1,200 | COLD |

---

### YOUR TOP 3 THIS WEEK

---

**#1 — James R, 1205 Poplar Ave (HEAT: 18/20) — EMERGENCY**
**Furnace died last night. Called this morning from Google LSA. You haven't responded yet.**

⚠️ **RESPOND RIGHT NOW.** He called from Google LSA — he's calling 3-5 contractors simultaneously. Every minute counts. The first contractor to respond professionally and show up today gets the job.

**The numbers:**
- Repair: $800-$3,500 depending on what failed
- If furnace is 15+ years old: replacement $5,500-$8,500
- Emergency call = highest close probability in your pipeline

**ONE ACTION:** Call him back in the next 10 minutes. Not text — call. "Hi James, this is [Name] with [Company]. Got your message about the furnace. I can have someone there [today/this afternoon]. What's the address situation — anyone home right now?"

**Revenue:** $3,500-$8,500 | **Close probability:** 85%+ if you respond within the hour

---

**#2 — Linda W, 892 Kirby Pkwy (HEAT: 15/20) — HOT**
**Referred by neighbor. $12,500 Best tier. "Let me talk to my husband." 3 days ago.**

This is your highest-revenue job and she's almost ready. Referral customers close at the highest rate. "Let me talk to my husband" is not a rejection — it's a process step.

**ONE ACTION:** Text today: "Hey Linda — I put together a quick one-page summary with the three options and financing math so you and your husband can look at it together. Want me to send that over? Also happy to answer any questions he has directly."

**Revenue:** $12,500 | **Close probability:** 65-75% | **Time-to-close:** 3-7 more days

---

**#3 — Sarah M, 3847 Oakwood Dr (HEAT: 12/20) — HOT**
**Quote shopper, $9,200 Better tier, 5 days since estimate, comparing other quotes.**

She's in the decision window. Day 5 is still alive — most quote shoppers decide in 5-14 days. Your next message needs to add value, not just check in.

**ONE ACTION:** Text today: "Hey Sarah — one thing worth looking at: the $850/year in energy savings on your system, plus any utility rebates you qualify for. Those change the real cost picture. Happy to compare your quotes side-by-side if that's helpful."

**Revenue:** $9,200 | **Close probability:** 40-50% | **Time-to-close:** 5-10 more days

---

### OTHER JOBS

**Tom D — Bartlett Blvd (HEAT: 7) — WARM**
Tune-up booked for Tuesday. $149. Low revenue but **high upsell opportunity** — system is 14 years old. This is a maintenance plan pitch AND a replacement seed conversation.

**Action:** During Tuesday tune-up, tech should assess system condition and pitch maintenance plan ($199/year). If system shows wear, plant the replacement seed: "Your system has a few more years in it, but I want to be upfront — at 14 years, the efficiency is down and repairs start coming more often. When you're ready to look at options, the rebates right now are really good."

**Maria G — Summer Ave (HEAT: 4) — COLD**
⚠️ **STALE — 14 days, no response to repair estimate.**

**Action:** One final text: "Hey Maria — just wanted to check in on the AC noise. Still happening? I can still get you on the schedule this week if you need it." If no response in 5 days, move to monthly drip.

---

### PIPELINE HEALTH

| Metric | Status |
|--------|--------|
| Active jobs (HEAT 11+) | 3 — solid |
| Pipeline value | $25,050 (replacements) + $1,349 (repairs/tune-ups) = **$26,399** |
| Revenue at risk | $1,200 (Maria G — going stale) |
| 🔥 **EMERGENCY** | James R — furnace down, NO RESPONSE YET |
| ⚠️ STALE | Maria G — 14 days no contact |
| ⚠️ QUOTE SHOPPER | Sarah M — comparing 3 quotes |
| ⚠️ MAINTENANCE OPP | Tom D — 14yr system, no plan pitched yet |
| ⚠️ NO FOLLOW-UP | Maria G — estimate sent, zero follow-up |
| Monthly goal progress | $0 closed / $40K target — need James + Linda + Sarah to hit goal |
| Pipeline depth | 5 active leads — minimum acceptable. Add 3-5 more leads this week. |

---

### THIS WEEK'S SCHEDULE (Starting Tuesday March 4)

| Day | Job | Action | Est. Time |
|-----|-----|--------|-----------|
| **Tue AM** | #1 James R | CALL NOW. Schedule same-day visit. | 15 min |
| **Tue AM** | #2 Linda W | Text one-page summary for husband review | 10 min |
| **Tue** | Tom D | Tune-up appointment. Tech pitches maintenance plan + replacement seed. | 1.5 hrs (on-site) |
| **Tue PM** | #3 Sarah M | Send value-add text (rebates + energy savings) | 5 min |
| **Tue PM** | Maria G | Final re-engagement text | 5 min |
| **Wed** | #1 James R | Service call (if booked). Diagnose → repair or replacement conversation. | 2-3 hrs |
| **Wed** | #2 Linda W | Follow up if she sent the summary to husband | 10 min |
| **Thu** | #1 James R | If replacement needed: run Quote Builder, present estimate | 1 hr |
| **Thu** | #3 Sarah M | If no response to Tue text: call her (Touch 4 in cadence) | 15 min |
| **Fri** | #2 Linda W | Check in — "Did you two get a chance to look it over?" | 10 min |
| **Fri** | Pipeline | Review all 5 jobs. Update status. Re-stack for next week. | 30 min |
| | | **Total: ~6-7 hrs sales + 1.5 hrs on-site service** | |
| | | **Remaining: 22+ hrs for lead generation, service calls, and admin** | |

---

## OUTPUT FORMAT

Deliver pipeline analysis as:
1. **Ranked pipeline table** — all jobs with HEAT scores + bucket
2. **Top 3 deep dive** — numbers, close probability, and ONE action per job
3. **Other jobs** — brief status + action for non-priority jobs
4. **Pipeline health** — all applicable flags + metrics + revenue at risk
5. **Weekly schedule** — day-by-day action plan starting from TODAY

---

## WITH THE RANKGRID PLATFORM

> This skill works standalone — paste your pipeline and get a ranked action plan. But if you're running the RankGrid platform, your pipeline loads automatically. Just say "stack my jobs" and it reads live data — open estimates, lead sources, last contact dates, follow-up status — all without typing a thing. Pipeline health flags update in real time.
>
> Want this connected to a CRM with automated follow-up? That's what the RankGrid platform does: https://rankgrid.ai

---

## QUALITY CHECKLIST

Before delivering, verify:
- [ ] Are HEAT scores calculated correctly across all 4 dimensions?
- [ ] Are the top 3 clearly identified with specific next actions?
- [ ] Is each action specific enough to execute? (Not "follow up" — WHO, WHAT, HOW)
- [ ] Are stale/expiring/emergency flags prominently displayed?
- [ ] Is there a revenue at risk calculation?
- [ ] If pipeline has <5 jobs, is the lead gen warning prominent?
- [ ] Does the weekly schedule start from TODAY?
- [ ] Is the schedule realistic for the contractor's available hours?
- [ ] Are maintenance plan opportunities flagged?
- [ ] Are dead leads honestly identified?
- [ ] If previous skills were run on any job, is that data being used?
- [ ] Would a contractor open this and immediately know what to do today?

---

## KNOWN LIMITATIONS

| Limitation | Workaround |
|-----------|------------|
| Can't auto-pull pipeline from CRM | User provides jobs manually |
| Seasonal context requires Perplexity | Without it, use general seasonal knowledge (summer = AC peak, winter = heating peak) |
| Close probability is estimated | Based on customer type patterns, not individual prediction |
| Schedule assumes weekday work | Adjust if contractor says otherwise (many HVAC contractors work Saturdays) |
| Can't track if follow-ups were actually sent | Contractor needs to confirm what they've done. The RankGrid platform tracks this. |
