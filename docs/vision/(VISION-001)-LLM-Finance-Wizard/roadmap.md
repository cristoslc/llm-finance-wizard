---
title: "Roadmap — LLM Finance Wizard"
type: Vision supporting document
parent: "VISION-001: LLM Finance Wizard"
author: cristos
created: 2026-03-01
last-updated: 2026-03-01
---

# Roadmap

Phased delivery plan for LLM Finance Wizard. Extracted from VISION-001 Section 6 (Phased Delivery) to enable independent tracking.

---

## Timeline

```mermaid
gantt
    title LLM Finance Wizard — Phased Delivery
    dateFormat YYYY-MM
    axisFormat %b %Y

    section Phase 0: Foundation
        Project scaffolding & docs       :done, p0a, 2026-02, 2026-03
        Research spikes                  :active, p0b, 2026-03, 2026-04
        Agent skill library structure    :p0c, 2026-03, 2026-04

    section Phase 1: Analyst
        Accounting engine integration    :p1a, 2026-04, 2026-06
        MCP server for accounting data   :p1b, 2026-04, 2026-06
        Core skill library               :p1c, 2026-05, 2026-07
        CSV ingestion with LLM rules     :p1d, 2026-05, 2026-07
        Chat-based interaction           :p1e, 2026-06, 2026-07

    section Phase 2: Coach + Scenario Modeler
        Lever identification skill       :p2a, 2026-07, 2026-09
        Scenario modeling skill          :p2b, 2026-07, 2026-09
        Interactive refinement           :p2c, 2026-08, 2026-10
        Financial literacy coaching      :p2d, 2026-09, 2026-11
        Multi-format output              :p2e, 2026-09, 2026-11
        Anomaly detection                :p2f, 2026-10, 2026-11
        Skill self-extension             :p2g, 2026-10, 2026-12

    section Phase 3: Advisor
        Life event modeling              :p3a, 2026-12, 2027-02
        Tax prep & optimization          :p3b, 2027-01, 2027-03
        Investment analysis              :p3c, 2027-02, 2027-04
        Tracking & drift detection       :p3d, 2027-02, 2027-04
        Web/mobile interfaces            :p3e, 2027-03, 2027-06
```

## Phase Status

| Phase | Status | Success Gate | Notes |
|-------|--------|-------------|-------|
| **Phase 0: Foundation** | Active | Scaffolding, docs, research spikes, skill structure | Current phase |
| **Phase 1: Analyst** | Planned | User asks financial question → agent queries data, writes code, delivers grounded answer | Core loop |
| **Phase 2: Coach + Scenario Modeler** | Planned | User identifies goal → agent surfaces levers, models scenarios, helps converge on plan | Full core loop |
| **Phase 3: Advisor** | Planned | User navigates major financial decision with agent analysis a planner would consider substantive | Strategic guidance |

## Phase Details

### Phase 0: Foundation (Current)

- Project scaffolding, documentation infrastructure, and vision
- Research spikes for key technical decisions
- Agent skill library structure

### Phase 1: Analyst (Core Loop)

Build the core analysis loop: structured data in, code-executed analysis out.

- Accounting engine integration (hledger first, Beancount second)
- MCP server exposing accounting data to the agent
- Core skill library: spending analysis, net worth, cash flow, basic lever identification
- Code execution for custom analyses
- Chat-based interaction as primary interface
- CSV ingestion with LLM-assisted rules generation

### Phase 2: Coach + Scenario Modeler

The phase where the core loop comes together.

- Lever identification skill
- Scenario modeling skill: combinatorial what-if modeling
- Interactive scenario refinement
- Financial literacy coaching skills
- Multi-format output: dashboards, slide decks, PDF reports
- Anomaly detection and proactive insights
- Skill self-extension
- Automated bank sync integration (Plaid)

### Phase 3: Advisor

Graduate from reactive analysis to proactive, strategic guidance.

- Life event modeling
- Tax preparation and optimization
- Investment allocation analysis
- Tracking and drift detection
- Community skill marketplace
- Web/mobile interfaces
