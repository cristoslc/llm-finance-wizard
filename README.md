# LLM Finance Wizard

**Your AI financial analyst. Powered by frontier LLMs. Grounded in structured accounting data.**

LLM Finance Wizard is a personal AI financial analyst -- an agentic coding agent that writes and executes code against structured accounting data to help you understand, manage, and improve your financial life.

## What It Does

The agent sits on top of a structured accounting engine (hledger, Beancount, or custom Python) and provides:

- **Financial analysis via code execution** -- not chat-based guessing, but actual Python scripts that compute answers from your validated data
- **Opinionated, battle-tested skills** for spending analysis, debt modeling, budgeting, net worth tracking, tax prep, and more
- **Self-extending capability** -- the agent builds new analytical tools on the fly when your situation demands it
- **Financial literacy coaching** personalized to your actual numbers, not generic advice
- **Flexible output formats** -- chat, interactive dashboards, slide decks, PDFs, Excel

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

**The core domain is the agent and its skill library.** The accounting engine and ingestion pipeline are generic subdomains -- important, but solved problems we integrate rather than rebuild.

## Example Interactions

```
You:   "Am I on track for my emergency fund goal?"

Agent: [queries accounting engine for savings balance and monthly essentials]
       [writes + executes Python: savings rate projection]

       "Your essential expenses average $3,200/mo. At your current savings
        rate of $680/mo, you'll hit the 3-month target ($9,600) in 7.8 months.
        Here's the trajectory..."
       [renders savings chart with milestone markers]
```

```
You:   "Generate my quarterly financial review as a slide deck."

Agent: [runs spending-analysis, net-worth, cash-flow-forecast skills]
       [compiles into PowerPoint with charts and narrative]

       "Saved to quarterly-review-Q4-2025.pptx. Key highlights:
        - Net worth up 4.2% ($+8,340)
        - Dining out was 2.3σ above your 6-month average
        - New recurring charge detected: StreamPlus ($29.99/mo)"
```

## Documentation

- **[Product Vision](docs/vision/(VISION-001)-LLM-Finance-Wizard.md)** -- Full product vision with competitive analysis, architecture, and phased roadmap
- **[Market Research](research/personal-finance-landscape-2026.md)** -- Comprehensive landscape analysis of personal finance tools

## Project Status

Early stage. The product vision is defined; implementation has not begun. See the [vision document](docs/vision/(VISION-001)-LLM-Finance-Wizard.md) for the full roadmap.

## License

TBD
