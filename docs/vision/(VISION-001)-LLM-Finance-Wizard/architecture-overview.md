---
title: "Architecture Overview — LLM Finance Wizard"
type: Vision supporting document
parent: "VISION-001: LLM Finance Wizard"
author: cristos
created: 2026-02-26
last_updated: 2026-02-26
---

# Architecture Overview

This document describes how the system works holistically — the shape of the system, not individual decisions. For discrete architectural decisions (chose X over Y because Z), see ADRs.

Extracted from VISION-001 to keep the vision focused on *what* and *why*.

---

## 1. How the Agent Works

### 1.1 Code Execution, Not Chat Completion

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

### 1.2 Opinionated Defaults, Extensible by Design

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

### 1.3 The Agent Develops New Capabilities Through Conversation

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

### 1.4 The Accounting Engine: A Generic Subdomain

The agent doesn't care which accounting engine you use, as long as it provides structured, queryable financial data with mathematical integrity.

| Engine | Strengths | Best for |
|--------|-----------|----------|
| **hledger** | Best CSV import rules, robust CLI with JSON output, hledger-web API, most active development | Users who want the strongest import pipeline |
| **Beancount** | Strictest validation, Python extensibility, Fava web UI, growing AI ecosystem | Users who want Python-native scripting and Fava's UI |
| **Custom Python** | Maximum flexibility, no learning curve for Python developers | Users who prefer dataframes over journal files |

The agent adapts its query strategy to the engine. With hledger, it runs `hledger balance -O json`. With Beancount, it uses `bean-query`. With custom Python, it reads whatever data structures you've defined. The analysis layer is engine-agnostic.

### 1.5 Ingestion: Another Generic Subdomain

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

## 2. Architecture Principles

### 2.1 The Agent Writes Code; Code Does Math

The LLM never performs arithmetic directly. When analysis requires computation, the agent writes and executes code (Python, SQL, shell scripts) that queries the accounting engine and performs calculations in a standard runtime (pandas, numpy, etc.).

LLMs are unreliable at math. Code is not. The agent's job is to translate intent into correct code. Novel analyses use agent-generated code (reliable but review-worthy); common analyses use battle-tested skill code (reviewed, tested, and reused). The skill library is the bridge between the two -- novel code that proves useful graduates into trusted skills over time.

### 2.2 Opinionated Defaults, Escape Hatches Everywhere

The skill library ships with strong opinions: preferred chart of accounts structures, recommended budgeting frameworks, standard report formats, lever identification heuristics. These opinions are explicitly documented, clearly justified, and easily overridden.

The agent should be useful in the first five minutes. It should also never prevent a power user from doing something unusual.

### 2.3 The Skill Library Is a First-Class Asset

Skills encode domain knowledge, analytical methodologies, output templates, and validation logic. The skill library is:
- **Version-controlled** alongside the user's financial data
- **Composable** -- skills can invoke other skills (lever identification feeds into scenario modeling)
- **Self-extending** -- the agent can draft new skills from novel analyses (like the transaction splitting example)
- **Shareable** -- users can publish and import community skills

### 2.4 Accounting Engine Agnosticism

The agent communicates with the accounting engine through a defined interface, not direct file manipulation. Switching from hledger to Beancount doesn't require rewriting skills. Users with custom Python data pipelines can integrate without adopting PTA.

### 2.5 Human-in-the-Loop for Data Writes; Autonomous for Analysis

The agent freely reads data, runs analyses, generates reports, and builds dashboards without approval -- these are read-only operations with no risk. Write operations (adding transactions, modifying journal entries) require human approval by default.

---

## 3. Core Capabilities in Detail

### 3.1 Lever Identification and Scenario Modeling

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

### 3.2 Financial Analysis via Code Execution

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

### 3.3 Financial Literacy Coaching

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

### 3.4 Multi-Format Output

The same analysis can be delivered as:

| Format | Use case |
|--------|----------|
| **Chat** | Quick questions, iterative exploration, scenario refinement |
| **Dashboard** | Ongoing monitoring (spending trends, net worth, budget vs. actual) |
| **Slide deck** | Quarterly reviews, sharing with a partner or financial advisor |
| **PDF report** | Tax preparation, loan applications, formal documentation |
| **Excel/CSV** | Further analysis in external tools, sharing raw data |
| **Interactive notebook** | Deep dives with adjustable assumptions |

### 3.5 Self-Extending Skill Library

When the agent builds a novel analysis, it can be saved as a reusable, parameterized skill. Skills compose: lever identification feeds into scenario modeling, which feeds into tracking. The library is the compound advantage -- it gets more valuable with every interaction.

---

## 4. The Three-Layer Architecture

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
