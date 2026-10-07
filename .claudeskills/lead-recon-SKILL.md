---
name: lead-recon
description: "Instantly research an incoming HVAC lead — property data, estimated system age, neighborhood context, and a ready-to-send speed response. Use when a lead comes in from any source (phone, web form, LSA, Angi) and the contractor needs to respond fast with context. Uses Firecrawl for Redfin/Zillow property scraping and Perplexity for market/energy data. Has two modes: Fast (60-second address-only speed response) and Deep (full research report)."
---

# Lead Recon Skill

> **Purpose:** When a lead comes in, arm the contractor with property intel and a personalized speed response in under 60 seconds — because the first contractor to respond with context wins the job.

---

## PREREQUISITE
- **Perplexity MCP** — neighborhood data, energy costs, climate context
- **Firecrawl MCP** — scraping Redfin/Zillow for property details

---

## WHAT THIS SKILL DOES

- Takes an address (minimum) and researches the property + neighborhood
- Estimates HVAC system age based on home age, last sale date, and permit history
- Pulls property details (sqft, beds/baths, year built, home value) from Redfin/Zillow
- Estimates system tonnage from square footage and climate zone
- Generates a **Speed Response** — a ready-to-send text or email that references their specific situation
- Classifies the lead into one of 4 priority buckets: Emergency / Hot / Warm / Cold
- Identifies upsell signals (aging system, high energy costs, no maintenance plan)
- **Fast Mode:** Address only → system age estimate + speed response in 60 seconds
- **Deep Mode:** Full property research + neighborhood context + lead classification

## WHAT THIS SKILL DOES NOT DO

- Does not diagnose HVAC problems (that requires an on-site visit)
- Does not guarantee system age — it's an estimate based on home age and available data
- Does not skip trace or find phone numbers
- Does not replace the contractor's expertise on equipment sizing

---

## INPUTS NEEDED

| Input | Required | Example |
|-------|----------|---------|
| Property address | Yes | "4821 Cedar Ln, Memphis TN 38118" |
| Lead source | Helpful | "Google LSA," "Angi," "referral," "web form," "phone call" |
| What they said | Helpful | "AC not cooling," "want a quote on new system," "maintenance" |
| Urgency signals | Helpful | "System is down," "no heat," "just getting prices" |
| Mode | Optional | "fast" (default) or "deep" |

> **Minimum viable input:** Just the address. Everything else improves the output but isn't required.

---

## GOAL

- Primary: Get a personalized speed response out in under 60 seconds (Fast Mode) or 5 minutes (Deep Mode)
- Secondary: Give the contractor enough context to sound like they already know the customer's situation
- Tertiary: Identify upsell opportunities (system replacement, maintenance plan, ductwork)

---

## THE SPEED ADVANTAGE

Only **17% of HVAC contractors** respond within 1 hour. **73.8% of homeowners** expect service within 24 hours for emergencies. Customers contact **3-5 contractors** simultaneously.

The contractor who responds first with something personalized — not just "when can I come out?" — wins. That's what this skill exists to do.

---

## FRAMEWORK: Fast Mode vs. Deep Mode

### FAST MODE (Default — 60 seconds)

**When to use:** Every incoming lead. No exceptions. Speed beats depth.

**What happens:**
1. Take the address
2. Estimate home age → estimate system age (see System Age Calculator below)
3. Estimate tonnage from sqft (see Tonnage Estimator below)
4. Generate speed response based on what you know
5. Classify as Emergency / Hot / Warm / Cold

**No MCP calls in Fast Mode.** Pure logic and estimation. The response goes out NOW.

**System Age Calculator:**
```
IF year_built is known:
  IF year_built before 1990 → System likely replaced at least once. Estimate current system: 12-20 years old.
  IF year_built 1990-2005 → Original system possible. Estimate: 20-35 years (likely on 2nd+ system).
  IF year_built 2005-2015 → Could be original. Estimate: 10-20 years.
  IF year_built 2015-present → Likely original system. Estimate: under 10 years.

AVERAGE HVAC system lifespan: 15-20 years (AC units avg 15, furnaces avg 18-20, heat pumps avg 15)
IF system_age > 15 → Flag: REPLACEMENT CANDIDATE
IF system_age > 10 → Flag: MAINTENANCE PLAN OPPORTUNITY
IF system_age < 5 → Flag: LIKELY UNDER WARRANTY — repair focus
```

**Tonnage Estimator (rule of thumb):**
```
General formula: 1 ton per 500-600 sqft (varies by climate zone)

HOT CLIMATES (Southeast, Southwest, Gulf Coast):
  1 ton per 400-500 sqft

MODERATE CLIMATES (Mid-Atlantic, Midwest):
  1 ton per 500-600 sqft

COLD CLIMATES (Northeast, Northern Midwest):
  1 ton per 600-700 sqft (heating load dominates)

Example: 1,800 sqft home in Memphis (hot) → 3.5-4.5 tons → likely 4-ton system
```

**Lead Classification (4 buckets):**

| Bucket | Signals | Response Speed |
|--------|---------|---------------|
| **EMERGENCY** | System down, no heat/AC, safety concern, "not working" | Respond in < 5 minutes |
| **HOT** | Getting quotes for replacement, system is old and struggling, referred by someone | Respond in < 15 minutes |
| **WARM** | Maintenance request, "thinking about replacing," seasonal tune-up | Respond within 1 hour |
| **COLD** | "Just getting prices," no urgency, info-only request | Respond within 4 hours |

### DEEP MODE (3-5 minutes)

**When to use:** After speed response is sent, OR for high-value leads you want to prep for.

**What happens (in addition to Fast Mode):**
1. Firecrawl → scrape Redfin/Zillow for property details
2. Perplexity → pull neighborhood energy costs, local HVAC market data
3. Build full property profile with value, age, size, and estimated system specs
4. Check if customer has left reviews for other contractors (reputation signal)
5. Identify all upsell opportunities
6. Generate a deeper follow-up talking points sheet for the sales call

---

## SPEED RESPONSE TEMPLATES

### Emergency Lead
```
"Hi [Name], this is [Contractor] with [Company]. I can see you're at [address] —
[estimated sqft] home built in [year]. I've got a tech who can be there
[today/tomorrow]. What's happening with the system right now?"
```

### Replacement Quote Lead
```
"Hi [Name], this is [Contractor] with [Company]. Got your request for [address].
Based on your home size, you're probably running a [tonnage]-ton system that's
[estimated age] years old — right around when most homeowners start looking at
options. I'd love to come take a look and put together some options for you.
What day works best this week?"
```

### Maintenance Lead
```
"Hi [Name], thanks for reaching out about [address]. A tune-up on a
[estimated age]-year-old system is smart — catches small problems before they
become expensive ones. We can get you on the schedule [this week/next week].
Does [day] work?"
```

### Referral Lead
```
"Hi [Name], [referrer] mentioned you might need some help with your HVAC at
[address]. They're one of our favorite customers. What's going on with the
system? Happy to take a look."
```

### Generic / Unknown
```
"Hi [Name], this is [Contractor] with [Company]. Got your info for [address] —
how can I help? Is there something specific going on with your heating or
cooling, or are you looking at options?"
```

---

## DEEP MODE: MCP USAGE

### Firecrawl — Property Data

**Find Redfin URL:**
```
firecrawl_search:
  query: "[full address] site:redfin.com"
  limit: 3
```

**Scrape property details:**
```
firecrawl_scrape:
  url: "[redfin URL]"
  formats: [{ type: "json", prompt: "Extract: address, bedrooms, bathrooms, sqft,
    year_built, lot_size, property_type, redfin_estimate, last_sale_date,
    last_sale_price, heating, cooling, annual_tax", schema: {...} }]
  proxy: "stealth"
  waitFor: 5000
```

**If Redfin fails:** Try Zillow. Search `"[address]" site:zillow.com` via Firecrawl, then scrape.

### Perplexity — Market Context

**Neighborhood + energy data:**
```
perplexity_ask: "For zip code [zip] [city] [state]: median home value, average
electric bill for residential homes, average natural gas bill, local utility
company name, and any current HVAC rebate programs or energy efficiency incentives
available to homeowners."

search_context_size: "high"
```

**Local HVAC competitive landscape (optional):**
```
perplexity_ask: "Top rated HVAC contractors near [zip code] [city] [state] on
Google Maps. How many reviews does the top-rated company have and what is their
star rating?"

search_context_size: "medium"
```

### Parallel Execution

**Batch 1 (fire simultaneously):**
- Firecrawl → Redfin property scrape
- Perplexity → neighborhood + energy data

**Batch 2 (after Batch 1):**
- Compile full profile
- Generate deep talking points

---

## UPSELL SIGNAL DETECTION

| Signal | What It Means | Upsell Opportunity |
|--------|--------------|-------------------|
| System age 15+ years | Near or past end of life | Replacement estimate (Good/Better/Best) |
| System age 10-15 years | Working but aging | Maintenance plan to extend life OR replacement conversation |
| System age < 10 years | Should be under warranty or running fine | Repair + maintenance plan |
| Home built pre-1990, no permit history | May have original ductwork | Ductwork inspection/replacement |
| High energy bills mentioned | Efficiency problem | High-SEER replacement or insulation |
| "Just moved in" | Don't know system history | Inspection + maintenance plan |
| Emergency call on old system | Repair vs replace decision point | Quote Builder for both options |
| Referral customer | High trust, high close rate | Premium tier (Best option) |

---

## DECISION LOGIC

```
IF only address provided → Run Fast Mode, classify as WARM (no urgency data)
IF "not working" / "broken" / "no heat" / "no AC" → Classify EMERGENCY
IF "replacing" / "new system" / "quote" / "estimate" → Classify HOT
IF "maintenance" / "tune-up" / "check-up" / "inspection" → Classify WARM
IF "prices" / "thinking about" / "someday" / "planning" → Classify COLD
IF lead source is LSA or Google → Classify one level hotter (these leads are actively searching)
IF lead source is referral → Classify one level hotter + use referral template
IF estimated system age > 15 AND lead is repair call → Include replacement mention in response
IF mode = "deep" OR contractor says "tell me more about this lead" → Run Deep Mode
DEFAULT → Fast Mode with WARM classification
```

---

## CONSTRAINTS

- [ ] Fast Mode NEVER makes MCP calls — speed is the entire point
- [ ] Never present system age as fact — always "estimated" or "likely around"
- [ ] Never diagnose problems remotely — "I'd need to take a look" is always the right answer
- [ ] Speed response must be under 160 characters for SMS (2-3 sentences)
- [ ] Always end speed response with a question (questions get replies)
- [ ] If lead is EMERGENCY, response goes out before any research
- [ ] Deep Mode always references where data came from (Redfin, Perplexity, etc.)
- [ ] Never mention competitor contractors by name in responses to the customer
- [ ] Tonnage estimates are rules of thumb — always note "your tech will confirm on-site"
- [ ] If home value is very high ($500K+), assume premium customer — adjust tone accordingly

---

## COMPLETE EXAMPLE

### Example Input:
> Run lead recon on 3847 Oakwood Dr, Memphis TN 38128. They called from Google LSA saying their AC isn't cooling. System sounds like it's running but blowing warm air.

### Example Output (Fast Mode):

---

## LEAD RECON — FAST MODE
**3847 Oakwood Dr, Memphis TN 38128**
*Classification: EMERGENCY | Source: Google LSA*

**Quick Profile:**
- Memphis, TN → Hot climate zone (1 ton per 400-500 sqft)
- 38128 is a mix of 1970s-1990s homes
- If built ~1985: system likely 10-20 years old (original system replaced at least once)
- Estimated tonnage: 3-4 ton (assuming ~1,600-2,000 sqft, typical for area)
- AC running but blowing warm → likely refrigerant, compressor, or capacitor issue

**Lead Bucket: EMERGENCY**
- System is actively failing in a hot climate
- Google LSA = actively searching, high intent
- Responding to 3-5 other contractors right now

**Speed Response (ready to send):**

> Hi, this is [Name] with [Company]. I saw your request about the AC at Oakwood Dr — warm air with the system running usually points to something we can diagnose fast. I've got availability [today/tomorrow]. What time works for you?

**Upsell Signals:**
- If system is 15+ years → Repair vs replace conversation (trigger Quote Builder)
- Emergency repair → Perfect time to pitch maintenance plan ("this could've been caught in a tune-up")
- LSA lead + emergency = highest close probability in your pipeline

**Recommended Next:**
- Send speed response NOW (< 5 minutes from lead)
- If they book: run Deep Mode before the appointment for full property context
- After diagnosis: if repair > 50% of replacement cost, run Quote Builder for Good/Better/Best

---

**Time saved:** ~15 minutes of research compressed into 60 seconds. Response goes out before competitors even check their voicemail.

---

### Example Output (Deep Mode — run after speed response sent):

---

## LEAD RECON — DEEP MODE
**3847 Oakwood Dr, Memphis TN 38128**
*Generated: March 4, 2026 | Sources: Redfin, Perplexity*

### PROPERTY DETAILS
| Field | Data | Source |
|-------|------|--------|
| Property Type | Single Family | Redfin |
| Beds/Baths | 3 / 2 | Redfin |
| Sqft | 1,850 | Redfin |
| Year Built | 1988 | Redfin |
| Home Value | $185,000 (Redfin estimate) | Redfin |
| Last Sale | 2019 at $142,000 | Redfin |
| Lot Size | 0.22 acres | Redfin |
| Annual Tax | $1,840 | Redfin |
| Heating | Central Gas Furnace | Redfin |
| Cooling | Central AC | Redfin |

### SYSTEM ESTIMATES
| Estimate | Value | Basis |
|----------|-------|-------|
| System Age | 12-18 years (likely original to 2019 purchase OR replaced 2006-2012) | Home built 1988, sold 2019 |
| Tonnage | 3.5-4 ton | 1,850 sqft in hot climate (Memphis) |
| SEER Rating | Likely 13-14 (if 2006-2012 install) or 10-12 (if older) | Age-based estimate |
| Annual Energy Cost | ~$2,400-$3,000 (Memphis average) | Perplexity |

### NEIGHBORHOOD CONTEXT
| Metric | Data | Source |
|--------|------|--------|
| Median Home Value (38128) | $165,000 | Perplexity |
| Avg Electric Bill | $145-$175/month | Perplexity |
| Local Utility | Memphis Light Gas & Water (MLGW) | Perplexity |
| Available Rebates | TVA EnergyRight heat pump rebates up to $1,500; MLGW weatherization program | Perplexity |
| Climate Zone | IECC Zone 3A (hot-humid) | Standard |
| Top Local Competitor | [Company] — 287 reviews, 4.7 stars | Perplexity |

### UPSELL OPPORTUNITIES
1. **Replacement candidate** — System is likely 12-18 years old (approaching or past 15-year avg lifespan for AC)
2. **Energy savings pitch** — Upgrading from SEER 13 to SEER 16+ saves ~20-30% on cooling costs ($400-$700/year in Memphis)
3. **Heat pump rebate** — TVA EnergyRight offers up to $1,500 for qualifying heat pump installations
4. **Maintenance plan** — 42% of homeowners have one, 37% more are interested. This repair visit is the perfect pitch moment.

### TALKING POINTS FOR THE SALES CALL
- "Your home is about 1,850 square feet — you're running a 3.5 to 4-ton system."
- "Based on when the home was built and sold, your AC is probably 12-18 years old. Most systems last about 15."
- "There are some solid rebates right now through TVA — up to $1,500 if you go with a heat pump. I can show you what that looks like."
- "Either way, I'll diagnose exactly what's happening and give you honest options — repair and replacement — so you can decide what makes sense."

### HANDOFF SUMMARY
- **For Quote Builder:** 3/2 home, 1,850 sqft, Memphis 38128, likely 3.5-4 ton system, 12-18 years old, central gas furnace + AC, TVA rebates available
- **For Sales Coach:** Emergency lead from Google LSA, actively searching, likely comparing 3-5 contractors, repair vs replace conversation incoming
- **For Job Stacker:** Emergency bucket, high close probability (LSA + system failure + replacement candidate)

---

*Property data from Redfin. System age and tonnage are estimates — your technician will confirm on-site. Energy costs based on Memphis averages via Perplexity.*

---

## OUTPUT FORMAT

**Fast Mode delivers:**
1. **Quick Profile** — property estimates from address alone
2. **Lead Bucket** — Emergency / Hot / Warm / Cold with reasoning
3. **Speed Response** — copy-paste ready text message
4. **Upsell Signals** — what to pitch when you get there
5. **Recommended Next** — what to do after sending the response

**Deep Mode adds:**
6. **Property Details** — table from Redfin/Zillow
7. **System Estimates** — age, tonnage, SEER, energy costs
8. **Neighborhood Context** — home values, energy costs, rebates, competition
9. **Talking Points** — what to say on the sales call
10. **Handoff Summary** — data formatted for Quote Builder, Sales Coach, Job Stacker

---

## WITH THE RANKGRID PLATFORM

> This skill works standalone — paste an address and get a speed response. But if you're running the RankGrid platform, new leads trigger recon automatically. The speed response sends before you even see the notification. Lead classification, property data, and upsell signals attach to the contact record so your whole team sees it.
>
> Want this connected to a CRM with automated follow-up? That's what the RankGrid platform does: https://rankgrid.ai

---

## QUALITY CHECKLIST

Before delivering, verify:
- [ ] Did the speed response go out in under 60 seconds (Fast Mode)?
- [ ] Does the speed response end with a question?
- [ ] Is the speed response under 160 characters / 2-3 sentences for SMS?
- [ ] Is system age presented as an estimate, not a fact?
- [ ] Is the lead classified into the right bucket with reasoning?
- [ ] Are upsell signals identified based on actual data?
- [ ] If Deep Mode: are all data points sourced?
- [ ] If Deep Mode: is there a Handoff Summary for the next skill in the chain?
- [ ] Is the response personalized to their specific situation (not generic)?
- [ ] Would the homeowner feel like this contractor already knows their house?

---

## KNOWN LIMITATIONS

| Limitation | Workaround |
|-----------|------------|
| System age is always an estimate | Only on-site inspection confirms. Note this in every output. |
| Firecrawl may not find the property on Redfin | Try Zillow. If neither works, use address + county records age only. |
| No permit history without county records | Note as gap. Suggest contractor ask homeowner about last system replacement. |
| Energy cost data is ZIP-level averages | Good enough for the pitch. Actual bills vary by insulation, usage, etc. |
| Can't determine actual system brand/model remotely | Tech confirms on-site. Estimate tonnage from sqft for now. |
| Fast Mode has no MCP calls | That's by design. Speed > depth for initial response. |
