# 6 AI Skills That Run Your HVAC Sales Operation

Built by [CyclSales](https://cyclsales.com) — AI-powered CRM for home service businesses.

These aren't templates. They're AI skills that plug into Claude Code and do real work — research leads in 60 seconds, build 3-tier estimates with live rebate data, coach your follow-up, rank your pipeline, and automate review collection.

---

## What's Inside

### 1. Lead Recon
Give Claude an address. In 60 seconds, it estimates the home's HVAC system age, calculates tonnage, classifies the lead (Emergency / Hot / Warm / Cold), and writes a personalized speed response ready to send — before your competitors even check their voicemail. Deep Mode pulls property details from Redfin, neighborhood energy costs, current rebate programs, and local market context. Only 17% of HVAC contractors respond within an hour. This puts you in that 17%.

### 2. Quote Builder
Stop sending one-price estimates that lose to the low bidder. Quote Builder creates Good / Better / Best pricing with real equipment recommendations, federal tax credits, utility rebates, financing options, and energy savings math. Shows the homeowner what each system actually costs over 15 years (the "expensive" system often saves $10K+), plus a Cost of Waiting calculator that shows what delaying costs them every month. Frames the purchase as an investment, not an expense.

### 3. Sales Coach
Most contractors send one estimate and wait. 80% of sales need at least 5 follow-up contacts. Sales Coach reads your conversation with the customer, figures out what type of buyer they are (Emergency, Quote Shopper, Price-Sensitive, Skeptical, Referred), and tells you exactly what to say next — the message, the timing, and why it works. Includes a 7-touch follow-up cadence, objection responses, maintenance plan scripts, and field scripts for your techs. Structured follow-up moves close rates from 25% to 40-50% with zero extra marketing spend.

### 4. Job Stacker
Give Claude your entire pipeline — 5 estimates or 50 — and it ranks them using a simple scoring system: Urgency, Value, Readiness, and Speed to Close. Tells you which 3 jobs to focus on this week, flags stale estimates, and builds a day-by-day action plan starting from today. At 25% close rate with 24 estimates/month: $504K/year. At 50%: $1.008M. The difference is knowing where to spend your time.

### 5. Review Engine
After every completed job, generates a personalized review request timed by job type (emergency = within 1 hour, installation = next morning, tune-up = same day). Includes a direct Google review link, QR code strategy, 3-touch follow-up if they don't review right away, and response templates for both positive and negative reviews that boost your Google ranking. Target: 300+ reviews at 4.7+ stars with 10+ new reviews/month. That's how you become the #1 HVAC contractor on Google Maps in your market.

### 6. CRM Connect 🔒 CyclSales Clients Only
Ties everything together by connecting Claude directly to your CRM. Lead Recon saves contacts automatically. Quote Builder pushes estimates to your pipeline. Sales Coach sends follow-ups on schedule. Job Stacker reads your pipeline live — no manual entry. Review Engine fires when a job is marked complete.

**This skill is available exclusively to CyclSales clients.** [Learn more at cyclsales.com](https://cyclsales.com)

---

## The Skill Chain

```
Lead comes in
    ↓
Lead Recon → Speed response out in 60 seconds
    ↓
Quote Builder → Good/Better/Best with rebates + financing
    ↓
Sales Coach → Follow-up on unsold estimates (7-touch cadence)
    ↓
Job Stacker → Weekly pipeline priority (who to call first)
    ↓
Review Engine → 5-star review request (timed by job type)
    ↓
CRM Connect → Everything flows into your CRM automatically (CyclSales clients only)
```

---

## Setup

### Step 1: Clone the repo
```bash
git clone https://github.com/miron-tech/hvac-claude-skills.git
```

### Step 2: Copy skills into your project
```bash
cp -r hvac-claude-skills/.claudeskills your-project/.claudeskills
cp hvac-claude-skills/CLAUDE.md your-project/CLAUDE.md
```

### Step 3: Connect your data sources (recommended)

These skills work best when Claude can look up property data and market information on its own. Without these connections, the skills still work — Claude will just ask you to provide the data manually.

You'll add these to your Claude Code settings file (`.mcp.json` in your project folder or `~/.claude/mcp.json` for global access).

**Perplexity** — powers property research, rebate lookups, equipment pricing, and market data:
```json
{
  "mcpServers": {
    "perplexity": {
      "command": "npx",
      "args": ["-y", "@perplexity-ai/mcp-server"],
      "env": {
        "PERPLEXITY_API_KEY": "your-key-here"
      }
    }
  }
}
```
Get your API key at [perplexity.ai/settings/api](https://www.perplexity.ai/settings/api)

**Firecrawl** — pulls property details from Redfin and Zillow (sqft, year built, beds/baths, home value):
```json
{
  "mcpServers": {
    "firecrawl": {
      "command": "npx",
      "args": ["-y", "firecrawl-mcp"],
      "env": {
        "FIRECRAWL_API_KEY": "your-key-here"
      }
    }
  }
}
```
Get your API key at [firecrawl.dev](https://www.firecrawl.dev/)

**CRM Connection** — connects Claude directly to your CyclSales CRM for reading/writing contacts, pipeline, and conversations:
```json
{
  "mcpServers": {
    "gohighlevel": {
      "type": "url",
      "url": "https://services.leadconnectorhq.com/mcp/",
      "headers": {
        "Authorization": "Bearer YOUR_PRIVATE_INTEGRATION_TOKEN",
        "Version": "2021-07-28"
      }
    }
  }
}
```
To get your token: CyclSales → Settings → Integrations → Private Integrations → Create New → Select scopes (contacts, conversations, opportunities, calendars) → Copy the token.

### Step 4: Start using
Open Claude Code in your project folder. The skills are ready — just tell Claude what you need.

---

## Usage Examples

**Lead recon (60-second speed response):**
> "Run lead recon on 3847 Oakwood Dr, Memphis TN 38128. AC not cooling, called from Google LSA."

**Build a replacement estimate:**
> "Build an estimate for 3847 Oakwood Dr — 1,850 sqft, system is about 16 years old, 3.5-ton AC with gas furnace. Customer is getting other quotes."

**Sales coaching on unsold estimate:**
> "I sent Sarah the $9,200 estimate 5 days ago. She said 'let me look it over' and hasn't responded. She's getting 2 other quotes. What do I say?"

**Pipeline prioritization:**
> "Here are my 5 open estimates: [paste list]. I have 30 hours this week. Which ones should I focus on?"

**Review request:**
> "Just finished installing a Carrier 4-ton for Sarah at 3847 Oakwood Dr. She was really happy. Generate a review request."

**CRM integration:**
> "Save this lead to my CRM." / "Push this estimate to pipeline." / "Show my pipeline." / "Stack my jobs." / "Send that review request."

---

## What Makes These Different

| What You Do Now | What These Skills Do |
|----------------|---------------------|
| Google the address, hope you find something useful | Claude pulls property data from Redfin, estimates system age, and writes a speed response in 60 seconds |
| Type numbers into a spreadsheet or proposal tool | Claude builds 3-tier pricing with live rebate data, financing math, and 15-year cost comparison |
| Send one estimate and hope they call back | Claude gives you a 7-touch follow-up plan with the exact messages, timing, and objection responses |
| Look at your pipeline and guess who to call | Claude scores every lead and builds a day-by-day action plan for the week |
| Remember to ask for reviews sometimes | Claude generates a personalized review request timed to the job type, with follow-up if they don't respond |
| Copy-paste everything into your CRM | Claude reads from and writes to your CRM directly |
| Memorize scripts | Claude explains WHY each approach works — so you actually get better at selling, not just more scripted |

---

## Who This Is For

- HVAC contractors who want to close more of the estimates they already send
- Owners spending 2-3 hours a day on follow-up, estimates, and admin
- Contractors who know they need to follow up more but don't have a system for it
- Anyone who wants 300+ Google reviews but can't remember to ask after every job
- Teams that need a consistent sales process across techs and estimators

## Who This Is NOT For

- Contractors already closing at 50%+ with 500+ reviews — you're already doing this
- Anyone expecting AI to show up and install a furnace — Claude handles the research, math, and messaging. You do the work.
- People who don't have Claude Code yet — [get it here](https://claude.com/code)

---

## Marketing Funnel Included

This repo also includes a complete lead magnet funnel for acquiring HVAC contractors as clients. Everything lives in `campaigns/hvac-speed-selling/`.

**The HVAC Speed Selling Playbook** — a free 8-page guide that teaches HVAC contractors how to research leads in 60 seconds, build Good/Better/Best estimates, and run a follow-up system that actually works. It's the manual version of what the AI skills automate.

What's in the campaign folder:
- **Lead magnet** — 8-page playbook following the proven formula (hook → quick win → framework → implementation → CTA bridge)
- **Landing page** — GHL-ready HTML with background hero video, opt-in form, UTM tracking, and mobile-responsive design
- **7-email nurture sequence** — Delivery → Story → Problem → Proof → Objection → Nudge → Breakup (Days 0-10)
- **5 social promotion hooks** — Pain, Data, Question, How-To, and Story formats for Facebook, LinkedIn, and Nextdoor
- **3 Facebook ad variations** — Short/retargeting, Medium/cold traffic, Long/story format with targeting and budget recommendations
- **Campaign brief** — Full funnel map, segmentation logic, UTM tracking, and go-live checklist

The funnel bridges the free playbook to a CyclSales demo — showing contractors the manual process first, then offering the automated version.

---

## Want This Running on Autopilot?

These skills are powerful inside Claude Code. But if you want lead research triggering automatically when a call comes in, follow-up sequences running while you sleep, review requests firing when you mark a job complete, and your pipeline updating itself — that's what [CyclSales](https://cyclsales.com) does.

- AI follow-up that runs 24/7 — SMS, email, and voice
- Pipeline with scoring and automatic stage advancement
- Voice AI that answers inbound calls and qualifies leads
- Review requests that fire on every completed job
- All 6 skills pre-configured and connected to your CRM
- Done-for-you setup

**[Book a demo](https://cyclsales.com)** and see what it looks like when these skills run without you touching anything.

---

## License

MIT — use these however you want. If they help you close a deal, that's all we need.

---

Built by [Miron Briley](https://cyclsales.com) at CyclSales.
