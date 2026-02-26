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
| Draft | 2026-02-26 | -- | Restructure: extract architecture to supporting doc; extract competitive analysis; remove usage stories (will become JOURNEY-NNN artifacts) |

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

The agent writes code; code does math. The LLM never performs arithmetic directly -- all numerical work is executed as code against structured data, producing verifiable, reproducible results. See [Architecture Overview](architecture-overview.md) for how this works technically.

---

## 3. Market Context

No existing tool combines lever identification from actual spending data, combinatorial scenario modeling, and personalized coaching. The closest competitors (Origin Financial, Hiro) use pre-built planning models -- they can answer "what if you save $300/month more?" but can't tell you *which* $300. Planning tools (ProjectionLab, Boldin) model parameters you define manually but never analyze your data to find the parameters. Dashboard apps (Monarch, YNAB) show where money went but can't model what to change.

The DIY version (Claude Code + hledger-mcp) proves the concept works but lacks validated computation, persistent skills, and accessibility beyond developers.

The competitive window is real but not permanent. Origin, Hiro, or Anthropic itself could move into this space.

Full analysis: [Competitive Analysis 2026](competitive-analysis-2026.md) | Market research: [Personal Finance Landscape](../../research/personal-finance-landscape-2026.md)

---

## 4. Target Audience

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

## 5. Value Proposition

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

## 6. Phased Delivery

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

## 7. Success Metrics

| Metric | Target | Rationale |
|--------|--------|-----------|
| Analysis grounding | 100% of numerical claims traceable to code execution | The agent never guesses numbers |
| Lever identification | Surfaces actionable levers the user hadn't identified | Must provide genuine insight, not obvious observations |
| Scenario accuracy | All scenarios reproducible by re-running generated code | Scenarios must be verifiable, not vibes |
| Time to first insight | < 10 min from initial setup | Must feel immediately valuable |
| Plan convergence | User converges on a plan within one interactive session | The scenario refinement loop must be tight |
| Skill library growth | Core skills + user-generated skills accumulate over time | System gets more valuable with use |

---

## 8. Non-Goals

- **Building an accounting engine.** hledger, Beancount, and custom Python handle this.
- **Building an ingestion pipeline from scratch.** Plaid, hledger CSV rules, BeanHub Connect handle this. We make ingestion easier but don't own it.
- **Replacing professional financial advice.** The agent provides analysis and education, not fiduciary advice. It should help users have better conversations with real advisors, not replace them.
- **Competing on UI with Monarch or Copilot.** We generate dashboards and slides as output, but we're not building a polished consumer finance app.
- **Replicating ProjectionLab's UI.** ProjectionLab's dedicated retirement planning interface is polished and deep. We don't need to rebuild that UI. But the agent should absolutely know how and when to run a Monte Carlo simulation, model Roth conversions, or project retirement trajectories -- these are techniques in the agent's toolkit, applied when the user's question calls for them.
- **Building a fintech product.** No payment processing, lending, or financial product recommendations.
- **Requiring local-only deployment.** Local LLMs are supported for data-sensitive operations like categorization. But the core analysis loop benefits from frontier model quality. Cloud LLMs are a first-class option.

---

## 9. Risks and Open Questions

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

---

## Supporting Documents

| Document | Purpose |
|----------|---------|
| [Architecture Overview](architecture-overview.md) | How the system works: code execution, skill library, accounting engine integration, capabilities |
| [Competitive Analysis 2026](competitive-analysis-2026.md) | Detailed competitive positioning against Origin, Hiro, ProjectionLab, Monarch, and others |
| [Personal Finance Landscape](../../research/personal-finance-landscape-2026.md) | Market research on the personal finance + AI ecosystem |
