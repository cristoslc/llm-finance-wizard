# LLM Finance Wizard

**Your AI financial analyst. Powered by frontier LLMs. Grounded in structured accounting data.**

LLM Finance Wizard is a personal AI financial analyst -- an agentic coding agent that writes and executes code against structured accounting data to help you understand, manage, and improve your financial life.

## The Core Loop

Most finance tools can tell you what you spent. None of them help you figure out what to change.

LLM Finance Wizard connects **analysis** (what's happening) → **coaching** (why it matters) → **lever identification** (what you can change) → **scenario modeling** (what happens if you do) → **interactive refinement** (finding the right tradeoffs for your life).

```
You:   "I want to build a 3-month emergency fund. I have $4,300
        saved and my essentials are about $3,200/month."

Agent: [queries accounting engine, executes spending analysis code]

       "You need $5,300 more. At your current savings rate, that's
        12.9 months. But I found several levers in your spending:

        1. Dining out: $480/mo avg (up 34% YoY). Your Q2 baseline
           was $320. Reducing to $400 saves $80/mo.
        2. Subscriptions: 3 of 9 show zero usage in 90 days ($90/mo).
        3. Auto insurance: 22% above profile average (~$40/mo savings).

        Scenario A (subs only): 9.5 months
        Scenario B (subs + dining): 8.0 months
        Scenario C (subs + dining + insurance): 7.6 months
        Scenario D: Tell me which levers feel realistic."

You:   "B, but I can't cut dining that much. $400 not $320."

Agent: [re-models with adjusted parameters]

       "Subs ($90) + dining to $400 ($80) + insurance ($40) = $210/mo
        more → emergency fund by mid-November. Set this as your plan?"
```

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│  CORE: Frontier Agentic Coding Agent                    │
│  Opinionated skills + frontier coding + domain knowledge│
├──────────────┬──────────────────────┬───────────────────┤
│  Ingestion   │  Accounting Engine   │  Output           │
│  (Plaid,CSV) │  (hledger, Beancount)│  (chat, slides…)  │
└──────────────┴──────────────────────┴───────────────────┘
```

**The core domain is the agent and its skill library.** The accounting engine and ingestion pipeline are generic subdomains -- solved problems we integrate rather than rebuild. The agent writes and executes code for all numerical work (never does math in its head), ships with opinionated skills for common analyses, and develops new capabilities through conversation.

## Key Capabilities

- **Lever identification** -- systematically scans your spending for concrete optimization opportunities, ranked by impact
- **Scenario modeling** -- models combinations of levers across time horizons so you can find the tradeoffs that fit your life
- **Financial analysis via code execution** -- actual Python scripts computing answers from validated data, not chat-based guessing
- **Financial literacy coaching** -- personalized education grounded in your actual numbers
- **Self-extending skills** -- the agent builds new analytical tools on the fly; useful ones become reusable skills
- **Flexible output** -- chat, dashboards, slide decks, PDFs, Excel

## Documentation

- **[Product Vision](docs/vision/(VISION-001)-LLM-Finance-Wizard.md)** -- Full product vision with competitive analysis, architecture, and phased roadmap
- **[Market Research](research/personal-finance-landscape-2026.md)** -- Comprehensive landscape analysis of personal finance tools

## Project Status

Early stage. The product vision is defined; implementation has not begun. See the [vision document](docs/vision/(VISION-001)-LLM-Finance-Wizard.md) for the full roadmap.

## License

TBD
