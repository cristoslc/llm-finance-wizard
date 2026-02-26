# LLM Finance Wizard

**Sovereign, AI-augmented personal finance. Powered by LLMs. Grounded by hledger.**

LLM Finance Wizard is an agentic pipeline that brings commercial-grade automation to plain-text accounting -- without surrendering your financial data to the cloud.

## The Problem

Personal finance tools force a false choice: surrender your data to cloud apps (Monarch, YNAB, Copilot) for convenience, or accept the manual drudgery of plain-text accounting for data sovereignty. LLM Finance Wizard eliminates that tradeoff.

## How It Works

```
Bank data (CSV, Plaid, manual)
  -> LLM agent generates/updates hledger CSV rules
    -> hledger imports, deduplicates, validates
      -> LLM categorizes remaining unknowns
        -> You review a clean diff
          -> Approved changes committed to git
```

The LLM handles the tedious parts (categorization, format conversion, natural language queries). hledger handles the math. You keep full control.

## Key Principles

- **Your data stays on your machine.** Default deployment uses local LLMs. Cloud is opt-in.
- **Plain text is the source of truth.** Git-tracked `.journal` files. No databases, no proprietary formats, no lock-in.
- **LLMs suggest, you decide.** Every change is a reviewable diff. The agent never commits without approval.
- **hledger does the math.** LLMs are unreliable at arithmetic ([FinNLP 2025](https://aclanthology.org/2025.finnlp-1.6/)). hledger validates every entry.

## Planned Capabilities

| Capability | Status |
|-----------|--------|
| CSV ingestion with LLM-generated rules | Planned (Phase 1) |
| Transaction categorization (local LLM) | Planned (Phase 1) |
| Natural language financial queries | Planned (Phase 1) |
| MCP server for LLM-hledger integration | Planned (Phase 1) |
| Plaid bank sync | Planned (Phase 2) |
| Anomaly detection and insights | Planned (Phase 2) |
| Receipt scanning (vision LLM) | Planned (Phase 3) |
| Web UI for non-CLI users | Planned (Phase 3) |

## Documentation

- **[Product Vision](docs/vision/(VISION-001)-LLM-Finance-Wizard.md)** -- Full product vision with competitive analysis, architecture, and phased roadmap

## Prerequisites

- [hledger](https://hledger.org/install.html) -- the plain-text accounting engine
- An LLM provider -- local ([Ollama](https://ollama.ai/)) or cloud (Claude, GPT-4)

## Project Status

Early stage. The product vision is defined; implementation has not begun. See the [vision document](docs/vision/(VISION-001)-LLM-Finance-Wizard.md) for the full roadmap and research backing.

## License

TBD
