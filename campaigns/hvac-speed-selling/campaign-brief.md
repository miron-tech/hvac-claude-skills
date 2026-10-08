# Campaign Brief — HVAC Speed Selling Playbook

**Campaign:** Lead magnet funnel for HVAC contractor acquisition
**Product:** RankGrid HVAC Claude Skills → done-for-you setup on the RankGrid platform
**Target:** HVAC owner-operators, 1-10 employees, running 5-15 calls/day
**Goal:** Lead magnet downloads → email nurture → booked calls with RankGrid

---

## Funnel Architecture (Brunson Value Ladder)

```
Facebook Ad / Social Post / SEO
        ↓
Landing Page (lead magnet opt-in)
        ↓
Email 1: Deliver playbook (immediate)
Email 2: Origin story — why I built this (Day 1)
Email 3: The $50K problem — speed kills (Day 2)
Email 4: The math — what the fixes are worth on 5 leads a day (Day 4)
Email 5: Objection — "will this work for me?" (Day 6)
Email 6: Revenue math nudge (Day 8)
Email 7: Breakup — "should I stop?" (Day 10)
        ↓
Book a call → done-for-you setup
```

---

## Assets Produced

| Asset | File | Status |
|-------|------|--------|
| Lead Magnet (8-page playbook) | `lead-magnet.md` | Done |
| Landing Page (HTML) | `landing-page.html` | Done |
| Email 1 — Delivery | `emails/01-delivery.md` | Done |
| Email 2 — Story | `emails/02-the-story.md` | Done |
| Email 3 — Problem | `emails/03-the-problem.md` | Done |
| Email 4 — Proof | `emails/04-the-proof.md` | Done |
| Email 5 — Objection | `emails/05-the-objection.md` | Done |
| Email 6 — Nudge | `emails/06-the-nudge.md` | Done |
| Email 7 — Breakup | `emails/07-the-breakup.md` | Done |
| Social Hooks (5 variations) | `social/promotion-hooks.md` | Done |
| Facebook Ads (3 variations) | `ads/facebook-ads.md` | Done |

---

## Advisory Board Input Applied

| Advisor | What They Influenced |
|---------|---------------------|
| **Alex Hormozi** | Value equation framing — dream outcome (2-3 hrs back/day), low effort (AI does it), fast time-to-result (works immediately). Revenue math on Page 6 of playbook. Offer positioning in emails 4-6. |
| **Russell Brunson** | Full value ladder architecture — free playbook → email nurture → call → done-for-you setup. Hook-Story-Offer in every email. Epiphany Bridge in Email 2 (origin story). |
| **Jeff Miller** | Ad creative strategy — stupid simple, product and price. Text-based Canva graphics. No biz-opi guarantees. Clear what-you-get messaging. Budget and targeting recommendations. |
| **Justin Welsh** | Content strategy — write for ONE person (HVAC owner-operator, 5-15 calls/day, losing jobs to slow follow-up). Document real use cases. Social hooks written as educational content, not sales pitches. |
| **Neil Patel** | ROI proof within 30 days. Data-driven messaging (9x conversion, 50% first-responder stat). Revenue math table in playbook. SEO-ready landing page structure. |

---

## Positioning Angle (Primary)

**"You're losing HVAC jobs because you're too slow — not because your price is wrong."**

This works because:
- Every HVAC contractor knows this is true (instant recognition)
- It reframes from "I need more leads" to "I need to catch the ones I have"
- It's provable with data (9x conversion rate, 50% first-responder stat)
- It naturally bridges to the RankGrid platform (speed response + automation)

---

## Segmentation Logic

| Trigger | Action |
|---------|--------|
| Downloaded playbook, opened 3+ emails | Tag: "Engaged — HVAC" |
| Clicked the booking link in email 4 or 6 | Move to Sales Follow-Up sequence |
| Replied to any email | Pull from automation → personal follow-up |
| Opened 0 of first 3 emails | Move to Re-Engagement at Day 14 |
| Replied "not now" to Email 7 | Tag: "HVAC — Not Now" → re-engage in 60 days |
| Replied "let's go" to Email 7 | Tag: "HVAC — Ready" → book call immediately |

---

## UTM Tracking

| Channel | URL |
|---------|-----|
| Facebook (organic) | `[landing-page-url]?utm_source=facebook&utm_medium=social&utm_content=organic-post` |
| Facebook (paid) | `[landing-page-url]?utm_source=facebook&utm_medium=paid&utm_content=ad-[variant]` |
| LinkedIn | `[landing-page-url]?utm_source=linkedin&utm_medium=social&utm_content=organic-post` |
| Nextdoor | `[landing-page-url]?utm_source=nextdoor&utm_medium=social&utm_content=organic-post` |
| Email nurture | `rankgrid.ai?utm_source=email&utm_medium=nurture&utm_content=email-[number]` |
| Lead magnet PDF | `rankgrid.ai?utm_source=lead-magnet&utm_medium=pdf&utm_content=speed-selling-playbook` |

---

## Next Steps

- [ ] Replace `YOUR_WEBHOOK_URL` in landing-page.html with your form webhook
- [ ] Upload landing page to your site or funnel builder
- [ ] Build 7-email automation workflow in your email platform with timing from email files
- [ ] Create Canva ad graphics (see creative direction in ads/facebook-ads.md)
- [ ] Set up Facebook ad campaign with test budget ($20-30/day)
- [ ] Post first social hook on Facebook
- [ ] Set up segmentation tags and branching logic in your email platform
