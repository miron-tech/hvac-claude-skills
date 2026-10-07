# HVAC Contractor Claude Skills, by RankGrid

## What This Is
5 AI skills that turn Claude Code into your HVAC sales assistant — researching leads in seconds, building 3-tier estimates, coaching your follow-up, ranking your pipeline, and automating review collection.

## Data Sources

| Connection | What It Does | Required? |
|------------|-------------|-----------|
| **Perplexity** | Looks up property data, energy costs, rebates, equipment pricing, and market info | Recommended |
| **Firecrawl** | Pulls property details from Redfin and Zillow (sqft, year built, home value) | Recommended |

## How To Use
1. Clone this repo into your project directory (see README for setup)
2. Connect Perplexity and Firecrawl for live data (see README)
3. Tell Claude what you need — it picks the right skill automatically
4. Or be specific: "Run lead recon on 3847 Oakwood Dr, Memphis TN 38128"

## Available Skills

| Skill | Use When |
|-------|----------|
| **Lead Recon** | A lead comes in and you need to respond fast — property data, system age estimate, speed response |
| **Quote Builder** | You need a 3-tier estimate with rebates, financing, and energy savings |
| **Sales Coach** | An estimate went unsold and you need to know what to say next |
| **Job Stacker** | You have multiple estimates and need to know which ones to focus on this week |
| **Review Engine** | A job is done and you need to get a 5-star review + respond to existing reviews |

## How Claude Picks the Right Skill

```
Lead comes in (new customer, address, phone call) → Lead Recon
Need to build an estimate (replacement, repair, maintenance) → Quote Builder
Estimate went unsold or customer stopped responding → Sales Coach
Multiple leads/estimates and need to prioritize → Job Stacker
Job is done, need a review request → Review Engine
```

## How the Skills Work Together

Each skill passes information to the next one, so you don't repeat yourself:

```
Lead comes in → Lead Recon (research + speed response)
                    ↓
             Quote Builder (Good/Better/Best estimate)
                    ↓
              Sales Coach (follow-up on unsold estimates)
                    ↓
              Job Stacker (weekly pipeline priority)
                    ↓
             Review Engine (post-job review request)
```

| What You're Doing | What to Tell Claude |
|-------------------|-------------------|
| New lead comes in | "Run lead recon on [address]" |
| Need an estimate | "Build an estimate for this lead" |
| Estimate went cold | "Coach me on this unsold estimate" |
| Weekly planning | "Stack my jobs for this week" |
| Job finished | "Generate a review request for [customer]" |

## Time Savings

| Task | Before | After | Time Back |
|------|--------|-------|-----------|
| Research a lead | 15-20 min | 60 seconds | ~18 min |
| Build a 3-tier estimate | 30-45 min | 5 min | ~35 min |
| Figure out what to say on a cold estimate | 10-15 min | 2 min | ~12 min |
| Weekly pipeline review | 1-2 hours | 10 min | ~80 min |
| Review request + response | 5-10 min per job | 1 min | ~7 min/job |

At 5 leads/day and 3 completed jobs/day: **2-3 hours back every day.**

## Marketing Campaign: HVAC Speed Selling Playbook

A complete lead magnet funnel to acquire HVAC contractors as clients. All assets live in `campaigns/hvac-speed-selling/`.

### Funnel Flow
```
Facebook Ad / Social Post / SEO
        ↓
Landing Page (lead magnet opt-in + hero background video)
        ↓
7-Email Nurture Sequence (Days 0-10)
        ↓
Book a call → done-for-you setup
```

### Assets

| Asset | File |
|-------|------|
| Lead Magnet (8-page playbook) | `campaigns/hvac-speed-selling/lead-magnet.md` |
| Landing Page (HTML, background hero video) | `campaigns/hvac-speed-selling/landing-page.html` |
| Email 1 — Delivery (immediate) | `campaigns/hvac-speed-selling/emails/01-delivery.md` |
| Email 2 — Story (Day 1) | `campaigns/hvac-speed-selling/emails/02-the-story.md` |
| Email 3 — Problem (Day 2) | `campaigns/hvac-speed-selling/emails/03-the-problem.md` |
| Email 4 — Proof (Day 4) | `campaigns/hvac-speed-selling/emails/04-the-proof.md` |
| Email 5 — Objection (Day 6) | `campaigns/hvac-speed-selling/emails/05-the-objection.md` |
| Email 6 — Nudge (Day 8) | `campaigns/hvac-speed-selling/emails/06-the-nudge.md` |
| Email 7 — Breakup (Day 10) | `campaigns/hvac-speed-selling/emails/07-the-breakup.md` |
| Social Hooks (5 variations) | `campaigns/hvac-speed-selling/social/promotion-hooks.md` |
| Facebook Ads (3 variations) | `campaigns/hvac-speed-selling/ads/facebook-ads.md` |
| Campaign Brief | `campaigns/hvac-speed-selling/campaign-brief.md` |

### Hero Video
- YouTube: https://youtu.be/xYHaAvDzwVY
- Implementation: Background video (autoplay, muted, looped) on desktop, gradient fallback on mobile
- Matches wholesaler funnel pattern from `claude skills for wholesalers/landing-page.html`

### Go-Live Checklist
- [ ] Replace `YOUR_WEBHOOK_URL` in landing-page.html
- [ ] Upload landing page to your site or funnel builder
- [ ] Build 7-email automation workflow in your email platform
- [ ] Create Canva ad graphics
- [ ] Launch Facebook test ads ($20-30/day)
- [ ] Post first social hook

## Built by RankGrid
Built by [RankGrid](https://rankgrid.ai). We build lead websites that rank and get contractors found on Google and AI search. Want this connected to a CRM with automated follow-up? That's what the RankGrid platform does: https://rankgrid.ai
