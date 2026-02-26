---
title: "VISION-001: LLM Finance Wizard -- Your AI Financial Analyst"
status: Draft
author: cristos
created: 2026-02-26
last_updated: 2026-02-26
---

### Lifecycle

| Phase | Date | Commit | Notes |
|-------|------|--------|-------|
| Draft | 2026-02-26 | -- | Initial creation; v3 after internal iteration |
| Draft | 2026-02-26 | -- | Rewrite: reframed around agentic coding agent as core domain |
| Draft | 2026-02-26 | -- | Rewrite: scenario modeling as central concept; honest competitive analysis |
| Draft | 2026-02-26 | -- | Fix: Monte Carlo as tool not non-goal; clarify code reliability spectrum; "existing = win" framing |
| Draft | 2026-02-26 | -- | Add: Section 7 usage stories — five personas illustrating breadth of core loop |

---

# LLM Finance Wizard

**A frontier-level agentic coding agent for personal finance -- opinionated, self-extending, and grounded in structured accounting data.**

---

## 1. The Problem

Personal finance tools in 2026 can show you where your money went. None of them can help you figure out where it should go.

**The polished dashboards (Monarch, YNAB, Copilot)** categorize your transactions and render pie charts. Some now offer AI-powered summaries. But ask "I need to save $300 more per month -- what should I actually change?" and you get nothing. They can tell you that you spent $480 on dining out; they can't tell you that cutting dining by 30% while canceling three unused subscriptions and switching car insurance would collectively get you to $300 -- or model what that looks like over 12 months alongside your debt payoff timeline.

**The planning tools (ProjectionLab, Boldin, Pralana)** are excellent at modeling forward-looking scenarios: "If you reduce spending by $500/month, you can retire 2 years earlier." But they never look at your actual spending data and tell you *which* $500 to cut. They model parameters you define manually; they don't identify the parameters for you.

**The AI financial advisors (Origin Financial, Hiro)** are the newest entrants. Origin uses multi-agent LLM architecture with deterministic math engines; Hiro offers conversational what-if scenarios. These are the most direct competitors to this vision and worth watching closely. But even they don't combine structured accounting data with agentic code execution -- they use pre-built models with adjustable parameters, which means they can only answer the questions their developers anticipated. And they don't help you discover the levers in your own spending.

**Plain-text accounting tools (hledger, Beancount)** give you a rigorous, programmable data foundation. But extracting insight requires both accounting knowledge and programming skill -- and every analysis must be hand-coded.

**General-purpose AI (ChatGPT Code Interpreter, Claude)** can do brilliant ad-hoc analysis when you upload data and prompt carefully. But there's no persistence, no structured data layer, no domain skills, and no accumulated context. A developer *can* string together Claude Code + hledger-mcp + a good CLAUDE.md and get maybe 40-60% of this vision in a focused weekend -- but the gap between "answered my question about last month's spending" and "reliable financial coaching system that identifies levers and models scenarios across my financial life" is enormous.

**The real gap is the synthesis.** Analysis tells you *what* ("you need $300/month more"). Coaching tells you *why* ("here's what that means for your emergency fund timeline"). Scenario modeling tells you *how* ("here are the levers available to you, and here's what different combinations look like"). No tool does all three, grounded in your actual data, with the computational rigor to be trustworthy.

---

## 2. The Vision

LLM Finance Wizard is a **personal AI financial analyst** -- an agentic coding agent that sits on top of structured accounting data and helps you understand, manage, and improve your financial life.

### The Core Loop: Analysis → Coaching → Scenario Modeling

The agent's central capability is an integrated loop that connects understanding your finances to changing them:

```
1. ANALYSIS    "What's happening?"
   The agent queries your structured accounting data and executes code
   to understand your current financial state. Not summaries -- computation.

          ↓

2. COACHING    "Why does it matter?"
   The agent explains the implications in terms you understand, connecting
   your current state to your goals. Personalized education, not generic tips.

          ↓

3. LEVER       "What can I change?"
   IDENTIFICATION
   The agent scans your actual spending, income, and obligations to identify
   specific, concrete levers available to you -- not abstract advice.

          ↓

4. SCENARIO    "What happens if I pull these levers?"
   MODELING
   The agent models multiple combinations of levers across time horizons,
   showing you the tradeoffs. Not a single recommendation -- a menu of
   options with computed consequences.

          ↓

5. INTERACTIVE "This combination feels close, but..."
   REFINEMENT
   You adjust. The agent re-models. You converge on a plan that fits
   your actual life, not a textbook recommendation.

          ↓

6. TRACKING    "Am I on track?"
   The agent checks in against the plan. Flags drift. Suggests course
   corrections. The loop begins again.
```

**Example:**

```
User: "I want to build a 3-month emergency fund. I have $4,300 saved
       and my essentials run about $3,200/month. Help me get there."

Agent: [queries accounting engine: 12 months of categorized spending]
       [executes code: essential vs. discretionary breakdown, variability
        analysis, recurring charge detection]

       "You need $9,600 total, so $5,300 more. At your current savings rate
        of $410/month, that's 12.9 months.

        But I found several levers in your spending that could accelerate this.
        Here are the top 5 by monthly impact:"

       1. Dining out: $480/mo avg (up 34% YoY). Reducing to your Q2
          baseline of $320 saves $160/mo.
       2. Subscriptions: $210/mo across 9 services. 3 show zero usage
          in 90 days (StreamPlus $30, CloudGym $45, NewsDaily $15).
          Canceling saves $90/mo.
       3. Grocery optimization: Your Costco trips average $340/mo, but
          ~15% ($51) is household supplies currently categorized as food.
          [More on this below.] Actual grocery spend is $289/mo, which
          is close to area median.
       4. Insurance: Your auto premium ($185/mo) is 22% above the average
          for your profile. Shopping quotes could save ~$40/mo.
       5. Coffee shops: $95/mo (Starbucks 4x/week). A daily habit, not
          a quick cut -- but worth knowing.

       "Let me model some combinations:"

       Scenario A (Low effort): Cancel 3 unused subs → $90/mo
         Emergency fund in 9.5 months

       Scenario B (Moderate): Subs + dining to Q2 level → $250/mo
         Emergency fund in 8.0 months

       Scenario C (Aggressive): Subs + dining + insurance shop → $290/mo
         Emergency fund in 7.6 months

       Scenario D (Your mix): Tell me which levers feel realistic and
         I'll model the combination.

User: "B is close but I can't cut dining that much. What if I do $400
       instead of $320, and I do shop for insurance?"

Agent: [re-executes scenario model with adjusted parameters]

       Scenario B-modified: Subs ($90) + dining to $400 ($80) + insurance ($40)
         = $210/mo additional savings
         → $620/mo total savings rate
         → Emergency fund in 8.5 months
         → You'll hit it by mid-November.

       "Want me to set this as your plan and check in monthly?"
```

This loop -- from data to levers to scenarios to commitment -- is what no existing tool provides.

### The Architecture: Three Layers

```
┌─────────────────────────────────────────────────────────────────┐
│                     CORE DOMAIN                                  │
│                                                                  │
│   Frontier Agentic Coding Agent                                  │
│   ┌──────────────────────────────────────────────────────┐      │
│   │  Opinionated skill library (battle-tested defaults)  │      │
│   │  + frontier coding capability (build what you need)  │      │
│   │  + financial domain knowledge (coaching, advice)     │      │
│   └──────────────────────────────────────────────────────┘      │
│                          │                                       │
│            ┌─────────────┼─────────────┐                        │
│            ▼             ▼             ▼                         │
│      Code execution   Queries    Skill library                  │
│      (Python, SQL,    & reports  (.agents/skills/)              │
│       visualizations)                                            │
├────────────┬────────────────────────────────┬───────────────────┤
│  GENERIC   │                                │  GENERIC          │
│  SUBDOMAIN │   Accounting Engine            │  SUBDOMAIN        │
│            │                                │                    │
│  Ingestion │   hledger, Beancount,          │  Output /         │
│            │   or custom Python scripts     │  Delivery         │
│  Plaid,    │                                │                    │
│  CSV,      │   Handles: math, validation,   │  Chat, dashboards │
│  OFX,      │   balance checking, reporting, │  slide decks,     │
│  manual    │   data integrity               │  PDFs, Excel      │
│  entry     │                                │                    │
└────────────┴────────────────────────────────┴───────────────────┘
```

**The core domain is the agent and its skill library.** The accounting engine and ingestion pipeline are generic subdomains -- important, but solved problems that we integrate rather than reinvent.

The differentiated value is the agent's **judgment** (opinionated defaults), **capability** (frontier-level code execution), and **growth** (the skill library improves with use).

---

## 3. How the Agent Works

### 3.1 Code Execution, Not Chat Completion

When you ask "Am I saving enough for retirement?", the agent doesn't generate a text answer. It:

1. **Queries the accounting engine** for your income, expenses, savings rate, and investment balances
2. **Writes a Python script** that models compound growth scenarios using your actual numbers, tax bracket, and stated retirement age
3. **Executes the script** and generates a visualization of outcomes
4. **Interprets the results** in plain language with specific, actionable recommendations
5. **Optionally packages the analysis** as a dashboard panel, a slide in a quarterly review deck, or a PDF

The LLM provides intelligence. The code provides numerical accuracy. The accounting engine provides data integrity. Each layer does what it's best at.

This separation is architecturally necessary, not just aesthetically clean. The FinNLP 2025 paper (ACL Anthology) found that *"LLMs struggle severely with accounting, often producing inaccurate calculations."* Origin Financial reached the same conclusion independently -- their system uses pre-built math modules rather than letting the LLM compute directly.

**The reliability spectrum of code.** All executed code is deterministic -- given the same inputs, it produces the same outputs. But not all code has the same reliability profile:

- **Battle-tested skill code** (e.g., the debt payoff planner): Written once, reviewed, tested against known scenarios, and reused many times. This is as reliable as a traditional financial calculator. It's the equivalent of Origin's pre-built modules, except it started as agent-generated code and graduated through use.
- **Agent-generated code** (e.g., a novel "should I refinance?" analysis): Written by the LLM on the fly. Correct in structure (the LLM is good at writing code) but might contain logic errors, miss edge cases, or use wrong tax rates. Trustworthy enough for exploration; should be reviewed before making major decisions.

Skills are just code that's been validated through use. They start as generated code and graduate to trusted code. The skill library is the mechanism that converts ad-hoc reliability into battle-tested reliability over time.

### 3.2 Opinionated Defaults, Extensible by Design

The agent ships with a core library of battle-tested skills:

| Skill | What it does |
|-------|-------------|
| **Spending analysis** | Categorized trends, period-over-period comparisons, anomaly flagging |
| **Lever identification** | Scans spending for optimization opportunities ranked by impact |
| **Scenario modeling** | Combinatorial what-if modeling across multiple levers and time horizons |
| **Budget modeling** | Envelope, zero-based, or custom frameworks against actual data |
| **Debt payoff planning** | Avalanche vs. snowball with your actual balances, rates, and cash flow |
| **Net worth tracking** | Multi-account, multi-currency net worth over time |
| **Tax preparation** | Annual income/expense summaries organized by tax category |
| **Cash flow forecasting** | Forward-looking projections from recurring patterns |
| **Subscription audit** | Detect, list, and cost-analyze recurring charges; flag unused services |
| **CSV rules generation** | Analyze a bank CSV and generate import rules for the accounting engine |
| **Financial literacy coaching** | Personalized education modules grounded in the user's own data |

But the agent isn't limited to these. When you ask something the skill library doesn't cover, the agent writes a new analysis from scratch. If the analysis proves useful, it becomes a new skill. **The skill library is a living asset that grows as you use the system.**

### 3.3 The Agent Develops New Capabilities Through Conversation

One of the most powerful properties of an agentic coding agent is that it can build tools it doesn't have yet. A concrete example:

**The transaction splitting problem.** You shop at Costco twice a month. Each trip is one transaction. But ~85% is groceries and ~15% is household supplies. No existing tool -- not hledger, not Beancount, not Monarch -- lets you automatically split that transaction based on historical ratios.

```
User: "My Costco trips are mostly groceries but about 15% is usually
       household stuff like paper towels, cleaning supplies, etc."

Agent: [queries historical Costco transactions]
       [writes a post-processing script that splits Costco transactions
        85/15 between expenses:food:groceries and expenses:household]
       [adds it as a rule in the import pipeline]

       "Done. I'll split your Costco transactions 85/15 going forward.
        If a particular trip was different -- like that $280 one last month
        that was mostly a vacuum cleaner -- just tell me and I'll adjust
        that specific transaction and update the ratio if needed."
```

Over time, this generalizes:
- The 85/15 ratio refines as the user flags exceptions
- The pattern becomes a parameterized "proportional transaction splitting" skill applicable to any mixed-category merchant (Target, Amazon, Walmart)
- The skill is saved to the library for reuse

This is the fundamental advantage of an agentic coding agent over a feature-driven app. Apps have features or they don't. The agent develops capabilities through conversation.

### 3.4 The Accounting Engine: A Generic Subdomain

The agent doesn't care which accounting engine you use, as long as it provides structured, queryable financial data with mathematical integrity.

| Engine | Strengths | Best for |
|--------|-----------|----------|
| **hledger** | Best CSV import rules, robust CLI with JSON output, hledger-web API, most active development | Users who want the strongest import pipeline |
| **Beancount** | Strictest validation, Python extensibility, Fava web UI, growing AI ecosystem | Users who want Python-native scripting and Fava's UI |
| **Custom Python** | Maximum flexibility, no learning curve for Python developers | Users who prefer dataframes over journal files |

The agent adapts its query strategy to the engine. With hledger, it runs `hledger balance -O json`. With Beancount, it uses `bean-query`. With custom Python, it reads whatever data structures you've defined. The analysis layer is engine-agnostic.

### 3.5 Ingestion: Another Generic Subdomain

Getting data into the system should be easy but is not the core innovation. We integrate existing solutions:

| Method | Tools | Complexity |
|--------|-------|-----------|
| **CSV import** | hledger CSV rules (LLM-generated), Beancount importers | Low -- drop a file |
| **Bank sync** | Plaid (finfetch, plaid-cli, BeanHub Connect), Tiller Money | Medium -- one-time setup |
| **OFX/QFX** | ledger-autosync, ofxclient | Low -- download and import |
| **Manual entry** | hledger add, hledger-web, Fava, or natural language via agent | Trivial |
| **Receipt scanning** | Vision LLM (cloud or local) | Medium -- photo to transaction |

The agent helps with ingestion -- especially CSV rules generation, categorization of unknowns, and capabilities like transaction splitting that emerge through use. But ingestion is not the product. The product is what happens after the data is structured.

---

## 4. Market Context

No existing tool combines lever identification from actual spending data, combinatorial scenario modeling, and personalized coaching. The closest competitors (Origin Financial, Hiro) use pre-built planning models — they can answer "what if you save $300/month more?" but can't tell you *which* $300. Planning tools (ProjectionLab, Boldin) model parameters you define manually but never analyze your data to find the parameters. Dashboard apps (Monarch, YNAB) show where money went but can't model what to change.

The DIY version (Claude Code + hledger-mcp) proves the concept works but lacks validated computation, persistent skills, and accessibility beyond developers.

The competitive window is real but not permanent. Origin, Hiro, or Anthropic itself could move into this space.

Full analysis: [Competitive Analysis 2026](../competitive/competitive-analysis-2026.md) | Market research: [Personal Finance Landscape](../../research/personal-finance-landscape-2026.md)

---

## 5. Target Audience

### Primary: People Who Want to Understand Their Finances Deeply

Technically-literate individuals who:
- Want more than a dashboard -- they want analysis, modeling, and actionable scenarios grounded in their real data
- Are comfortable with (or willing to learn) CLI tools, but don't want to write every analysis script themselves
- Are at a financial inflection point (new job, buying a house, retirement planning, paying off debt) where deep analysis matters
- Value data ownership as a practical benefit (portability, longevity, no vendor risk)

### Secondary: Financial Literacy Learners

People who:
- Want to build genuine financial understanding, not just follow a budgeting app's rules
- Learn best from personalized, concrete examples (their own money) rather than generic advice
- Would benefit from an AI tutor that explains amortization, tax-loss harvesting, or compound growth using their actual numbers

### Adjacent: Existing PTA Users

hledger and Beancount users who already have structured financial data and want an intelligence layer on top. They're tired of writing one-off scripts for every analysis.

---

## 6. Value Proposition

### The One-Liner

> "A personal financial analyst that writes code against your structured accounting data -- opinionated enough to be useful out of the box, capable enough to model anything you can describe."

### For Different Audiences

**Coming from Monarch/YNAB/Copilot:**
> "Your budgeting app shows you pie charts. This shows you what to *do* -- identifies the specific levers in your spending, models different combinations, and helps you find the tradeoffs that fit your life."

**Coming from ProjectionLab/Boldin:**
> "Your planning tool models scenarios you define. This identifies the scenarios worth modeling by analyzing your actual spending data -- then models them computationally."

**Coming from hledger/Beancount:**
> "Keep your journals. Add an agent that queries them in English, identifies optimization opportunities you'd miss manually, and generates the analyses you've been meaning to build."

**Coming from ChatGPT Code Interpreter:**
> "Same analytical power, but with a persistent structured data layer, domain-specific skills, accumulated context, and validated computation. No re-uploading CSVs every session."

---

## 7. Usage Stories

These are illustrative scenarios -- what a session looks like for different people with different needs. They are not comprehensive user journeys (which would cover discovery, onboarding, first-value moments, habit formation, and expansion over time). They show the breadth of what the agent does once someone is already using it.

Each story enters the core loop (Section 2) at a different point, but all share the same foundation: structured data, code-executed analysis, and personalized interpretation.

### 7.1 "Where did my money go?" — The Monthly Surprise

**Maya, 31, product manager.** She checks her bank app and her savings balance is $200 less than she expected.

```
Maya:  "Why am I short $200 this month compared to last month?"

Agent: [queries hledger: register expenses -p "this month" vs "last month"]
       [executes Python diff analysis across categories]

       Your total spending this month is $4,180 vs. $3,940 last month (+$240).
       Three categories explain the difference:

       ┌─────────────────────┬──────────┬──────────┬─────────┐
       │ Category            │ This Mo. │ Last Mo. │ Change  │
       ├─────────────────────┼──────────┼──────────┼─────────┤
       │ food:dining-out     │   $620   │   $410   │  +$210  │
       │ transport:rideshare │   $185   │   $130   │  +$55   │
       │ shopping:clothing   │   $290   │   $340   │  -$50   │
       └─────────────────────┴──────────┴──────────┴─────────┘

       Dining accounts for almost all of it — 14 restaurant transactions
       this month vs. 8 last month.

Maya:  "Is this a trend or a one-off?"

Agent: [executes 6-month rolling average analysis]

       Your 6-month dining average is $440/month. This month ($620) is
       1.4σ above your norm — notable but not your highest (February
       was $680). However, the trend is upward:

       $380 → $410 → $440 → $620 over the last four months.

       If this trajectory holds, you're looking at ~$700/month by summer.
```

**What this illustrates:** The agent doesn't show a dashboard and wait — it identifies the specific driver, contextualizes it historically, and quantifies the trajectory. The user entered the loop at "analysis" and got coaching without asking for it.

### 8.2 "What's this charge?" — The Subscription Audit

**Priya, 35, freelance designer.** She notices a $14.99 charge she doesn't recognize and decides to clean house.

```
Priya:  "What is this DGTL*MBRSHP charge for $14.99? And while you're
         at it, audit all my subscriptions."

Agent:  [queries for recurring patterns matching DGTL*MBRSHP]
        [executes subscription detection: regex on merchant names +
         recurring amount/interval detection]

        DGTL*MBRSHP has been recurring monthly since August 2025
        ($14.99 × 7 = $104.93 total). Common matches: MasterClass,
        Skillshare, or a news site. Check your email for a welcome
        receipt around Aug 3, 2025.

        Full subscription audit:

        ┌──────────────────────┬─────────┬───────────┬─────────────────┐
        │ Service              │ Monthly │ Since     │ Status          │
        ├──────────────────────┼─────────┼───────────┼─────────────────┤
        │ Spotify Family       │  $16.99 │ Jan 2023  │ Active          │
        │ iCloud+ 200GB        │   $2.99 │ Mar 2023  │ Active          │
        │ Adobe CC Photography │  $10.99 │ Jun 2023  │ Low usage       │
        │ DGTL*MBRSHP          │  $14.99 │ Aug 2025  │ Unidentified    │
        │ Netflix Standard     │  $17.99 │ Feb 2022  │ Active          │
        │ Figma Professional   │  $15.00 │ Sep 2024  │ Active (work)   │
        │ YouTube Premium      │  $13.99 │ Nov 2023  │ Active          │
        │ Duolingo Plus        │   $6.99 │ Jan 2025  │ Low usage       │
        │ NYT All Access       │   $4.00 │ Apr 2024  │ Active          │
        └──────────────────────┴─────────┴───────────┴─────────────────┘

        Total: $103.93/month ($1,247/year)

        Flagged for review:
        • Adobe CC — last identifiable usage was Oct 2025.
        • Duolingo Plus — small charge, worth confirming usage.
        • DGTL*MBRSHP — identify this one. If unused, that's $180/year.

        Canceling the three flagged items saves $32.97/month ($396/year).
```

**What this illustrates:** A simple "what's this charge?" turns into a broader audit. This is also the kind of analysis that starts as agent-generated code and graduates into the skill library once the subscription-detection pattern is validated.

### 8.3 "Tax time" — The Annual Summary

**Marcus, 42, freelancer + part-time W2.** It's March and his accountant needs a summary.

```
Marcus: "I need my tax prep summary for 2025. I have W2 income from
         Acme Corp, freelance 1099 income, and home office expenses."

Agent:  [queries hledger for full-year income and expense by tax category]
        [executes categorization validation + Schedule C allocation]

        2025 Tax Preparation Summary
        ════════════════════════════

        INCOME
        ┌────────────────────────┬────────────┬─────────────┐
        │ Source                 │ Amount     │ Tax Form    │
        ├────────────────────────┼────────────┼─────────────┤
        │ Acme Corp (W2)         │ $68,400.00 │ W-2         │
        │ Freelance clients (4)  │ $41,250.00 │ 1099-NEC    │
        │ Interest income        │    $342.18 │ 1099-INT    │
        ├────────────────────────┼────────────┼─────────────┤
        │ Total                  │$109,992.18 │             │
        └────────────────────────┴────────────┴─────────────┘

        SCHEDULE C — BUSINESS EXPENSES
        ┌────────────────────────┬────────────┬─────────────┐
        │ Category               │ Amount     │ Notes       │
        ├────────────────────────┼────────────┼─────────────┤
        │ Home office (sq ft)    │  $3,840.00 │ 200/1100 sf │
        │ Software & tools       │  $1,439.88 │ 12 services │
        │ Professional dev       │    $890.00 │ 2 courses   │
        │ Hardware               │  $2,149.00 │ MacBook Pro │
        │ Internet (biz %)       │    $540.00 │ 45% alloc   │
        ├────────────────────────┼────────────┼─────────────┤
        │ Total deductions       │  $8,858.88 │             │
        └────────────────────────┴────────────┴─────────────┘

        Review flags:
        • 3 transactions ($1,240) tagged "expenses:professional"
          look personal (Best Buy, Amazon). Please confirm.
        • Home office % (18.2%) is within safe harbor range.
        • Estimated quarterly payments made: $3,200 total. Freelance
          liability estimate is ~$8,400. You may be underpaid by ~$5,200.

        Want me to generate this as a PDF for your accountant, or
        export to a spreadsheet?
```

**What this illustrates:** Tax preparation demands exact numbers, correct allocations, and zero hallucination. Every row traces back to code executed against Marcus's structured journal — the agent queries, computes, and flags problems rather than summarizing from memory.

### 8.4 "I want an emergency fund" — The Goal Seeker

This is the same archetype as the core example in Section 2, from a slightly different angle. Jordan (27, software engineer, hledger user) asks for help building a 3-month emergency fund. The agent:

1. Calculates the gap ($5,400 needed)
2. Scans spending for 5 ranked levers (dining trend, unused subscriptions, insurance requote, grocery brand switching, coffee shops)
3. Models 4 scenarios from low-effort ($47/month saved, 9.5 months) to aggressive ($387/month, 3.1 months)
4. Jordan says "Scenario B, but I can't cut dining that much"
5. Agent re-models with adjusted parameter — $137/month, 6.6 months, target date September

**What this illustrates:** The full core loop in a single session — analysis, lever identification, scenario modeling, interactive refinement, plan commitment. The user enters at "goal-setting" rather than "something feels off."

### 8.5 "Life is changing" — The Big Decision

**Sam & Alex, couple.** Alex got a job offer in Denver ($95K vs. current $82K in Austin). Rent is $2,100 in Austin.

```
Sam:    "What does a move to Denver look like financially?"

Agent:  [queries current spending baseline from hledger]
        [executes cost-of-living adjustment model]
        [executes relocation cost estimation]

        CURRENT BASELINE (Austin, last 12 months)
        Combined income:    $154,000/year ($12,833/month)
        Total spending:     $9,240/month
        Current savings:    $3,593/month

        DENVER SCENARIO
        ┌────────────────────────┬──────────┬──────────┬──────────┐
        │ Category               │ Austin   │ Denver   │ Delta    │
        ├────────────────────────┼──────────┼──────────┼──────────┤
        │ Gross income (combined)│ $12,833  │ $13,917  │ +$1,084  │
        │ After-tax income*      │ $10,450  │ $11,180  │  +$730   │
        │ Rent (comparable area) │  $2,100  │  $2,550  │  +$450   │
        │ Groceries (CoL adj)    │    $680  │    $720  │   +$40   │
        │ Auto insurance         │    $178  │    $155  │   -$23   │
        │ Other (unchanged)      │  $6,092  │  $6,092  │    $0    │
        ├────────────────────────┼──────────┼──────────┼──────────┤
        │ Net monthly savings    │  $3,210  │  $3,453  │  +$243   │
        └────────────────────────┴──────────┴──────────┴──────────┘
        * CO has 4.4% flat state tax vs. TX 0%, factored in.

        RELOCATION COSTS (one-time): ~$11,100
        BREAK-EVEN: 3.8 years at +$243/month net improvement.

Sam:    "What if we negotiate to $100K?"

Agent:  [re-models]

        At $100K: net improvement becomes +$570/month.
        Break-even drops to 1.6 years. Monthly savings: $3,780.

        That's an extra $6,840/year. Invested at 7% over 5 years,
        that's roughly $39,500 in additional wealth.

        The $5K salary negotiation is worth ~$39K over 5 years.
```

**What this illustrates:** Life-event modeling that composes multiple analysis types — baseline extraction from real data, cost-of-living adjustment, tax modeling, relocation costing, break-even analysis, and investment projection. This is Phase 3 territory, but built from Phase 1 and 2 primitives.

### What ties these stories together

Every story follows the same core loop, entered at a different point:

| Story | Entry point | Core loop stages exercised |
|-------|-------------|---------------------------|
| Maya (monthly surprise) | Analysis | Analysis → Coaching |
| Priya (subscription audit) | A specific charge | Analysis → Lever identification |
| Marcus (tax prep) | Reporting need | Analysis → Output |
| Jordan (emergency fund) | Goal | Analysis → Levers → Scenarios → Refinement |
| Sam & Alex (relocation) | Life event | Analysis → Scenarios → Refinement |

The agent grounds every response in structured data queried and analyzed through code. The difference between these stories and what a chatbot produces is that every number in every table traces back to an executed query or calculation.

---

## 8. Architecture Principles

### 8.1 The Agent Writes Code; Code Does Math

The LLM never performs arithmetic directly. When analysis requires computation, the agent writes and executes code (Python, SQL, shell scripts) that queries the accounting engine and performs calculations in a standard runtime (pandas, numpy, etc.).

LLMs are unreliable at math. Code is not. The agent's job is to translate intent into correct code. Novel analyses use agent-generated code (reliable but review-worthy); common analyses use battle-tested skill code (reviewed, tested, and reused). The skill library is the bridge between the two -- novel code that proves useful graduates into trusted skills over time.

### 8.2 Opinionated Defaults, Escape Hatches Everywhere

The skill library ships with strong opinions: preferred chart of accounts structures, recommended budgeting frameworks, standard report formats, lever identification heuristics. These opinions are explicitly documented, clearly justified, and easily overridden.

The agent should be useful in the first five minutes. It should also never prevent a power user from doing something unusual.

### 8.3 The Skill Library Is a First-Class Asset

Skills encode domain knowledge, analytical methodologies, output templates, and validation logic. The skill library is:
- **Version-controlled** alongside the user's financial data
- **Composable** -- skills can invoke other skills (lever identification feeds into scenario modeling)
- **Self-extending** -- the agent can draft new skills from novel analyses (like the transaction splitting example)
- **Shareable** -- users can publish and import community skills

### 8.4 Accounting Engine Agnosticism

The agent communicates with the accounting engine through a defined interface, not direct file manipulation. Switching from hledger to Beancount doesn't require rewriting skills. Users with custom Python data pipelines can integrate without adopting PTA.

### 8.5 Human-in-the-Loop for Data Writes; Autonomous for Analysis

The agent freely reads data, runs analyses, generates reports, and builds dashboards without approval -- these are read-only operations with no risk. Write operations (adding transactions, modifying journal entries) require human approval by default.

---

## 9. Core Capabilities in Detail

### 9.1 Lever Identification and Scenario Modeling

This is the central capability -- the thing no existing tool provides.

**Lever identification** means the agent systematically scans your financial data and surfaces specific, concrete opportunities for change:
- Spending categories trending upward (dining out +34% YoY)
- Recurring charges with zero usage (subscription audit)
- Above-median costs for your profile (insurance, utilities, groceries)
- Mixed-category transactions that could be better categorized (the Costco 85/15 split)
- Timing optimization (paying credit cards before interest accrues, timing large purchases)

**Scenario modeling** means the agent takes combinations of levers and models their compound effects:
- Not "what if you save $300/month more" but "what if you pull levers #1, #3, and #7 -- here's the compound effect over 6/12/24 months, including debt payoff acceleration and investment growth"
- Multiple scenarios side by side, each with different lever combinations
- Interactive refinement: "Lever #3 doesn't feel realistic for me. What if I do half of that and add lever #5 instead?"
- Time-aware modeling: some changes are immediate (cancel a subscription), some ramp (gradually reduce dining out), some are one-time (refinance a loan)

**The synthesis** is what makes this more than a calculator: the agent connects levers to goals, models the combinations computationally, and coaches the user through the tradeoffs until they converge on a plan that fits their life.

### 9.2 Financial Analysis via Code Execution

The agent's primary mode of operation for any question: translate it into executable analysis.

```
User: "I'm thinking about switching from renting ($2,400/mo) to buying
       a condo. What price range makes sense?"

Agent: [queries accounting engine for income, expenses, savings, existing debt]
       [writes Python: mortgage calculator with PMI, property tax, insurance,
        HOA estimates, opportunity cost of down payment, comparison to renting
        with investment of the difference]
       [generates interactive chart showing buy-vs-rent breakeven by price point]
       [delivers analysis with specific range based on user's actual numbers]
```

```
User: "Something feels off with my spending this month."

Agent: [queries current month vs. trailing 6-month averages by category]
       [writes anomaly detection: z-scores by category, new merchants,
        unusual amounts, new recurring charges]
       [flags specifics with context and asks for clarification]
```

### 9.3 Financial Literacy Coaching

Not generic tips -- personalized education grounded in the user's actual data.

```
User: "I keep hearing about the 'avalanche method' for debt. Is it
       actually better for me?"

Agent: [queries all debt accounts: balances, rates, minimum payments]
       [models both avalanche (highest rate first) and snowball (smallest
        balance first) with the user's actual debts]

       "With your debts, avalanche saves you $1,340 in interest and pays
        off 2 months faster. But here's the tradeoff: with snowball, you
        eliminate your $800 store card in 3 months, which frees up $45/mo
        of cash flow sooner. With avalanche, your first payoff isn't until
        month 9.

        Given your emergency fund is still building, the early cash flow
        from snowball might matter more than the $1,340 saved. Here's what
        both paths look like month by month..."
```

The coaching adapts to the user's level -- explains concepts when they're new, skips the explanation for returning users.

### 9.4 Multi-Format Output

The same analysis can be delivered as:

| Format | Use case |
|--------|----------|
| **Chat** | Quick questions, iterative exploration, scenario refinement |
| **Dashboard** | Ongoing monitoring (spending trends, net worth, budget vs. actual) |
| **Slide deck** | Quarterly reviews, sharing with a partner or financial advisor |
| **PDF report** | Tax preparation, loan applications, formal documentation |
| **Excel/CSV** | Further analysis in external tools, sharing raw data |
| **Interactive notebook** | Deep dives with adjustable assumptions |

### 9.5 Self-Extending Skill Library

When the agent builds a novel analysis, it can be saved as a reusable, parameterized skill. Skills compose: lever identification feeds into scenario modeling, which feeds into tracking. The library is the compound advantage -- it gets more valuable with every interaction.

---

## 10. Phased Delivery

### Phase 0: Foundation (Current)

- Project scaffolding, documentation infrastructure, and vision
- Research spikes for key technical decisions
- Agent skill library structure (`.agents/skills/`)

### Phase 1: Analyst (Core Loop)

Build the core analysis loop: structured data in, code-executed analysis out.

- Accounting engine integration (hledger first, Beancount second)
- MCP server exposing accounting data to the agent
- Core skill library: spending analysis, net worth, cash flow, basic lever identification
- Code execution for custom analyses
- Chat-based interaction as primary interface
- CSV ingestion with LLM-assisted rules generation

**Success gate:** User asks a financial question, agent queries structured data, writes and executes analysis code, and delivers a grounded answer with visualization.

### Phase 2: Coach + Scenario Modeler

The phase where the core loop (Section 2) comes together.

- Lever identification skill: systematic scanning of spending for optimization opportunities
- Scenario modeling skill: combinatorial what-if modeling across levers and time horizons
- Interactive scenario refinement (adjust levers, re-model, converge)
- Financial literacy coaching skills (personalized to user data)
- Multi-format output: dashboards, slide decks, PDF reports
- Anomaly detection and proactive insights
- Skill self-extension: agent develops new capabilities through conversation
- Automated bank sync integration (Plaid / existing tools)

**Success gate:** User identifies a financial goal, agent surfaces concrete levers from their data, models multiple scenarios, and helps them converge on a plan -- with all computations validated by code execution.

### Phase 3: Advisor

Graduate from reactive analysis to proactive, strategic guidance.

- Life event modeling (career change, home purchase, retirement, children)
- Tax preparation and optimization
- Investment allocation analysis (with appropriate disclaimers)
- Tracking and drift detection against committed plans
- Community skill marketplace (share and import skills)
- Web/mobile interfaces for non-CLI users

**Success gate:** User navigates a major financial decision with agent-generated analysis that a professional financial planner would consider substantive.

---

## 11. Success Metrics

| Metric | Target | Rationale |
|--------|--------|-----------|
| Analysis grounding | 100% of numerical claims traceable to code execution | The agent never guesses numbers |
| Lever identification | Surfaces actionable levers the user hadn't identified | Must provide genuine insight, not obvious observations |
| Scenario accuracy | All scenarios reproducible by re-running generated code | Scenarios must be verifiable, not vibes |
| Time to first insight | < 10 min from initial setup | Must feel immediately valuable |
| Plan convergence | User converges on a plan within one interactive session | The scenario refinement loop must be tight |
| Skill library growth | Core skills + user-generated skills accumulate over time | System gets more valuable with use |

---

## 12. Non-Goals

- **Building an accounting engine.** hledger, Beancount, and custom Python handle this.
- **Building an ingestion pipeline from scratch.** Plaid, hledger CSV rules, BeanHub Connect handle this. We make ingestion easier but don't own it.
- **Replacing professional financial advice.** The agent provides analysis and education, not fiduciary advice. It should help users have better conversations with real advisors, not replace them.
- **Competing on UI with Monarch or Copilot.** We generate dashboards and slides as output, but we're not building a polished consumer finance app.
- **Replicating ProjectionLab's UI.** ProjectionLab's dedicated retirement planning interface is polished and deep. We don't need to rebuild that UI. But the agent should absolutely know how and when to run a Monte Carlo simulation, model Roth conversions, or project retirement trajectories -- these are techniques in the agent's toolkit, applied when the user's question calls for them.
- **Building a fintech product.** No payment processing, lending, or financial product recommendations.
- **Requiring local-only deployment.** Local LLMs are supported for data-sensitive operations like categorization. But the core analysis loop benefits from frontier model quality. Cloud LLMs are a first-class option.

---

## 13. Risks and Open Questions

| Risk | Severity | Mitigation |
|------|----------|------------|
| Agent generates incorrect financial analysis | High | All numerical work is code-executed and verifiable. Agent shows its work. User can inspect and re-run. |
| Users over-trust agent's financial suggestions | High | Explicit disclaimers. Frame as "analysis" not "advice." Encourage professional consultation for major decisions. |
| Origin/Hiro adds lever identification | High | Move fast on the core capability. Open-source self-extending skills are hard to replicate in a closed product. |
| The DIY version is "good enough" | Medium | For developers, it might be. The product thesis is that packaging matters -- reliable skills, validated computation, and accessibility beyond the developer audience. |
| Scope creep toward "building an app" | Medium | This document. The core domain is the agent + skills. Everything else is integration. |
| Frontier model cost for heavy use | Low | Most interactions require one code execution cycle. Caching and skill reuse reduce redundant calls. |

### Open Questions (candidates for Research Spikes)

1. **SPIKE: Lever Identification Methodology** -- How should the agent systematically identify financial levers? What heuristics, benchmarks, and data patterns produce actionable (not obvious) suggestions?
2. **SPIKE: Scenario Modeling Engine** -- How should scenario modeling balance pre-built, tested computation (like ProjectionLab's models) with dynamically generated code (for novel analyses)? The skill library is the answer in principle -- but what's the right process for graduating ad-hoc analysis code into trusted skill code?
3. **SPIKE: Accounting Engine Interface Design** -- What's the right abstraction layer for engine-agnostic queries?
4. **SPIKE: Skill Specification Format** -- How should skills encode domain knowledge, parameters, validation, and output templates?
5. **SPIKE: Dashboard Generation** -- What's the right approach for agent-generated interactive dashboards? Streamlit, Observable, static HTML?
6. **SPIKE: Coaching Curriculum Design** -- How should financial literacy coaching be structured? Linear progression, topic-based, or reactive to user questions?

---

## Appendix A: Why Now

1. **The architecture is proven.** Claude for Financial Services demonstrates that frontier LLM + code execution + structured data + domain Skills works for finance. The question is whether anyone builds the personal version.
2. **The building blocks exist.** hledger-mcp, beanquery-mcp, Plaid integrations, and MCP provide the integration layer. The infrastructure cost of this project is low.
3. **The competitive window is open.** Origin and Hiro are focused on general financial advising, not lever identification from structured data. ProjectionLab has no AI. The DIY version works but isn't a product. Nobody has assembled the pieces.
4. **Demand is validated.** 37% of Americans use AI for financial tasks (BMO/Ipsos). r/plaintextaccounting users are already building ad-hoc versions. hledger-mcp has strong community adoption. The demand is real.
5. **The window could close.** Origin, Hiro, or Anthropic itself could move into this space. The advantage of starting now is building the skill library -- the self-extending, compound asset that gets harder to replicate the longer it grows.
