---
title: "JOURNEY-001: Financial Fog to Clarity"
status: Draft
author: cristos
created: 2026-02-26
last_updated: 2026-02-26
parent: VISION-001
---

### Lifecycle

| Phase | Date | Commit | Notes |
|-------|------|--------|-------|
| Draft | 2026-02-26 | -- | Initial creation |

---

# JOURNEY-001: Financial Fog to Clarity

## Persona

**Maya, 31, product manager.** Makes good money ($95K) but has no real picture of where it goes. Uses a checking account and two credit cards. Has tried Mint (dead), YNAB (quit after two months), and a spreadsheet (abandoned). Savings are growing slower than she'd like but she's not sure why. No debt crisis, no urgent event — just a persistent feeling that she should be doing better.

Maya is technically literate (comfortable with a terminal, has used git), but not a developer. She doesn't want to write Python scripts to understand her money.

## Goal

Go from "I don't really know where my money goes" to "I understand my finances, I have a plan, and I check in monthly."

## Stages

### 1. Discovery

**Trigger:** Maya reads a thread on Hacker News about someone using Claude Code + hledger to analyze their finances. She's intrigued by the idea of asking questions in plain English and getting real analysis back — not a pie chart.

**Actions:** Reads the README. Sees the emergency fund example in the vision. Thinks "this is what I wanted YNAB to be."

**Pain points:**
- "Is this just for developers? I'm not writing hledger journal files by hand."
- "How hard is the setup?"

**Opportunities:**
- First impression must communicate: you don't need to be a developer, and setup is fast.
- Time to first insight (< 10 min) is a key success metric for exactly this moment.

### 2. Setup & Ingestion

**Trigger:** Maya decides to try it. She has 12 months of bank statements she can download as CSV.

**Actions:**
- Installs the system (hledger + agent)
- Downloads CSVs from her bank and two credit cards
- Drops them in the intake folder

**What the agent does:**
- Detects the CSV files, analyzes their column structure
- Generates hledger import rules for each bank format
- Imports transactions, categorizing what it can confidently identify
- Flags ambiguous transactions for Maya to confirm: "Is 'AMZN MKTP' groceries, household, or something else?"
- After Maya categorizes a few, the agent learns the pattern and applies it retroactively

**Pain points:**
- CSV formats vary wildly between banks — column names, date formats, sign conventions
- First import will have many uncategorized transactions — this could feel overwhelming
- Maya doesn't know what a "chart of accounts" is

**Opportunities:**
- The agent's opinionated defaults handle chart of accounts — Maya doesn't need to design one
- CSV rules generation is a core skill — this should feel magical, not manual
- Batch categorization ("these 47 Amazon transactions — want me to split them 80/20 between shopping and household based on typical patterns?") reduces the manual work
- Once import rules are generated, subsequent months are automatic

**Ingestion variants (other users at this stage):**
- *Bank sync:* Maya could set up Plaid instead of CSV drops — one-time setup, then automatic. More convenient, less data sovereignty.
- *Receipt photos:* Maya photographs a receipt, texts it to the agent (WhatsApp, iMessage, email). Agent extracts merchant, amount, date, items, creates a transaction. Useful for cash purchases or splitting a dinner check.
- *Tax documents:* Upload a W-2 or 1099 PDF. Agent extracts income data and creates the appropriate journal entries.
- *Paystubs:* Upload a paystub photo/PDF. Agent extracts gross, deductions, net, and creates entries that properly track pre-tax contributions (401k, HSA, health insurance).

### 3. First Insight

**Trigger:** Data is imported. Maya asks her first question.

```
Maya:  "Where is my money going?"

Agent: [queries 12 months of categorized spending]
       [executes category breakdown with trends]

       Your average monthly spending is $4,850. Here's where it goes:

       Housing:        $2,100  (43%) — rent, stable
       Food:           $1,020  (21%) — $540 groceries + $480 dining
       Transport:        $385  (8%)  — car payment + gas + rideshare
       Shopping:          $340  (7%)  — clothing, electronics, misc
       Subscriptions:     $210  (4%)  — 9 services
       Everything else:   $795  (16%)

       Three things stand out:
       1. Dining is $480/month and trending up (was $380 six months ago)
       2. You have 9 subscriptions totaling $210/month — 3 show no
          activity in the last 90 days
       3. Your savings rate is 18%. That's solid, but you could be
          at 22-25% without major lifestyle changes.
```

**Emotional state:** "Oh. I actually *see* it now." This is the moment YNAB never delivered — not just categories, but what they *mean*.

**Pain points:**
- If categorization was poor during import, the numbers here will be wrong and trust breaks immediately
- First insight needs to be genuinely surprising, not obvious

**Opportunities:**
- The agent should proactively surface something Maya didn't ask about (the subscription observation, the dining trend). This is what separates analysis from a dashboard.
- This is where the "time to first insight < 10 min" metric gets tested.

### 4. Going Deeper

**Trigger:** The first insight lands. Maya wants more.

Over the next few sessions, Maya explores:

- "Why am I short this month?" → Month-over-month diff analysis
- "What are all my subscriptions?" → Full subscription audit, flags unused ones
- "Am I spending more than last year?" → Year-over-year trend analysis
- "What's my net worth?" → Multi-account balance tracking

Each question exercises a different core skill. Each answer grounds Maya's understanding in her actual numbers, not rules of thumb.

**Emotional state:** Shifting from "I don't know" to "I see the patterns." Financial literacy is building — not through lessons, but through her own data.

**Pain points:**
- Maya might ask something the skill library doesn't cover yet — agent-generated code needs to handle gracefully
- Analysis fatigue: too many insights at once can overwhelm

**Opportunities:**
- Coaching moments: when Maya asks about net worth, the agent can explain what it means, why it matters, and how hers compares to benchmarks — grounded in her numbers
- Each session builds the agent's context about Maya's financial life

### 5. Goal Setting & Lever Identification

**Trigger:** Maya's understanding reaches the point where she wants to act.

```
Maya:  "I want to save $15,000 for a down payment in 18 months."

Agent: [queries current savings rate and trajectory]
       [executes lever identification scan]

       You're currently saving ~$1,450/month. Over 18 months that's
       $26,100 — but $11,000 of that is already spoken for (emergency
       fund target you mentioned). So you have ~$15,100 on track,
       barely making it.

       To build margin, here are levers ranked by impact:
       [lever identification output — similar to vision example]

       With Scenario B (subscriptions + dining moderation), you'd
       have $18,800 at month 18 — $3,800 of buffer.
```

**Emotional state:** "I have a plan. It's specific. It's mine."

**Pain points:**
- Lever suggestions that feel judgmental ("you spend too much on coffee") will backfire
- Unrealistic scenarios erode trust

**Opportunities:**
- Interactive refinement is critical here — Maya needs to feel she chose the plan, not that it was prescribed
- The plan should connect to her stated goal, not generic "save more" advice

### 6. Monthly Habit

**Trigger:** Maya sets the plan. The agent checks in monthly.

```
Agent: Monthly check-in — March 2026

       Savings progress: $2,890 of $15,000 (19.3%)
       Timeline: on track for September 2027

       This month vs. plan:
       • Dining: $410 (target: $400) — essentially on track
       • Subscriptions: $120 (target: $120) — you canceled the three ✓
       • Unexpected: $280 car repair (one-time, not a trend)

       Net assessment: On plan. The car repair didn't derail anything
       because your buffer absorbed it. That's the buffer working.
```

**Emotional state:** Confidence. The monthly check-in takes 5 minutes and Maya knows exactly where she stands.

**Pain points:**
- If the agent nags, Maya will stop checking in
- If the data isn't current (CSV import lag), the check-in is stale

**Opportunities:**
- Tone matters: celebrate wins, contextualize setbacks ("the car repair didn't derail anything"), don't moralize
- This is where automated ingestion (Plaid) pays off — no manual CSV drops needed for the habit to work
- Drift detection should be specific and actionable, not vague warnings

### 7. Expansion

**Trigger:** Months into the habit, Maya's comfort and trust grow. She starts asking bigger questions.

- "Should I increase my 401k contribution?" → Tax-advantaged analysis with her actual tax bracket
- "My lease is up — should I buy a car or keep leasing?" → Total cost of ownership modeling
- "What does my retirement look like at this savings rate?" → Long-term projection

Each question pushes into new territory. Some are handled by existing skills; some require the agent to write new analysis code. The skill library grows.

**Emotional state:** "I'm actually good at this." Maya has gone from financial fog to financial confidence. The tool didn't just organize her money — it built her financial literacy.

---

## Pain Points Summary

| Stage | Key Pain Point | Mitigation |
|-------|---------------|------------|
| Discovery | "Is this for developers?" | Clear messaging: no code required |
| Ingestion | CSV chaos, uncategorized transactions | Opinionated defaults, batch categorization, smart rules |
| First Insight | Bad data → bad trust | Import quality matters more than speed |
| Going Deeper | Analysis fatigue | Pace insights, don't overwhelm |
| Goal Setting | Judgmental tone | Frame as options, not prescriptions |
| Monthly Habit | Nagging or stale data | Celebrate wins, automate ingestion |
| Expansion | Capability gaps | Self-extending skills handle novel questions |

## Opportunities Summary

| Stage | Key Opportunity |
|-------|----------------|
| Discovery | Time to first insight < 10 min |
| Ingestion | CSV rules generation feels magical |
| First Insight | Surface something the user didn't ask about |
| Going Deeper | Financial literacy through the user's own numbers |
| Goal Setting | Interactive refinement — user owns the plan |
| Monthly Habit | 5-minute check-in that builds confidence |
| Expansion | Skill library grows with the user's ambition |
