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
| Draft | 2026-02-26 | -- | Complete rewrite: reframed around agentic coding agent as core domain |

---

# LLM Finance Wizard

**A frontier-level agentic coding agent for personal finance -- opinionated, self-extending, and grounded in structured accounting data.**

---

## 1. The Problem

Personal finance tools in 2026 fall into three camps, and none of them give you what a competent financial analyst would:

**The polished dashboards (Monarch, YNAB, Copilot, Quicken Simplifi)** show you where your money went. They categorize transactions, render charts, and some now offer AI-powered summaries. But they can't *analyze*. Ask "Should I pay off my student loans faster or invest the difference?" and you'll get a generic chatbot answer, not a computation grounded in your actual cash flows, tax bracket, and loan terms. The AI features in these tools are shallow -- classification and summarization, not analysis and reasoning.

**The plain-text accounting tools (hledger, Beancount, Ledger-CLI)** give you a rigorous, programmable data foundation. You can write queries, script reports, and version-control your financial history. But the burden falls entirely on you: you write every import rule, every report query, every analysis script. The data is structured and sovereign, but extracting insight from it requires accounting knowledge AND programming skill -- a combination most people don't have.

**General-purpose AI (ChatGPT Code Interpreter, Claude)** can analyze financial data brilliantly -- when you manually export CSVs, upload them, explain the schema, and prompt carefully. But there's no persistence, no structured data layer, no accumulated context, and no domain-specific skills. Every session starts from zero. And the AI does its own math, which the FinNLP 2025 paper (ACL Anthology) showed is unreliable: *"LLMs struggle severely with accounting, often producing inaccurate calculations."*

**The gap:** No tool combines a structured accounting engine (for mathematical integrity) with a frontier-level agentic coding agent (for intelligence and analysis) with an opinionated, growing skill library (for practical financial wisdom). That's what LLM Finance Wizard builds.

---

## 2. The Vision

LLM Finance Wizard is a **personal AI financial analyst** -- an agentic coding agent that sits on top of structured accounting data and helps you understand, manage, and improve your financial life.

The agent:
- **Writes and executes code** for numerical computation, analysis, and visualization -- it doesn't do math in its head
- **Queries structured accounting data** through the accounting engine (hledger, Beancount, or custom scripts) for mathematical integrity
- **Ships with opinionated, battle-tested skills** for common financial tasks: budgeting analysis, spending trends, debt payoff modeling, tax preparation, net worth tracking
- **Builds new skills and tools on the fly** when your situation demands something the defaults don't cover
- **Coaches you on financial literacy** -- not generic advice, but personalized education grounded in your actual financial data
- **Delivers insights in whatever format serves you** -- conversational chat, interactive dashboards, slide decks, PDF reports, Excel exports

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

**The core domain is the agent and its skill library.** The accounting engine and ingestion pipeline are generic subdomains -- important, but solved problems that we integrate rather than reinvent. hledger, Beancount, Plaid, CSV importers -- these are mature tools. We leverage them; we don't rebuild them.

The differentiated value is the agent's **judgment** (opinionated defaults), **capability** (frontier-level code execution), and **growth** (the skill library improves with use).

---

## 3. How the Agent Works

### 3.1 Code Execution, Not Chat Completion

When you ask "Am I saving enough for retirement?", the agent doesn't generate a text answer. It:

1. **Queries the accounting engine** for your income, expenses, savings rate, and investment balances
2. **Writes a Python script** that models compound growth scenarios using your actual numbers, tax bracket, and stated retirement age
3. **Executes the script** and generates a visualization of outcomes
4. **Interprets the results** in plain language with specific, actionable recommendations
5. **Optionally packages the analysis** as a dashboard panel, a slide in a quarterly review deck, or a PDF you can share with a financial planner

The LLM provides intelligence. The code provides numerical accuracy. The accounting engine provides data integrity. Each layer does what it's best at.

### 3.2 Opinionated Defaults, Extensible by Design

The agent ships with a core library of battle-tested skills:

| Skill | What it does |
|-------|-------------|
| **Spending analysis** | Categorized spending trends, period-over-period comparisons, anomaly flagging |
| **Budget modeling** | Envelope budgeting, zero-based budgeting, or custom frameworks against actual data |
| **Debt payoff planning** | Avalanche vs. snowball modeling with your actual balances and rates |
| **Net worth tracking** | Multi-account, multi-currency net worth over time with visualizations |
| **Tax preparation** | Annual income/expense summaries organized by tax category |
| **Cash flow forecasting** | Forward-looking projections based on recurring patterns |
| **Subscription audit** | Detect, list, and cost-analyze recurring charges |
| **CSV rules generation** | Analyze a bank CSV and generate hledger/Beancount import rules |
| **Financial literacy coaching** | Personalized education modules grounded in the user's own data |

But the agent isn't limited to these. When you ask something the skill library doesn't cover -- "Model the impact of refinancing my mortgage at 5.2% vs. investing the closing costs in index funds" -- the agent writes a new analysis from scratch, using its coding capability and financial domain knowledge. If the analysis is useful enough to reuse, it can be saved as a new skill.

**The skill library is a living asset.** It grows as you use the system. Core skills are curated and battle-tested; user-generated skills accumulate alongside them.

### 3.3 The Accounting Engine: A Generic Subdomain

The agent doesn't care which accounting engine you use, as long as it provides:
- Structured, queryable financial data (transactions, accounts, balances)
- Mathematical integrity (double-entry validation, balance checking)
- A CLI or API the agent can invoke programmatically

**Supported engines (planned):**

| Engine | Strengths | Best for |
|--------|-----------|----------|
| **hledger** | Best CSV import rules, robust CLI with JSON output, hledger-web API, most active development | Users who want the strongest import pipeline |
| **Beancount** | Strictest validation, Python extensibility, Fava web UI, growing AI ecosystem | Users who want Python-native scripting and Fava's UI |
| **Custom Python** | Maximum flexibility, no learning curve for Python developers | Users who prefer dataframes over journal files |

The agent adapts its query strategy to the engine. With hledger, it runs `hledger balance -O json`. With Beancount, it uses `bean-query`. With custom Python, it reads whatever data structures you've defined. The analysis layer is engine-agnostic.

### 3.4 Ingestion: Another Generic Subdomain

Getting data into the system should be easy but is not the core innovation. We integrate existing solutions:

| Method | Tools | Complexity |
|--------|-------|-----------|
| **CSV import** | hledger CSV rules (LLM-generated), Beancount importers | Low -- drop a file |
| **Bank sync** | Plaid (via finfetch, plaid-cli, BeanHub Connect), Tiller Money | Medium -- one-time setup |
| **OFX/QFX** | ledger-autosync, ofxclient | Low -- download and import |
| **Manual entry** | hledger add, hledger-web, Fava, or natural language via agent | Trivial |
| **Receipt scanning** | Vision LLM (cloud or local) | Medium -- photo to transaction |

The agent helps with ingestion (especially CSV rules generation and categorization of unknowns), but ingestion is not the product. The product is what happens after the data is structured.

---

## 4. Market Landscape

### 4.1 What Exists Today

The research for this vision included extensive analysis of the current market. Here's an honest assessment:

#### Commercial Finance Apps (Monarch, YNAB, Copilot, Quicken Simplifi)

**What they do well:** Beautiful UIs, automatic bank sync via Plaid, solid categorization (Monarch and Copilot now use LLMs for this), and Monarch has shipped an AI assistant for basic Q&A.

**Where they stop:** These tools show you data but don't analyze it computationally. Monarch's AI assistant can tell you your spending by category, but it can't model a debt payoff strategy or forecast the impact of a career change on your savings trajectory. They're dashboards with a chatbot, not analytical engines. They also lock your data in proprietary cloud systems -- Mint's March 2024 shutdown and Empower's 2025 migration degradation are cautionary tales.

**Our relationship to them:** These are fine products for people who want a simple dashboard. We serve users who want more depth.

#### Plain-Text Accounting Tools (hledger, Beancount, Ledger-CLI)

**What they do well:** Mathematically rigorous, fully sovereign, programmable, and version-controllable.

**Where they stop:** No intelligence layer. All analysis must be hand-coded by the user. The learning curve is steep and the community is small.

**Our relationship to them:** These are our accounting engines. We build on top of them, not instead of them.

#### General-Purpose AI with Code Execution (ChatGPT Code Interpreter, Claude Analysis Tool)

**What they do well:** Brilliant at ad-hoc financial analysis when given the right data and prompts. ChatGPT Code Interpreter can write Python to analyze an uploaded CSV, generate charts, and even produce PowerPoint slides.

**Where they stop:** No persistence (data vanishes between sessions). No structured accounting engine (the LLM does its own math, unreliably). No domain-specific skills. No accumulated context about your financial situation. Every interaction starts from zero.

**Our relationship to them:** These prove the concept. They demonstrate that LLM + code execution + financial data = powerful analysis. We add the missing pieces: persistence, structured data, opinionated skills, and a growing knowledge base.

#### AI Financial Coaching Apps (Cleo, Kiro, SoLo IQ, Tendi)

**What they do well:** Cleo's personality-driven nudges engage younger users. SoLo IQ connects to real bank data for personalized advice.

**Where they stop:** Chat-only, no code execution, no deep analysis. The "coaching" is generic tips and behavioral nudges, not substantive computation against your actual financial situation.

**Our relationship to them:** Different market. These are engagement tools for people who need motivation. We're an analytical tool for people who want understanding.

#### The Closest Analog: Claude for Financial Services

Anthropic's Claude for Financial Services is the most architecturally similar existing product. It offers:
- 11 specialized Skills (DCF models, pitch books, equity research)
- Data connectors via MCP (Daloopa, Aiera, Chronograph)
- Code execution for all Skills
- Multi-format output (Excel, PowerPoint, chat)

**But it targets institutional finance** -- investment banks, hedge funds, asset managers. The Skills build DCF models and earnings previews, not spending analyses and debt payoff plans. The data sources are SEC filings and market data, not bank transactions and credit card statements.

Every.to's "Claude Code for Finance" workshops ($5,000/person) teach this same architecture to investment professionals.

**Our relationship to it:** Same architecture, different market. LLM Finance Wizard is "Claude for Financial Services, but for your personal finances." We're translating the institutional pattern to the individual.

### 4.2 What Doesn't Exist

No product today combines:

1. A **structured accounting engine** (for data integrity and mathematical rigor)
2. A **frontier LLM that writes and executes analysis code** (not just chat, actual computation)
3. An **opinionated, self-extending skill library** (battle-tested defaults + build-on-the-fly capability)
4. **Financial literacy coaching** personalized to the user's own data
5. **Multi-format output** (chat, dashboards, slides, PDFs, Excel)

The individual components all exist. The integrated product does not.

#### Partial Implementations Worth Watching

| Project | What it does | What's missing |
|---------|-------------|----------------|
| **hledger-mcp** | MCP server wrapping hledger CLI (40+ tools) for Claude Desktop | No code execution, no skills, no coaching |
| **beanquery-mcp** | Experimental MCP server for BQL queries against Beancount | Query-only, no code execution, very early |
| **Beanborg** | AI categorization for Beancount (ChatGPT fallback) | Categorization only, no analysis |
| **beancount.io** | Markets "AI-assisted insights" with Beancount | Marketing the vision; hasn't shipped AI features |
| **BeanHub** | Plaid + Beancount + Git; announced MCP plans | Ingestion/data layer, no analysis agent |
| **Fava Dashboards** | Code-defined dashboards for Beancount via ECharts/D3 | Dashboard output, but no AI layer |

---

## 5. Target Audience

### Primary: People Who Want to Understand Their Finances Deeply

Technically-literate individuals who:
- Want more than a dashboard -- they want analysis, modeling, and forecasting grounded in their real data
- Are comfortable with (or willing to learn) CLI tools, but don't want to write all the analysis code themselves
- Value data ownership as a practical benefit (portability, longevity, no vendor risk), not necessarily as a political stance
- May be at a financial inflection point (new job, buying a house, planning for retirement, paying off debt) where deep analysis matters

### Secondary: Financial Literacy Learners

People who:
- Want to build genuine financial understanding, not just follow a budgeting app's rules
- Learn best from personalized, concrete examples (their own money) rather than generic advice
- Would benefit from an AI tutor that can explain concepts like amortization, tax-loss harvesting, or compound growth using their actual numbers

### Adjacent: Existing PTA Users

hledger and Beancount users who:
- Already have structured financial data and want an intelligence layer on top
- Are tired of writing one-off scripts for every analysis
- Want to query their data in natural language without memorizing BQL or hledger query syntax

---

## 6. Value Proposition

### The One-Liner

> "A personal financial analyst that writes code against your structured accounting data -- opinionated enough to be useful out of the box, capable enough to model anything you can describe."

### For Different Audiences

**Coming from Monarch/YNAB/Copilot:**
> "Your budgeting app shows you pie charts. This shows you what to *do* -- with computations grounded in your actual numbers, not generic advice. And your data stays on your machine."

**Coming from hledger/Beancount:**
> "Keep your journals. Add an agent that can query them in English, write analysis scripts on the fly, and generate the visualizations and reports you've been meaning to build but never got around to."

**Coming from ChatGPT Code Interpreter:**
> "Same analytical power, but with a persistent structured data layer, domain-specific skills, and accumulated context about your financial situation. No re-uploading CSVs every session."

---

## 7. Architecture Principles

### 7.1 The Agent Writes Code; The Engine Does Math

The LLM never performs arithmetic directly. When analysis requires computation, the agent writes and executes code (Python, SQL, shell scripts) that either:
- Queries the accounting engine for validated data, or
- Performs calculations in a deterministic runtime (pandas, numpy, etc.)

This is not a safety constraint bolted on after the fact -- it's the fundamental architecture. LLMs are unreliable at math. Code is not. The agent's job is to translate intent into correct code.

### 7.2 Opinionated Defaults, Escape Hatches Everywhere

The skill library ships with strong opinions: preferred chart of accounts structures, recommended budgeting frameworks, standard report formats. These opinions are explicitly documented, clearly justified, and easily overridden.

The agent should be useful in the first five minutes. It should also never prevent a power user from doing something unusual.

### 7.3 The Skill Library Is a First-Class Asset

Skills are not wrappers around prompts. They encode domain knowledge, analytical methodologies, output templates, and validation logic. The skill library is:
- **Version-controlled** alongside the user's financial data
- **Composable** -- skills can invoke other skills
- **Self-extending** -- the agent can draft new skills from novel analyses
- **Shareable** -- users can publish and import community skills

### 7.4 Accounting Engine Agnosticism

The agent communicates with the accounting engine through a defined interface, not direct file manipulation. This means:
- Switching from hledger to Beancount doesn't require rewriting skills
- Users with custom Python data pipelines can integrate without adopting PTA
- The agent can work with multiple engines simultaneously (e.g., hledger for tracking, custom Python for modeling)

### 7.5 Human-in-the-Loop for Data Writes; Autonomous for Analysis

The agent can freely read data, run analyses, generate reports, and build dashboards without approval. These are read-only operations with no risk.

Write operations (adding transactions, modifying journal entries, committing changes) require human approval by default. This can be relaxed for specific low-risk operations (e.g., auto-importing transactions from a trusted pipeline) via explicit configuration.

---

## 8. Core Capabilities in Detail

### 8.1 Financial Analysis via Code Execution

The agent's primary mode of operation: translate a question or goal into executable analysis.

**Example interactions:**

```
User: "I'm thinking about switching from my current apartment ($2,400/mo)
       to buying a condo. What price range makes sense?"

Agent: [queries accounting engine for income, expenses, savings, existing debt]
       [writes Python: mortgage calculator with PMI, property tax, insurance,
        HOA estimates, opportunity cost of down payment, comparison to renting
        with investment of the difference]
       [generates interactive chart showing buy-vs-rent breakeven by price point]
       [delivers analysis with specific recommendation based on user's numbers]
```

```
User: "Generate my quarterly financial review."

Agent: [queries accounting engine for Q4 data]
       [runs spending-analysis skill, net-worth skill, cash-flow-forecast skill]
       [compiles results into a slide deck with executive summary,
        spending breakdown, net worth trajectory, and action items]
       [saves deck as PDF + PowerPoint]
```

```
User: "Something feels off with my spending this month."

Agent: [queries current month vs. trailing 6-month averages by category]
       [writes anomaly detection script: z-scores by category,
        new merchants, unusual amounts]
       [flags: "Your dining out spend is 2.3σ above your 6-month average.
        $340 of the increase traces to 4 charges at a restaurant you haven't
        visited before. Also: a new $29.99 recurring charge from 'StreamPlus'
        appeared on the 3rd -- is this intentional?"]
```

### 8.2 Financial Literacy Coaching

Not generic tips -- personalized education grounded in the user's actual financial data.

**Example interactions:**

```
User: "I keep hearing I should have an emergency fund. Can you help me
       figure out what that means for me specifically?"

Agent: [queries monthly expenses by category for the last 12 months]
       [computes: essential expenses vs. discretionary, variability by month]
       "Based on your spending, your essential monthly expenses average $3,200
        (rent, utilities, insurance, groceries, minimum debt payments). Financial
        planners typically recommend 3-6 months of essentials.

        For you, that's $9,600-$19,200.

        You currently have $4,300 in your savings account. Here's a plan to reach
        the 3-month target in 8 months based on your current savings rate..."
       [generates a savings trajectory chart with milestones]
```

The coaching adapts to the user's level. It explains concepts when they're new, and skips the explanation for returning users who've already learned the concept.

### 8.3 Multi-Format Output

The same analysis can be delivered as:

| Format | Use case |
|--------|----------|
| **Chat** | Quick questions, iterative exploration |
| **Dashboard** | Ongoing monitoring (spending, net worth, budget status) |
| **Slide deck** | Quarterly reviews, sharing with a partner or financial advisor |
| **PDF report** | Tax preparation, loan applications, formal documentation |
| **Excel/CSV** | Further analysis in external tools, sharing raw data |
| **Interactive notebook** | Deep dives where the user wants to tweak assumptions |

The agent selects the default format based on context but the user can always request a different one.

### 8.4 Self-Extending Skill Library

When the agent builds a novel analysis, the user (or the agent, with permission) can save it as a reusable skill:

```
User: "That rent-vs-buy analysis was great. Save it as a skill so I can
       run it again with different assumptions."

Agent: [extracts the analysis into a parameterized skill with:
        - input schema (home price, down payment %, interest rate, HOA, etc.)
        - computation logic
        - output template (chart + narrative)
        - validation rules (sanity checks on inputs)]
       "Saved as 'rent-vs-buy-analysis' skill. You can invoke it anytime
        with different parameters, or I'll suggest it automatically when
        housing questions come up."
```

---

## 9. Phased Delivery

### Phase 0: Foundation (Current)

- Project scaffolding, documentation infrastructure, and vision
- Research spikes for key technical decisions
- Agent skill library structure (`.agents/skills/`)

### Phase 1: Analyst (Core Loop)

Build the core analysis loop: structured data in, intelligent analysis out.

- Accounting engine integration (hledger first, Beancount second)
- MCP server exposing accounting data to the agent
- Core skill library: spending analysis, net worth, cash flow, budget comparison
- Code execution for custom analyses
- Chat-based interaction as primary interface
- CSV ingestion with LLM-assisted rules generation

**Success gate:** User asks a financial question in natural language, agent queries structured data, writes and executes analysis code, and delivers a grounded answer with visualization.

### Phase 2: Coach

Add coaching, richer output, and deeper analysis capabilities.

- Financial literacy coaching skills (personalized to user data)
- Multi-format output: dashboards, slide decks, PDF reports
- Anomaly detection and proactive insights
- Debt payoff and savings goal modeling
- Automated bank sync integration (Plaid / existing tools)
- Skill self-extension: agent drafts new skills from novel analyses

**Success gate:** User receives a quarterly financial review as a slide deck with actionable insights, generated in under 2 minutes, with all computations traceable to validated accounting data.

### Phase 3: Advisor

Graduate from reactive analysis to proactive, strategic guidance.

- Tax preparation and optimization suggestions
- Investment allocation analysis (with appropriate disclaimers)
- Life event modeling (career change, home purchase, retirement, children)
- What-if scenario comparisons with interactive assumption tuning
- Community skill marketplace (share and import skills)
- Web/mobile interfaces for non-CLI users

**Success gate:** User navigates a major financial decision (home purchase, job change) with agent-generated analysis that a professional financial planner would consider substantive and well-reasoned.

---

## 10. Success Metrics

| Metric | Target | Rationale |
|--------|--------|-----------|
| Analysis grounding | 100% of numerical claims traceable to accounting engine or executed code | The agent never guesses numbers |
| Time to first insight | < 10 min from initial setup | Must feel immediately valuable |
| Analysis accuracy | Code-executed, verifiable by user | No LLM-in-the-head math |
| Skill library growth | Core skills + user-generated skills accumulate over time | The system gets more valuable with use |
| Output format coverage | Chat + at least 2 other formats by Phase 2 | Flexibility is a key differentiator |
| User financial literacy | Self-reported improvement in financial understanding | Coaching should produce lasting learning |

---

## 11. Non-Goals

- **Building an accounting engine.** hledger, Beancount, and custom Python scripts handle this. We integrate them; we don't compete with them.
- **Building an ingestion pipeline from scratch.** Plaid, hledger CSV rules, BeanHub Connect, and similar tools handle this. We make ingestion easier (especially CSV rules generation) but don't own it.
- **Replacing professional financial advice.** The agent provides analysis and education, not fiduciary advice. It should help users have better conversations with real financial advisors, not replace those conversations.
- **Competing on UI with Monarch or Copilot.** Our primary interface is conversational and code-driven. We generate dashboards and slides as output, but we're not building a polished consumer finance app.
- **Building a fintech product.** No payment processing, lending, financial product recommendations, or affiliate revenue.
- **Requiring local-only deployment.** Local LLMs (Ollama) are supported and recommended for data-sensitive operations like categorization. But the agent's highest-value capabilities (complex analysis, coaching, multi-format output) benefit from frontier model quality. Cloud LLMs are a first-class option, not a reluctant fallback.

---

## 12. Risks and Open Questions

| Risk | Severity | Mitigation |
|------|----------|------------|
| Agent generates incorrect financial analysis | High | All numerical work is code-executed and verifiable. Agent shows its work (code + data sources). User can inspect and re-run. |
| Users over-trust agent's financial suggestions | High | Explicit disclaimers. Frame as "analysis" not "advice." Encourage professional consultation for major decisions. |
| Accounting engine integration complexity | Medium | Start with hledger (best CLI/JSON support). Define a clean interface layer so engines are swappable. |
| Skill library quality control | Medium | Core skills are curated and tested. User-generated skills are clearly labeled. Community review for shared skills. |
| Scope creep toward "building an app" | Medium | This document. The core domain is the agent + skills. Everything else is integration. |
| Frontier model cost for heavy analysis use | Low | Most interactions require one code execution cycle. Batch operations and caching reduce redundant calls. |

### Open Questions (candidates for Research Spikes)

1. **SPIKE: Accounting Engine Interface Design** -- What's the right abstraction layer for engine-agnostic queries? Should it look like SQL, a custom DSL, or direct CLI wrapping?
2. **SPIKE: Skill Specification Format** -- How should skills encode their domain knowledge, parameters, validation, and output templates? Can we use the existing `.agents/skills/SKILL.md` format or do we need something richer?
3. **SPIKE: Code Execution Sandboxing** -- What's the right isolation model for agent-generated analysis code? Docker, nsjail, or trust-the-user?
4. **SPIKE: Dashboard Generation** -- What's the best approach for agent-generated interactive dashboards? Streamlit, Observable, static HTML with embedded charts?
5. **SPIKE: Local LLM Viability for Categorization** -- Which local models provide adequate categorization accuracy? This is specifically for the ingestion subdomain, not the core analysis loop.
6. **SPIKE: Coaching Curriculum Design** -- How should financial literacy coaching be structured? Linear progression, topic-based, or purely reactive to user questions?

---

## Appendix A: Competitive Positioning Summary

| Dimension | Monarch / YNAB / Copilot | ChatGPT Code Interpreter | Claude for Financial Services | **LLM Finance Wizard** |
|-----------|--------------------------|--------------------------|-------------------------------|------------------------|
| Primary value | Dashboard + tracking | Ad-hoc analysis | Institutional financial analysis | **Personal financial analysis** |
| Data layer | Proprietary cloud DB | Ephemeral uploads | SEC filings, market data (MCP) | **Structured accounting engine** |
| AI approach | Classification + chat | Code execution (general) | Code execution + domain Skills | **Code execution + domain skills** |
| Persistence | Yes (cloud) | No (session-only) | Yes (within workspace) | **Yes (local, git-tracked)** |
| Domain knowledge | Shallow (categorization) | None (general-purpose) | Deep (institutional finance) | **Deep (personal finance)** |
| Output formats | Dashboard only | Chat + file downloads | Chat + Excel + PPT | **Chat + dashboards + slides + PDF** |
| Self-extending | No | No | Via custom Skills | **Yes (agent drafts new skills)** |
| Data ownership | Vendor-controlled | Session-scoped | Vendor workspace | **User-controlled (local files)** |
| Price | $72-$109/yr | $20-$200/mo | Enterprise pricing | **Open source (bring your own LLM)** |
| Target user | Consumers | Analysts (ad-hoc) | Investment professionals | **Individuals who want depth** |

**Key insight:** The closest architectural analog is Claude for Financial Services -- same pattern (frontier LLM + code execution + structured data + domain Skills + multi-format output), different market (institutional vs. personal). LLM Finance Wizard translates that architecture to the individual.

---

## Appendix B: Why Now

1. **Agentic coding has matured.** Claude Code, ChatGPT Code Interpreter, and similar tools have demonstrated that LLM + code execution is a viable architecture for complex analytical tasks. The infrastructure exists.
2. **MCP provides the integration layer.** The Model Context Protocol gives us a standard way to connect the agent to accounting engines, data sources, and output tools without building custom integrations from scratch.
3. **Accounting engines are ready.** hledger's JSON output, Beancount's Python API, and existing MCP servers (hledger-mcp, beanquery-mcp) mean the structured data layer is already accessible to agents.
4. **The institutional version exists.** Claude for Financial Services proves the architecture works for finance. The question isn't whether this pattern works -- it's whether anyone will build the personal version.
5. **The demand signal is clear.** 37% of Americans use AI for financial tasks (BMO/Ipsos). The beancount community is actively experimenting with LLM integration (GitHub Discussion #971). hledger-mcp has strong community uptake. People want this.
6. **No one has assembled the pieces.** beancount.io markets the vision but hasn't shipped it. BeanHub has announced MCP plans but hasn't built them. The components are all available. The product is not.
