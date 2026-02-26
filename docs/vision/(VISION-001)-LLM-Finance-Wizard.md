---
title: "VISION-001: LLM Finance Wizard -- Sovereign, AI-Augmented Personal Finance"
status: Draft
author: cristos
created: 2026-02-26
last_updated: 2026-02-26
---

### Lifecycle

| Phase | Date | Commit | Notes |
|-------|------|--------|-------|
| Draft | 2026-02-26 | -- | Initial creation (v3 after internal iteration) |

---

# LLM Finance Wizard

**An agentic pipeline that brings commercial-grade automation to sovereign, plain-text personal finance -- powered by LLMs, grounded by hledger.**

---

## 1. The Problem

Personal finance management in 2026 forces a false choice:

**Option A: Surrender your data for convenience.** Tools like Monarch Money ($100/yr), YNAB ($109/yr), and Copilot ($95/yr) offer polished UIs, automatic bank sync, and increasingly AI-powered insights. But your financial history -- every purchase, every paycheck, every debt payment -- lives on someone else's servers, governed by someone else's terms. Mint's sudden shutdown in March 2024, which stranded millions of users, proved this isn't a theoretical risk. Empower's 2025 migration degraded Personal Capital into near-unusability. These aren't edge cases; they're the inevitable lifecycle of cloud-dependent financial tools.

**Option B: Accept manual drudgery for sovereignty.** Plain-text accounting tools (hledger, Beancount, Ledger-CLI) offer total data ownership -- your finances as version-controlled text files you can read, edit, and keep forever. But the cost is steep: hand-writing CSV import rules, manually categorizing transactions, learning double-entry bookkeeping from scratch, and accepting that "bank sync" means downloading CSVs from your bank's website. The community is passionate but small, and the learning curve locks out anyone who isn't already technically proficient.

**Neither option serves the growing population of privacy-conscious users who want both automation AND control.** 37% of Americans now use AI for financial tasks (BMO/Ipsos 2025), but zero tools let them do so without sending their transaction history to third-party servers.

---

## 2. The Vision

LLM Finance Wizard is an **agentic pipeline** -- not a budgeting app, not a chatbot -- that makes hledger-based personal finance as automated as Monarch while keeping every byte of financial data under the user's sole control.

The core architecture follows a simple separation of concerns:

| Layer | Responsibility | Trust model |
|-------|---------------|-------------|
| **LLM agents** | Categorize transactions, generate CSV rules, interpret reports, answer natural language queries, detect anomalies | Suggest only -- never commit without approval |
| **hledger** | All arithmetic, balance checking, report generation, validation, data integrity | Deterministic -- the LLM does no math |
| **Plain-text journals** | Source of truth for all financial data | User-owned, git-tracked, human-readable |
| **Human** | Final approval of all data changes, oversight of agent suggestions | Always in the loop for writes |

This separation is not just a design preference -- it's an architectural necessity. The FinNLP 2025 paper (ACL Anthology) found that **"LLMs struggle severely with accounting, often producing inaccurate calculations and misinterpreting financial scenarios."** But the same research shows LLMs excel at the parts of finance management that humans find tedious: pattern matching, categorization, format conversion, and natural language interpretation. LLM Finance Wizard exploits this asymmetry.

---

## 3. Market Position

### 3.1 The Sovereignty Spectrum

| Level | Description | Examples | LLM Finance Wizard |
|-------|-------------|----------|---------------------|
| 0 - Exploited | Data monetized by provider | Mint (dead), Credit Karma | -- |
| 1 - Protected | Data not sold, but cloud-hosted | Monarch, YNAB, Copilot | -- |
| 2 - Self-hosted | Data on your server | Firefly III | -- |
| 3 - Local-first | Data on your device, optional sync | Actual Budget | -- |
| 4 - Plain text | Human-readable files you control | hledger, Beancount (today) | Baseline |
| **5 - Sovereign AI** | **Plain text + version control + local AI + automation** | **None exist yet** | **Target** |

LLM Finance Wizard targets Level 5 -- the first tool to combine full plain-text data sovereignty with AI-powered automation. This is not incremental improvement; it's a category that doesn't exist yet.

### 3.2 Competitive Comparison

| Capability | Monarch | YNAB | Copilot | Firefly III | Actual Budget | hledger (raw) | **LLM Finance Wizard** |
|-----------|---------|------|---------|-------------|---------------|---------------|------------------------|
| Bank sync | Plaid | Direct | Plaid | No | Limited | Via tools | **Plaid + CSV + manual** |
| AI categorization | Cloud LLM | No | Cloud LLM | Rules only | Rules only | Regex rules | **Local or cloud LLM** |
| AI assistant | Yes (cloud) | No | No | No | No | No | **Yes (local-first)** |
| Natural language queries | Limited | No | Search only | No | No | No | **Full** |
| Data sovereignty | Low | Low | Medium | High | High | Highest | **Highest** |
| Vendor lock-in risk | High | High | High | Medium | Low | None | **None** |
| Learning curve | Low | Medium | Low | Medium | Low | High | **Medium (AI-assisted)** |
| Open source | No | No | No | Yes | Yes | Yes | **Yes** |
| Price | $100/yr | $109/yr | $95/yr | Free | Free | Free | **Free** |
| Mobile | Yes | Yes | iOS | Web | Web | No | **Phase 2** |

### 3.3 Emerging Competitors

Several projects are converging on parts of this space:

- **hledger-mcp** (@iiAtlas): An MCP server wrapping hledger's CLI with 40+ tools for Claude Desktop. Proves the LLM + hledger concept works. Users report "bookkeeping in the background" by feeding receipts to Claude. However, it's a tool integration, not a pipeline -- there's no automation, no ingestion workflow, no local LLM support.
- **Beanborg**: AI-powered categorization for Beancount using ChatGPT as a fallback. Demonstrates LLM categorization value but limited to Beancount and requires cloud API.
- **BeanHub Connect**: Plaid-to-Beancount commercial service. Closest to automated bank ingestion for PTA but is itself a cloud dependency and charges per-institution.
- **smart_importer**: ML-based categorization for Beancount/Fava using scikit-learn. Local-first but requires significant training data and doesn't leverage LLMs.

None of these provide an **end-to-end agentic pipeline** from bank data to categorized, validated journal entries with local AI and human-in-the-loop oversight.

---

## 4. Target Audience

### Primary: The Sovereignty-Conscious Technical User

Developers, sysadmins, and technically-literate knowledge workers who:
- Already use or are curious about plain-text accounting
- Value data ownership and are uncomfortable with cloud-only financial tools
- Want automation but not at the cost of control
- Are comfortable with CLI tools and git workflows
- May have been burned by Mint's shutdown or a similar service discontinuation

### Secondary: The Privacy-Aware Automation Seeker

Non-developer professionals who:
- Are drawn to local-first and privacy-preserving tools
- Want the power of AI-assisted finance without sending data to the cloud
- Need a guided onboarding path to double-entry accounting (LLM as tutor)
- Might adopt if the experience is smooth enough, even without deep CLI comfort

### Explicitly Not (for now): Casual Budgeters

Users who just want a pretty app to see where their money goes -- Monarch and Copilot serve them well. LLM Finance Wizard's value proposition requires some appreciation for data sovereignty to justify the self-hosted setup.

---

## 5. Value Proposition

### For users coming from commercial apps (Monarch, YNAB, Copilot):

> "Keep the automation you're used to -- AI categorization, natural language queries, bank sync -- but own your data completely. Your financial history lives in plain text files on your machine, tracked in git, readable by any text editor, and yours forever. No subscriptions. No shutdowns. No one selling your spending habits."

### For existing PTA users (hledger, Beancount, Ledger-CLI):

> "Keep your journals, your workflow, and your sovereignty. Add an LLM layer that writes CSV rules for you, categorizes the transactions your rules miss, answers questions about your finances in plain English, and flags anomalies you wouldn't have spotted manually. The agent suggests; you approve; hledger validates."

---

## 6. Core Capabilities

### 6.1 Agentic Transaction Ingestion

The ingestion pipeline is the highest-value automation target. Today's PTA workflow:

```
Download CSV from bank website (manual)
  -> Write/maintain CSV rules file (manual, per-bank)
    -> Run hledger import (manual)
      -> Review and fix miscategorized transactions (manual)
```

LLM Finance Wizard's pipeline:

```
Bank data arrives (Plaid API, CSV drop, manual upload)
  -> LLM agent analyzes CSV structure, generates/updates rules file
    -> hledger import applies rules, deduplicates, appends to journal
      -> LLM agent categorizes remaining unknown transactions
        -> Human reviews staged changes in diff view
          -> Approved changes committed to git
            -> hledger check validates journal integrity
```

Each step is auditable. Every LLM suggestion is a diff the user can accept, modify, or reject. The journal file is never modified without validation.

### 6.2 Intelligent CSV Rules Generation

Instead of hand-writing regex rules for each bank, the user drops a CSV and the LLM:
1. Identifies the bank format (date position, amount columns, description fields)
2. Generates a complete `.csv.rules` file
3. Maps known merchants to account categories using the user's existing chart of accounts
4. Learns from corrections -- rules improve over time

This addresses the single biggest onboarding friction in PTA: the initial rules authoring investment.

### 6.3 Transaction Categorization

For transactions that rules can't match, the LLM categorizes based on:
- Description text and merchant name
- Amount and date patterns
- Historical categorization of similar transactions
- The user's existing account hierarchy

Confidence levels determine the workflow:
- **High confidence** (> 95%): Auto-categorized, flagged for batch review
- **Medium confidence** (70-95%): Presented individually for approval
- **Low confidence** (< 70%): Presented with multiple suggestions

### 6.4 Natural Language Financial Queries

```
User: "How much did I spend on food last quarter compared to the one before?"

Agent: runs `hledger balance expenses:food -p 'last quarter'` and prior quarter
Agent: interprets results, computes delta
Agent: "You spent $2,340 on food last quarter, up 12% from $2,089 the quarter
        before. The increase was driven by dining out ($+180) -- groceries
        were actually down slightly ($-29)."
```

The LLM translates natural language to hledger queries, runs them, and interprets the structured output. All computation is done by hledger -- the LLM only interprets.

### 6.5 Anomaly Detection and Insights

Periodic (or on-demand) analysis that surfaces:
- Unusual transactions (amount outliers, new merchants)
- Subscription creep (new recurring charges)
- Category drift (spending trends over time)
- Missing expected transactions (rent didn't post, paycheck late)
- Duplicate charges across accounts (same merchant + amount + date)

### 6.6 LLM-Assisted Onboarding

For new PTA users, the LLM serves as a tutor:
- Explains double-entry bookkeeping concepts with the user's own data as examples
- Suggests an initial chart of accounts based on the user's transaction history
- Walks through the first CSV import interactively
- Generates starter journal files from existing bank exports

---

## 7. Architecture Principles

### 7.1 LLM as Agent, hledger as Engine

The LLM never performs arithmetic, generates balance assertions, or directly writes to journal files without validation. hledger is the single source of computational truth. The LLM's role is intelligence (pattern matching, natural language, categorization); hledger's role is integrity (math, validation, reporting).

### 7.2 Local-First AI

The default deployment uses a local LLM (via Ollama, llama.cpp, or similar) for all operations involving financial data. Cloud LLMs are available as an opt-in for users who prefer higher capability and accept the privacy tradeoff. The architecture is model-agnostic -- any LLM accessible via API or local inference can be swapped in.

### 7.3 Human-in-the-Loop by Default

Every write operation is staged as a reviewable diff before committing. The system can operate in three modes:
- **Interactive**: Every suggestion presented for approval (default)
- **Batch review**: Suggestions accumulated and presented in a single review session
- **Supervised auto-commit**: High-confidence changes committed automatically; medium/low presented for review (opt-in, requires explicit configuration)

### 7.4 Plain Text as API

Journal files ARE the API. There is no database, no binary format, no proprietary schema. Any tool that can read text can read the data. Any tool that can write text can contribute data (subject to hledger validation). This is the ultimate vendor lock-in escape hatch.

### 7.5 Git as Audit Trail

Every change to financial data is a git commit with a meaningful message. This provides:
- Complete history of every modification
- Attribution (human vs. agent)
- Easy rollback of any change
- Branching for what-if scenarios
- Standard collaboration workflows if multiple people manage household finances

---

## 8. Technical Strategy

### 8.1 Integration Layer: MCP (Model Context Protocol)

The existing hledger-mcp server proves that MCP is a viable integration layer between LLMs and hledger. LLM Finance Wizard will either extend hledger-mcp or build a purpose-built MCP server that exposes:
- All hledger read operations (reports, queries, account lists)
- Staged write operations (propose changes, validate, commit on approval)
- Ingestion pipeline triggers (import CSV, generate rules, categorize unknowns)
- Journal file resources for LLM context

MCP is the right choice because it's model-agnostic (works with Claude, GPT, local models via compatible clients) and has a growing ecosystem of tooling.

### 8.2 Ingestion Adapters

Modular adapters for data sources, prioritized by user impact:

| Priority | Source | Method | Notes |
|----------|--------|--------|-------|
| P0 | CSV files | hledger CSV rules + LLM | Drop a CSV, get categorized transactions |
| P1 | Plaid API | finfetch or custom adapter | Automated bank sync for supported institutions |
| P1 | OFX/QFX files | ledger-autosync conversion | Common bank export format |
| P2 | Receipt images | Vision LLM + OCR | Photo of receipt -> journal entry |
| P2 | Email/SMS parsing | LLM extraction | "Your card ending in 4532 was charged $42.50 at..." |
| P3 | Tiller Money | Spreadsheet export -> CSV | Bridge for Tiller users migrating |

### 8.3 LLM Provider Strategy

| Tier | Provider | Use Case | Privacy |
|------|----------|----------|---------|
| Local (default) | Ollama (Llama, Mistral, Qwen) | Categorization, rules generation, simple queries | Full -- data never leaves machine |
| Cloud (opt-in) | Claude, GPT-4 | Complex analysis, onboarding tutoring, vision (receipts) | User consents; data sent to API |
| Hybrid | Local for data, cloud for reasoning | Anonymize data locally, send patterns to cloud | Partial -- no raw transactions leave |

---

## 9. Phased Delivery

### Phase 0: Foundation (Now)

- Project scaffolding and documentation infrastructure
- Research spikes for key technical decisions
- Community engagement and validation of the vision

### Phase 1: Core Pipeline (Crawl)

- CSV ingestion with LLM-generated rules files
- Transaction categorization (local LLM)
- Basic natural language queries over hledger data
- MCP server for LLM <-> hledger integration
- CLI-based human review workflow (diff + approve)

**Success gate**: A user can drop a bank CSV and get categorized, validated journal entries with <5 minutes of manual review.

### Phase 2: Automation (Walk)

- Plaid integration for automated bank sync
- Recurring import schedules (cron / launchd)
- Improved categorization from user feedback loop
- Anomaly detection and periodic insights
- Multi-account reconciliation and transfer matching

**Success gate**: Monthly financial maintenance takes <15 minutes for a user with 3-5 bank accounts.

### Phase 3: Intelligence (Run)

- Receipt and document scanning (vision LLM)
- Forecasting and budget recommendations
- Tax preparation assistance (annual summary reports)
- Web UI for non-CLI users
- Mobile-friendly interface for on-the-go review and entry

**Success gate**: A non-technical user can set up and maintain their finances with LLM guidance, without touching a terminal directly.

---

## 10. Success Metrics

| Metric | Target | Rationale |
|--------|--------|-----------|
| Time from CSV drop to validated journal entries | < 5 min (Phase 1) | Must beat the ~30 min manual workflow |
| Transaction categorization accuracy | > 90% (Phase 1), > 95% (Phase 2) | Competitive with Monarch's AI categorization |
| Monthly maintenance time (3-5 accounts) | < 15 min (Phase 2) | Must be comparable to commercial apps |
| Data that leaves the user's machine | 0 bytes (default config) | Core sovereignty promise |
| Journal validation errors introduced by LLM | 0 (always) | hledger check is the final gate |

---

## 11. Non-Goals

- **Replacing hledger.** This project augments hledger; it does not fork, wrap, or compete with it. hledger is the engine; we build the cockpit.
- **Building a budgeting methodology.** YNAB owns envelope budgeting; Monarch owns the "financial dashboard." We're building infrastructure, not philosophy. Users bring their own budgeting approach.
- **Competing on UI polish with Monarch/Copilot.** These are well-funded teams with dedicated design resources. Our advantage is sovereignty and extensibility, not pixel-perfect mobile apps.
- **Autonomous financial management.** The LLM never makes financial decisions. It suggests, the human decides. This is a philosophical commitment, not a temporary limitation.
- **Supporting non-hledger PTA tools (initially).** Beancount and Ledger-CLI compatibility may come later, but hledger's superior CSV import system and active development make it the right foundation.
- **Becoming a fintech product.** No payment processing, no lending, no financial product recommendations, no affiliate revenue. This is a tool, not a platform.

---

## 12. Risks and Open Questions

| Risk | Severity | Mitigation |
|------|----------|------------|
| Local LLM quality insufficient for reliable categorization | High | Benchmark local models against cloud; allow cloud opt-in; focus on rules-generation (one-time) over per-transaction categorization |
| Plaid API access difficult for personal/OSS projects | Medium | CSV import is P0; Plaid is P1. The product is viable without Plaid. Finfetch and plaid-cli provide existing patterns. |
| hledger journal format changes break LLM generation | Low | hledger format is stable (15+ years). Use hledger check as validation gate. |
| Users don't trust LLM-generated financial entries | Medium | Default to maximum review friction. Build trust incrementally. Show diffs, not just results. |
| Scope creep toward "building an app" vs. "building a pipeline" | High | This vision document exists to prevent that. We build agents and pipelines, not dashboards. |

### Open Questions (candidates for Research Spikes)

1. **SPIKE: Local LLM Benchmarking** -- Which local models (Llama 3, Mistral, Qwen) provide adequate categorization accuracy for financial transactions? What's the minimum hardware requirement?
2. **SPIKE: Plaid Integration Feasibility** -- What are the actual costs, approval requirements, and maintenance burden of Plaid API access for an open-source personal tool?
3. **SPIKE: MCP Server Design** -- Extend hledger-mcp or build purpose-built? What additional tools does the agentic pipeline need beyond what hledger-mcp provides?
4. **SPIKE: Ingestion Pipeline Architecture** -- What's the right orchestration layer for the multi-step import pipeline? Shell scripts, Python, TypeScript, or agent framework?
5. **SPIKE: Transfer Detection** -- How to reliably detect and match transfers between accounts (the same transaction appearing in two CSVs)?

---

## Appendix A: Why hledger

| Factor | hledger | Beancount | Ledger-CLI |
|--------|---------|-----------|------------|
| CSV import system | Built-in, robust rules engine | External importers required | Basic |
| Active development | Most active (weekly releases) | Active (v3 transition) | Mature, slower |
| Performance at scale | 80s for 1M txns | Competitive (v3) | Failed at 1M txns |
| CLI JSON output | All reports | Limited | Limited |
| Web API | hledger-web (OpenAPI spec) | Via Fava | None |
| MCP integration | hledger-mcp (production) | None | mcp-server-ledger (basic) |
| Error messages | Best in class | Good | Cryptic |
| Community | Largest active community | Growing | Large but less active |

hledger is the right foundation because it has the best CSV import primitives (the critical path for ingestion), the most machine-friendly output formats, an existing MCP integration, and the most active development trajectory.

---

## Appendix B: Market Context and Timing

**Why now:**

1. **Mint's death (March 2024)** shattered the assumption that free financial tools are permanent. Millions of users learned the hard way that cloud-dependent finance tools are ephemeral.
2. **The AI inflection (2025-2026)** brought LLM capabilities to the point where categorization, natural language queries, and format conversion are reliably useful -- not just demos.
3. **Local LLM maturity (2025-2026)** made it possible to run capable models on consumer hardware. Privacy-preserving AI finance is now technically feasible, not just aspirational.
4. **MCP ecosystem growth (2025-2026)** established a standard for LLM-tool integration that makes this kind of agentic pipeline architecturally clean.
5. **hledger-mcp's reception (2025)** validated demand: 55+ upvotes on Reddit, active community adoption, users already doing "bookkeeping in the background" with Claude Desktop.
6. **Growing sovereignty awareness** in the developer community, driven by cloud service shutdowns, privacy regulations, and the local-first software movement.

The window is open. The components exist. No one has assembled them into a coherent, end-to-end pipeline yet.
