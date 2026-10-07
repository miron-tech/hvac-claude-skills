---
name: quote-builder
description: "Build professional Good/Better/Best HVAC estimates with rebates, financing, energy savings, and lifetime cost of ownership. Use when a contractor needs to create a multi-tier estimate for a replacement, repair, or maintenance plan. Includes Hormozi Value Equation framing, Cost of Waiting calculator, and common estimating error flags. Uses Perplexity for current equipment pricing, rebate programs, and local energy costs."
---

# Quote Builder Skill

> **Purpose:** Help contractors build estimates that close — not just list prices. Good / Better / Best with rebates, financing math, energy savings, and a lifetime cost frame that turns a $12K expense into a $33/month investment that pays for itself.

---

## PREREQUISITE
- **Perplexity MCP** — current equipment pricing, rebate programs, local energy costs, financing rates

---

## WHAT THIS SKILL DOES

- Takes property data (from Lead Recon or manual input) + job type
- Generates **3-tier pricing** (Good / Better / Best) with specific equipment recommendations
- Calculates applicable **rebates** (utility rebates, state programs, manufacturer rebates)
- Adds **financing options** (monthly payment at different terms)
- Includes **energy savings comparison** (old system vs new, annual savings estimate)
- Calculates **lifetime cost of ownership** — total cost over 15-20 years including energy + maintenance
- Calculates **Cost of Waiting** — what the homeowner loses every month they delay
- Flags common **estimating errors** (SEER vs SEER2, oversizing, missing ductwork mods, wrong rebate eligibility)
- Recommends the **anchor tier** (which option to present first based on customer type)

## WHAT THIS SKILL DOES NOT DO

- Does not replace a proper Manual J load calculation for complex homes
- Does not guarantee pricing — equipment costs vary by supplier and region
- Does not generate a formatted PDF proposal (that's the contractor's proposal software)
- Does not account for custom ductwork situations without on-site assessment

---

## INPUTS NEEDED

| Input | Required | Example |
|-------|----------|---------|
| Job type | Yes | "replacement," "repair," "maintenance plan," "emergency repair" |
| Property sqft | Yes | "1,850 sqft" |
| Location (city, state, ZIP) | Yes | "Memphis, TN 38128" |
| Current system info | Helpful | "15-year-old 3.5 ton AC, gas furnace, SEER 13" |
| Customer situation | Helpful | "System died, needs replacement fast" or "Getting quotes, not urgent" |
| Budget signals | Helpful | "Price-sensitive," "wants the best," "asked about financing" |
| Lead Recon data | Helpful | Home value, system age estimate, rebate info |

---

## GOAL

- Primary: Give the contractor a professional 3-tier estimate that closes at higher rates
- Secondary: Make sure no rebate money is left on the table (40-60% of rebate apps get rejected — help avoid errors)
- Tertiary: Frame the purchase as an investment, not an expense — using lifetime cost and energy savings

---

## THE VALUE EQUATION (Hormozi Framework)

Every estimate should maximize this equation:

```
VALUE = (Dream Outcome × Perceived Likelihood) / (Time Delay × Effort)
```

**Dream Outcome:** "Your energy bill drops $120/month. Your home stays 72 degrees all summer. No more emergency calls at 2 AM."

**Perceived Likelihood:** "Here are 3 homeowners nearby who installed the same unit." "This system comes with a 10-year parts warranty." "We've installed 200+ of these."

**Time Delay:** "Installed tomorrow. Cooling by dinner." "We handle permits, disposal, and rebate paperwork."

**Effort & Sacrifice:** "You don't lift a finger. We handle everything — old system removal, new install, permits, rebate filing, inspection."

**This means:** Don't just list prices. Frame every tier in terms of what the homeowner GETS, how LIKELY it is to work, how FAST they get it, and how LITTLE they have to do.

---

## FRAMEWORK: The 3-Tier Estimate Builder

### Step 1 — Determine System Requirements

**Tonnage (confirm or estimate):**
```
Hot climate (SE, SW, Gulf): 1 ton per 400-500 sqft
Moderate climate (Mid-Atlantic, Midwest): 1 ton per 500-600 sqft
Cold climate (NE, Upper Midwest): 1 ton per 600-700 sqft

Example: 1,850 sqft in Memphis → 3.5-4.5 tons → recommend 4-ton system
```

**System Type Decision:**
```
IF has gas furnace + AC → Quote AC replacement OR heat pump conversion
IF all-electric → Quote heat pump (qualify for higher rebates)
IF boiler/radiant → Quote AC + keep existing heat (unless converting)
IF customer says "I want a heat pump" → Quote heat pump + keep gas furnace as backup (dual fuel)
IF climate zone 1-3 (hot) → Heat pump is often most efficient, highest rebates
IF climate zone 5-7 (cold) → Dual fuel or gas furnace + AC (heat pump alone struggles below 0°F)
```

### Step 2 — Build 3 Tiers

| Tier | What It Is | Target Customer | Profit Margin |
|------|-----------|----------------|---------------|
| **Good** | Entry-level brand, standard efficiency (14-15 SEER2), builder-grade. Gets the job done. | Price-sensitive, "just need it to work" | 40-45% |
| **Better** | Mid-tier brand, higher efficiency (16-17 SEER2), better warranty, quieter. | Value-conscious, wants a good deal | 45-50% |
| **Best** | Premium brand, highest efficiency (18-21+ SEER2), variable speed, smart thermostat, longest warranty. | Wants the best, values comfort + savings | 50-60% |

**For each tier, include:**
1. Equipment (brand, model series, SEER2 rating, tonnage)
2. Installation (labor, permits, disposal of old system)
3. Total price before rebates
4. Applicable rebates (itemized)
5. Net price after rebates
6. Financing option (monthly payment at 2-3 term lengths)
7. Estimated annual energy savings vs current system
8. Lifetime cost of ownership (15 or 20 years: purchase + energy + maintenance)

### Step 3 — Calculate Rebates

**Federal Tax Credits:**
```
Do NOT quote a federal tax credit. The federal 25C energy efficient home
improvement credit (heat pumps, central AC, furnaces, heat pump water
heaters, insulation) ended for equipment placed in service after
December 31, 2025.

Tell the customer to check current federal, state and utility rebates:
their utility company and DSIRE (dsireusa.org). Tax questions go to
their tax preparer.
```

**Utility / State Rebates (use Perplexity to find current programs):**
```
perplexity_ask: "Current HVAC rebates and energy efficiency incentive programs
for homeowners in [city] [state] [zip] in 2026. Include utility company rebates,
state programs, and any special heat pump incentives. List specific dollar amounts
and eligibility requirements."

search_context_size: "high"
search_recency_filter: "month"
```

**Manufacturer Rebates:**
```
perplexity_ask: "Current manufacturer rebates for [brand] HVAC systems in 2026.
Any seasonal promotions, dealer incentives, or consumer rebates available?"

search_context_size: "medium"
```

**Common Rebate Errors to Flag:**
- Wrong SEER2 rating for the rebate tier (must meet MINIMUM, not just close)
- Missing AHRI certificate number (required for most rebates)
- Wrong system type (heat pump rebate claimed for AC-only install)
- Missing energy audit (some utility rebates require pre-install audit)
- Rebate expired between estimate and installation
- Contractor not on utility's approved installer list

### Step 4 — Calculate Financing

**Standard financing presentation:**
```
FOR EACH TIER:
  Monthly at 60 months (5 years)  — shows lowest number first
  Monthly at 120 months (10 years) — middle ground
  Monthly at 180 months (15 years) — lowest possible payment

USE current rates. If unknown, estimate:
  Same-as-cash (0%): 12-18 months typical
  Reduced rate: 4.99-7.99% for 60-120 months
  Extended: 9.99-11.99% for 120-240 months

ALWAYS show:
  "Your monthly payment: $XX"
  "Your monthly energy savings: $XX"
  "Net monthly cost: $XX" (payment minus savings)
```

**The magic number:** When net monthly cost is under $50 — or negative — the system "pays for itself." Lead with that.

### Step 5 — Lifetime Cost of Ownership

This is the frame that changes everything. Don't compare the $7K system to the $12K system. Compare what each costs over 15 years.

```
LIFETIME COST = Purchase Price - Rebates + (Annual Energy Cost × Years) + (Annual Maintenance × Years)

Example (Good tier):
  Purchase: $7,500 | Rebates: $600 | Net: $6,900
  Annual energy: $2,400 (SEER 15)
  Annual maintenance: $200
  15-year total: $6,900 + $36,000 + $3,000 = $45,900

Example (Best tier):
  Purchase: $12,000 | Rebates: $2,600 | Net: $9,400
  Annual energy: $1,600 (SEER 20)
  Annual maintenance: $150 (variable speed = less wear)
  15-year total: $9,400 + $24,000 + $2,250 = $35,650

DIFFERENCE: The "expensive" system saves $10,250 over 15 years.
```

### Step 6 — Cost of Waiting Calculator

For customers with aging systems who are delaying replacement:

```
MONTHLY COST OF WAITING:
  Extra energy cost: (Old system annual energy - New system annual energy) / 12
  Emergency repair risk: Average emergency repair ($800-$2,500) × probability/month
  Lost rebate risk: Current rebates may change/expire

Example:
  Old system (SEER 10): $3,200/year energy
  New system (SEER 18): $1,800/year energy
  Monthly overpayment: $117/month
  Emergency risk: ~$150/month (averaged over probability)
  Total cost of waiting: ~$267/month

  "Every month you wait, you're spending about $267 more than you need to.
   In 6 months, that's $1,600 — money that could've gone toward the new system."
```

---

## DECISION LOGIC

```
IF job_type = emergency_repair →
  Skip full 3-tier build. Provide repair estimate + "while we're here" replacement mention.
  "We can fix this for $[X]. But I want to be honest — your system is [age] years old.
   A repair today is a band-aid. Want me to show you what replacement options look like
   so you can compare?"

IF job_type = replacement + system_age > 15 →
  Lead with efficiency gains and rebates. Show lifetime cost.
  Anchor on Better tier (most contractors close here).

IF job_type = replacement + customer_says "too expensive" →
  Show financing breakdown first. Net monthly cost after energy savings.
  "The Better option is $33/month after energy savings. That's less than your
   streaming subscriptions."

IF job_type = replacement + customer mentioned "other quotes" →
  Focus on value differentiation, not price matching.
  Include warranty comparison table, rebate assistance, and installation quality markers.

IF job_type = maintenance_plan →
  Show annual cost vs emergency repair cost.
  Include: priority scheduling, parts discount, seasonal tune-ups, extended equipment life.
  "A maintenance plan is $199/year. The average emergency repair is $800-$2,500.
   Plus you jump the line in summer when everyone's AC breaks."

IF customer_type = referral →
  Anchor on Best tier. Referred customers have higher trust and close at higher rates.

IF customer_type = emergency →
  Anchor on Better tier. They need it now — don't oversell, but don't leave money on the table.

IF home_value > $400K →
  Anchor on Best tier. Budget is likely not the constraint — comfort and quality are.

IF home_value < $200K →
  Anchor on Good tier but always show all three. Many choose Better when they see the math.

DEFAULT → Anchor on Better tier. Present all three. Show lifetime cost comparison.
```

---

## ESTIMATING ERROR FLAGS

Before delivering, check for these common mistakes:

| Error | What to Flag |
|-------|-------------|
| **SEER vs SEER2** | As of Jan 2023, new standard. SEER2 ratings are ~5% lower than SEER. A SEER 16 system is roughly SEER2 15.2. Don't confuse them on rebate applications. |
| **Oversizing** | Bigger is NOT better. Oversized system short-cycles, creates humidity problems, and fails faster. Match tonnage to load, not "round up to be safe." |
| **Undersizing** | System runs constantly, can't keep up on peak days, and wears out faster. |
| **Missing ductwork mods** | New high-efficiency system on old undersized ductwork = terrible performance. Flag if home is pre-1990. |
| **R-410A vs R-454B** | R-410A phasedown is happening. New systems may use R-454B (A2L refrigerant). Check equipment availability. |
| **Electrical panel upgrade** | Heat pump conversion from gas may require 200A panel or new circuit. Add $1,500-$3,000 if needed. |
| **Permit costs** | Vary by city ($75-$500). Don't forget to include in estimate. |
| **Disposal fees** | Old system removal + refrigerant reclamation = $150-$500. Include in estimate. |
| **Wrong rebate tier** | Double-check SEER2 rating meets the MINIMUM for the rebate being claimed. |

---

## MCP USAGE

### Perplexity — Equipment + Pricing

**Current equipment pricing:**
```
perplexity_ask: "Average installed cost for a [tonnage]-ton [system type] HVAC
system in [city] [state] in 2026. Include Good (entry-level like Goodman/Amana),
Better (mid-tier like Carrier/Trane), and Best (premium like Lennox/Daikin
variable speed) tiers. Include labor and materials."

search_context_size: "high"
```

**Rebate lookup:**
```
perplexity_ask: "All available HVAC rebates and incentives for homeowners in
[city] [state] [zip] in 2026. Include: state incentive programs,
[utility company] rebates, and any heat pump specific incentives.
List dollar amounts and eligibility requirements for each."

search_context_size: "high"
search_recency_filter: "month"
```

**Energy cost comparison:**
```
perplexity_ask: "Average annual energy cost to run a [tonnage]-ton central AC
at SEER [old rating] vs SEER2 [new rating] in [climate zone/city]. Include
electricity rate per kWh for [utility company] residential customers."

search_context_size: "medium"
```

**Financing rates:**
```
perplexity_ask: "Current HVAC financing rates for residential customers in 2026.
What rates do GreenSky, Synchrony, and Service Finance offer for 60, 120, and
180 month terms? Any dealer-subsidized 0% options available?"

search_context_size: "medium"
```

### Parallel Execution

**Batch 1 (fire simultaneously):**
- Perplexity → equipment pricing for all 3 tiers
- Perplexity → rebate lookup for location
- Perplexity → energy costs / utility rates

**Batch 2 (after Batch 1):**
- Calculate all tiers with rebates applied
- Calculate lifetime cost of ownership
- Calculate financing options
- Flag any estimating errors

---

## MAINTENANCE PLAN BUILDER

When job_type = maintenance_plan OR any service visit where a plan isn't in place:

**Standard maintenance plan structure:**

| Feature | Basic | Premium |
|---------|-------|---------|
| Annual price | $149-$199 | $249-$349 |
| Tune-ups per year | 1 (spring or fall) | 2 (spring AND fall) |
| Priority scheduling | Yes — jump the line | Yes — same day/next day |
| Parts discount | 10% | 15-20% |
| Diagnostic fee waived | No | Yes |
| After-hours rate | Standard | Reduced |
| Filter delivery | No | Quarterly |
| Equipment life extension | 3-5 years avg | 5-7 years avg |

**The pitch math:**
```
"A maintenance plan is $199/year. That's $16.58/month.
The average emergency repair is $800-$2,500.
A tune-up extends your system life by 3-5 years — that's $2,000-$4,000 in extra life.
Plus, you jump to the front of the line in July when 50 people are calling about their AC.
Is that worth $17 a month?"
```

**42% of homeowners already have a maintenance plan. Another 37% say they're interested.** That's 79% of customers who are open to this. If you're not pitching it, you're leaving $200-$350/year per customer on the table.

---

## COMPLETE EXAMPLE

### Example Input:
> Build a replacement estimate for 3847 Oakwood Dr, Memphis TN 38128. 1,850 sqft, 3/2, built 1988. Current system is approximately 16 years old, 3.5-ton AC with gas furnace, SEER 13. Customer called because AC is blowing warm. They're getting other quotes. Home value around $185K.

### Example Output:

---

## REPLACEMENT ESTIMATE
**3847 Oakwood Dr, Memphis TN 38128**
*1,850 sqft | 3/2 | Built 1988 | Current: 3.5-ton SEER 13 AC + Gas Furnace*
*Generated: March 4, 2026*

---

### SYSTEM RECOMMENDATION
Based on 1,850 sqft in Memphis (Climate Zone 3A, hot-humid): **4-ton system** recommended.

> Note: Your tech should verify tonnage on-site. 3.5-ton may be correct if home is well-insulated, but most 1988 homes in Memphis are slightly under-insulated — 4-ton gives headroom.

---

### GOOD / BETTER / BEST

| | Good | Better | Best |
|---|------|--------|------|
| **System** | Goodman 4-ton AC + 80% Furnace | Carrier Comfort 4-ton AC + 96% Furnace | Trane XV18 4-ton Variable Speed HP + Gas Backup (Dual Fuel) |
| **SEER2 / AFUE** | 14.3 SEER2 / 80% AFUE | 16 SEER2 / 96% AFUE | 18 SEER2 / 97% AFUE |
| **Features** | Single-stage, standard warranty | Two-stage, quieter, 10-yr parts | Variable speed, ultra-quiet, Wi-Fi thermostat, 12-yr parts |
| **Install Price** | $7,200 | $9,200 | $10,900 |
| **TVA Rebate** | $0 | $0 | $1,500 (heat pump) |
| **Net Price** | **$7,200** | **$9,200** | **$9,400** |
| **Monthly (10yr @ 6.99%)** | $84/mo | $107/mo | $109/mo |
| **Annual Energy Cost** | ~$2,200 | ~$1,750 | ~$1,400 |
| **Energy Savings vs Current** | $400/yr ($33/mo) | $850/yr ($71/mo) | $1,200/yr ($100/mo) |
| **Net Monthly Cost** | $84 - $33 = **$51/mo** | $107 - $71 = **$36/mo** | $109 - $100 = **$9/mo** |
| **Warranty** | 5-yr parts, 1-yr labor | 10-yr parts, 2-yr labor | 12-yr parts, 5-yr labor |

> **The Best option costs $2/month more than the Better option after rebates and energy savings — but gives you variable speed comfort, dual fuel efficiency, a 12-year warranty, and saves $800/year more in energy.**

---

### LIFETIME COST OF OWNERSHIP (15 Years)

| | Good | Better | Best |
|---|------|--------|------|
| Net Purchase | $7,200 | $9,200 | $9,400 |
| Energy (15 yrs) | $33,000 | $26,250 | $21,000 |
| Maintenance (15 yrs) | $3,000 | $2,700 | $2,250 |
| **15-Year Total** | **$43,200** | **$38,150** | **$32,650** |
| **Monthly ownership** | **$240/mo** | **$212/mo** | **$181/mo** |

> **The "cheapest" system costs $10,550 MORE over 15 years than the "most expensive" one.** The Best option is the cheapest to own.

---

### COST OF WAITING

Your current SEER 13 system at 16 years old:

| Monthly Cost | Amount |
|-------------|--------|
| Energy overpayment vs Best | $100/month |
| Emergency repair risk (avg) | $125/month |
| Rebate expiration risk | TVA and other utility programs can change or run out of funding |
| **Total cost of waiting** | **~$225/month** |

> Every month you wait costs roughly $225 more than it needs to. In 6 months, that's $1,350 — almost 15% of the Best system's net cost.

---

### FINANCING OPTIONS

| Term | Good ($7,200) | Better ($9,200) | Best ($9,400) |
|------|--------------|-----------------|---------------|
| 0% for 18 months | $400/mo | $511/mo | $522/mo |
| 60 months @ 6.99% | $143/mo | $182/mo | $186/mo |
| 120 months @ 7.99% | $84/mo | $107/mo | $109/mo |
| 180 months @ 9.99% | $67/mo | $86/mo | $88/mo |

*Rates are estimates. Actual rates depend on credit approval.*

---

### ANCHOR RECOMMENDATION

**For this customer (quote shopper, $185K home, system failure): Anchor on Better.**

Why: They're comparing quotes. The Good tier makes you look cheap. The Best tier may scare them before they see the math. The Better tier at $9,200 ($107/mo, net $36/mo after energy savings) hits the sweet spot. Then show them the Best tier is only $2/month more — many will upgrade themselves.

---

### REBATE DETAIL

| Rebate | Amount | Tier | Requirements |
|--------|--------|------|-------------|
| TVA EnergyRight Heat Pump | $1,500 | Best only | Must be on TVA-approved equipment list, installed by participating contractor |
| Federal tax credit | Not quoted | n/a | The 25C credit ended for equipment installed after Dec 31, 2025. Customer should check current federal, state and utility rebates (their utility, DSIRE at dsireusa.org). |
| **Total Available** | **$0** | **$0** | **$1,500** |

⚠️ **Common errors to avoid:** Ensure AHRI certificate number is on file before submitting. TVA requires the contractor to be a registered EnergyRight partner.

---

### ESTIMATING FLAGS

- ✅ Tonnage matches sqft for climate zone (4-ton for 1,850 sqft in Memphis)
- ⚠️ **Check ductwork** — 1988 home may have undersized ducts for high-efficiency system. Add ductwork inspection to scope.
- ⚠️ **R-410A availability** — Check if selected Good tier uses R-410A or R-454B. R-410A prices are rising due to phasedown.
- ✅ Electrical panel should handle AC replacement. Heat pump (Best) may need a new circuit — verify 200A panel.

---

### MAINTENANCE PLAN PITCH (include with every estimate)

> "Whatever option you choose, I'd recommend our maintenance plan — $199/year gets you priority scheduling, 2 tune-ups a year, and 15% off parts. On a brand new system, it keeps your warranty valid and extends the system life by 3-5 years. That's worth $17 a month?"

---

### HANDOFF SUMMARY
- **For Sales Coach:** Customer is a quote shopper comparing prices. Anchored on Better tier ($9,200). Best tier is only $2/mo more after rebates — if they hesitate on Better, show the Best math. Price objection likely.
- **For Job Stacker:** Replacement estimate, $9,200-$9,400 range, emergency-turned-replacement. Quote shopper = 2-7 day close cycle.
- **For Review Engine:** After installation — reference specific system installed, energy savings promise, rebate help provided.

---

*Equipment pricing based on 2026 market data via Perplexity. Actual pricing varies by supplier, region, and installation complexity. Rebate information current as of generation date — verify eligibility before submitting applications. This is an estimate framework, not a binding proposal.*

---

## OUTPUT FORMAT

Deliver estimates as:
1. **System Recommendation** — tonnage, type, climate zone rationale
2. **Good / Better / Best table** — equipment, price, rebates, net price, monthly, energy savings, net monthly cost
3. **Lifetime Cost of Ownership** — 15-year total cost comparison
4. **Cost of Waiting** — monthly cost of delaying (for replacement estimates)
5. **Financing Options** — monthly payments at 3-4 terms
6. **Anchor Recommendation** — which tier to present first and why
7. **Rebate Detail** — itemized with requirements and error warnings
8. **Estimating Flags** — anything that needs on-site verification
9. **Maintenance Plan Pitch** — included with every estimate
10. **Handoff Summary** — data for Sales Coach, Job Stacker, Review Engine

---

## WITH THE RANKGRID PLATFORM

> This skill works standalone — give it a property and job type, get back a complete 3-tier estimate. But if you're running the RankGrid platform, the estimate saves directly to the contact record with all three tiers, rebates, and financing options attached. When the customer calls back, your whole team sees what was quoted — no digging through emails or notebooks.
>
> Want this connected to a CRM with automated follow-up? That's what the RankGrid platform does: https://rankgrid.ai

---

## QUALITY CHECKLIST

Before delivering, verify:
- [ ] Are all 3 tiers priced realistically for the market? (Not too high, not impossibly low)
- [ ] Are rebates correctly applied to the right tiers? (Heat pump credits only on heat pump installs)
- [ ] Is the lifetime cost comparison included? (This is the frame that closes deals)
- [ ] Is there a financing breakdown with net monthly cost after energy savings?
- [ ] Is the anchor tier recommendation based on the customer's situation?
- [ ] Are common estimating errors flagged? (SEER vs SEER2, ductwork, panel, etc.)
- [ ] Is the maintenance plan pitch included?
- [ ] Is there a Handoff Summary for the next skill?
- [ ] Would a homeowner look at this and understand the value, not just the price?
- [ ] Does the Best tier's net monthly cost look compelling compared to the Good tier?

---

## KNOWN LIMITATIONS

| Limitation | Workaround |
|-----------|------------|
| Equipment pricing varies by region and supplier | Perplexity provides ballpark. Contractor adjusts to their actual supplier pricing. |
| Rebate programs change frequently | Always use Perplexity with recency filter. Flag "verify before submitting." |
| Manual J not calculated | Note as "tech confirms tonnage on-site." Rule-of-thumb tonnage is directional. |
| Ductwork condition unknown remotely | Flag as estimating error. Add line item for ductwork inspection if home is pre-1990. |
| Financing rates depend on customer credit | Note "rates depend on credit approval" on all financing math. |
| Can't account for attic/crawlspace access difficulty | Note as potential install complexity. Contractor adjusts labor on-site. |
