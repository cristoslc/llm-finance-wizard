---
title: "JOURNEY-005: The Missing Pieces"
status: Draft
author: cristos
created: 2026-03-01
last_updated: 2026-03-01
parent: VISION-001
---

### Lifecycle

| Phase | Date | Commit | Notes |
|-------|------|--------|-------|
| Draft | 2026-03-01 | -- | Initial creation |

---

# JOURNEY-005: The Missing Pieces

## Persona

**Priya, 29, software engineer at a mid-size company.** Makes $115K. She enrolled in her 401k during onboarding three years ago — picked a target-date fund, set her contribution to 6%, and never looked at it again. She vaguely remembers checking boxes on a benefits enrollment form but couldn't tell you what she actually signed up for. She has no FSA, no HSA, and isn't sure if her company offers them.

Priya has been using LFW for two months. She imports her bank and credit card CSVs monthly and has a decent picture of her spending. But her financial picture has a hole in it: she only sees what hits her bank account. Her paystub tells a different story — gross pay, federal and state withholding, 401k deductions, health insurance premiums, disability insurance, a legal plan she doesn't remember signing up for — none of which exists in her ledger.

Priya didn't come looking for this. She asked "why is my take-home lower than I expected?" and the answer is in a document she's never really read.

## Goal

Go from "I track what hits my bank account" to "I understand my full compensation picture and I'm not leaving money on the table."

## Stages

### 1. The Question

**Trigger:** Priya is reviewing her monthly check-in and something bugs her.

```
Priya: "My salary is $115K but I only see about $6,200/month
        deposited. Where's the rest going?"

Agent: That's a $3,400/month gap between gross and net. I can see
       your direct deposits but not what's being withheld or deducted
       before they hit your bank.

       If you upload a recent paystub, I can break down exactly
       where that $3,400 goes — taxes, retirement, insurance, and
       anything else your employer deducts.
```

**Emotional state:** Mild curiosity. Priya knows about taxes, but $3,400/month feels like a lot and she can't account for it.

**Pain points:**
- Without paystub data, the agent can only see net deposits — the pre-tax world is invisible
- Priya may not know where to find her paystub (employer portal, ADP, Workday, etc.)

**Opportunities:**
- The agent identified a gap in its own data and asked for the specific document that would fill it — this is proactive, not reactive
- This is a natural moment: the question arose from Priya's own data, not a feature tour

### 2. Document Upload & Extraction

**Trigger:** Priya finds her latest paystub PDF in her employer's HR portal and uploads it.

**What the agent does:**
- Reads the paystub PDF (OCR if scanned, structured extraction if digital)
- Extracts every line item: gross pay, federal withholding, state withholding, Social Security, Medicare, 401k contribution, health insurance premium, dental, vision, disability insurance, legal plan, and net pay
- Cross-references: net pay on the paystub matches the direct deposit amount in the ledger
- Creates journal entries that capture the full paycheck, not just the deposit

```
Agent: Here's what your February 28 paycheck looks like in full:

       GROSS PAY                              $4,423.08
       ────────────────────────────────────────────────
       Federal withholding                     -$621.00
       State withholding (CA)                  -$354.00
       Social Security                         -$274.23
       Medicare                                 -$64.13
       ────────────────────────────────────────────────
       401k (6%)                               -$265.38
       Health insurance (employee share)       -$189.00
       Dental insurance                         -$23.50
       Vision insurance                          -$8.75
       Long-term disability                     -$12.40
       Legal plan                               -$18.50
       ────────────────────────────────────────────────
       NET PAY (matches your deposit)        $2,592.19

       I notice a few things already. Want me to walk through them?
```

**Emotional state:** "I've literally never seen my paycheck broken down like this." Priya has glanced at paystubs before but never internalized the numbers.

**Pain points:**
- Paystub formats vary enormously — ADP, Workday, Gusto, Paylocity, custom PDFs, scanned images
- Some line items are abbreviated or cryptic ("LTD EE", "VOL LIFE AD&D")
- If extraction is wrong, trust breaks immediately — Priya can verify against the PDF

**Opportunities:**
- The cross-reference (extracted net pay matches bank deposit) builds trust immediately
- This is the first time Priya's ledger captures her *full* compensation, not just the deposit
- The agent flagged it has observations — this is the hook for the next stage

### 3. The Gap Analysis

**Trigger:** Priya says yes.

```
Agent: Three things stand out from your paystub:

       1. 401K: EMPLOYER MATCH LEFT ON THE TABLE
          You're contributing 6% ($265/paycheck, $6,900/yr).
          Your employer matches 50% up to 8%. That means:
          - At 6%: you get 3% match ($3,450/yr)
          - At 8%: you'd get 4% match ($4,600/yr)
          You're leaving $1,150/year in free money on the table.
          Bumping to 8% costs you $88/paycheck in take-home.

       2. NO FSA OR HSA
          You're paying $189/paycheck for health insurance, so you
          have employer coverage. But I don't see an FSA or HSA
          contribution on your paystub.

          If your plan is HSA-eligible (high-deductible), you could
          contribute pre-tax to an HSA — $4,150/yr in 2026.
          If not, a healthcare FSA lets you set aside up to $3,300/yr
          pre-tax for medical expenses.

          Last year you had $1,840 in out-of-pocket medical expenses
          (I can see the charges in your transaction history). An FSA
          would have saved you roughly $460 in taxes on that spending.

          You'll need to check your benefits portal to see which
          option is available — I can't tell from the paystub alone.

       3. LEGAL PLAN: DO YOU USE THIS?
          You're paying $18.50/paycheck ($481/yr) for a legal plan.
          Do you know what it covers? If you haven't used it in three
          years, it might not be worth keeping at next open enrollment.
```

**Emotional state:** A mix of "oh no" and "oh, that's useful." The 401k match gap feels like finding a $20 bill in a coat pocket — except it's $1,150/year. The FSA absence is less dramatic but the tax savings are concrete. The legal plan is a small "wait, why am I paying for that?"

**Pain points:**
- The agent can identify *what's missing* from the paystub but can't always determine *what's available* — it doesn't have access to the benefits portal
- FSA vs. HSA eligibility depends on the health plan type, which isn't on the paystub
- Recommendations that require action during open enrollment (months away) may feel inactionable now

**Opportunities:**
- The 401k match analysis is the centerpiece: it's concrete, it's money left on the table, and the fix is trivial (change a percentage in the HR portal)
- Cross-referencing paystub data with transaction history (the $1,840 in medical expenses) is uniquely powerful — no other tool does this because no other tool has both datasets
- The agent can maintain a "benefits action list" that surfaces at open enrollment time

### 4. Building the Full Picture

**Trigger:** Priya is convinced. She uploads several more documents.

- **Prior year's W-2:** Agent extracts total compensation, tax withholding, retirement contributions, and compares to current trajectory. "You're on track for $2,100 more in federal withholding this year — did you get a raise?"
- **Benefits enrollment summary (PDF from HR portal):** Agent reads what Priya is actually enrolled in, confirms no HSA/FSA, identifies the health plan type. "Your plan is a PPO with a $1,500 deductible — that's not HSA-eligible. But you can do a healthcare FSA."
- **Year-end 401k statement:** Agent extracts balance, fund allocations, YTD contributions, employer match. "Your 401k is 100% in a 2060 target-date fund. That's a fine default. Balance is $24,800 — you're ahead of the median for your age."
- **Old offer letter:** Agent extracts base salary, signing bonus, equity vesting schedule. "Your offer letter shows 4-year vesting with 1-year cliff. You passed the cliff 2 years ago — you should have vested shares. Are you tracking those?"

Each document fills in a piece of Priya's financial picture that bank transactions alone could never show.

```
Agent: With your paystub, W-2, benefits summary, and 401k statement,
       I now have a much more complete picture:

       TOTAL COMPENSATION (2026, projected)
       ┌─────────────────────────┬────────────┐
       │ Base salary             │ $115,000   │
       │ Employer 401k match     │   $3,450   │
       │ Health/dental/vision    │   $8,400   │  ← employer share
       │ Other benefits          │   $1,200   │
       ├─────────────────────────┼────────────┤
       │ Total compensation      │ $128,050   │
       └─────────────────────────┴────────────┘

       Your salary is $115K but your total comp is $128K.
       And with the 401k fix, it'd be $129.2K.
```

**Emotional state:** "I had no idea my benefits were worth $13K." Priya has never thought about total compensation before. The number reframes how she thinks about her job.

**Pain points:**
- Document accumulation can feel like a chore — "how many things do I need to upload?"
- Some documents are hard to find (old offer letters, benefits summaries)
- Equity/stock vesting adds complexity that may overwhelm

**Opportunities:**
- Each document provides a distinct insight — the agent should make each upload feel worthwhile, not like homework
- Total compensation view is a perspective shift that changes how Priya evaluates her job, future offers, and negotiation leverage
- The vested shares question ("are you tracking those?") may surface an entirely new account to add to her financial picture

### 5. The Action Plan

**Trigger:** Priya has the full picture. Now she wants to act.

```
Agent: Based on everything we've found, here's what I'd suggest,
       ordered by impact and urgency:

       DO NOW (takes 15 minutes)
       ☐ Increase 401k contribution from 6% to 8%
         → +$1,150/yr in employer match
         → -$88/paycheck in take-home
         Log into [your HR portal] → Retirement → Change contribution

       DO AT OPEN ENROLLMENT (November)
       ☐ Enroll in healthcare FSA, elect $1,800
         → ~$450/yr tax savings (based on your medical spending)
         → $150/month pre-tax deduction
       ☐ Evaluate legal plan — cancel if unused
         → +$481/yr in take-home if dropped

       INVESTIGATE
       ☐ Check on vested equity — do you have shares to track?
       ☐ Review 401k fund selection (target-date is fine, but
         you could reduce fees with index funds if available)

       Total potential impact: ~$2,080/yr in additional value
       ($1,150 match + $450 FSA savings + $481 legal plan)

       Want me to add these to your action list and remind you
       at open enrollment?
```

**Emotional state:** Empowered. The actions are specific, ordered, and achievable. The "do now" item takes 15 minutes and is worth $1,150/year. That's an extraordinary return on effort.

**Pain points:**
- The agent can't execute these actions for Priya — she has to log into HR portals herself
- Open enrollment items require waiting months — will Priya remember?

**Opportunities:**
- The "do now / do at enrollment / investigate" triage makes this actionable instead of overwhelming
- Reminders at open enrollment close the loop — the agent surfaces the FSA and legal plan decisions when Priya can actually act on them
- The $2,080/yr figure is a concrete "this journey was worth it" number

### 6. Ongoing Document Intelligence

**Trigger:** Months later, Priya uploads a new document — or the agent notices something in a transaction.

```
Agent: I see a $450 charge to "QUEST DIAGNOSTICS" last month
       that you categorized as medical.

       Since you enrolled in your FSA in November, that's
       an FSA-eligible expense. Did you submit it for
       reimbursement? That's $450 you can get back pre-tax.
```

Or, at tax time:

```
Agent: Your W-2 just became available. Comparing to last year:

       401k contributions: $9,200 (was $6,900) ✓ You made the change
       FSA election: $1,800 ✓ New this year
       Federal withholding: down $380 (FSA reduced taxable income)

       Your effective tax rate dropped from 22.4% to 21.1%.
       The changes we identified saved you $2,030 this year.
```

**Emotional state:** Validation. The actions Priya took months ago are paying off in concrete, measurable ways. The agent isn't just tracking money — it's tracking *decisions* and showing their impact.

**Pain points:**
- FSA reimbursement is a manual process (submit receipts to the FSA administrator) — easy to forget
- Document uploads may taper off once the initial picture is built

**Opportunities:**
- Transaction-level FSA reminders ("this looks FSA-eligible, did you submit it?") are high-value, low-effort nudges
- The year-over-year W-2 comparison closes the loop on the entire journey: here's what you changed, here's the result
- This naturally feeds into other journeys — the total comp view informs JOURNEY-002 (big decisions like job changes) and the tax optimization feeds JOURNEY-004 (annual reckoning)

---

## Pain Points Summary

| Stage | Key Pain Point | Mitigation |
|-------|---------------|------------|
| The Question | Pre-tax world is invisible from bank data alone | Agent identifies the gap and asks for the specific document |
| Document Upload | Paystub formats vary enormously | Robust extraction + cross-reference against known deposit amount |
| Gap Analysis | Can't determine benefits eligibility from paystub alone | Be explicit about what requires checking the benefits portal |
| Full Picture | Document accumulation feels like homework | Each upload delivers a distinct, immediate insight |
| Action Plan | Agent can't execute actions in HR portals | Triage by urgency, give specific instructions, offer reminders |
| Ongoing | FSA reimbursement is easy to forget | Transaction-level nudges when FSA-eligible expenses appear |

## Opportunities Summary

| Stage | Key Opportunity |
|-------|----------------|
| The Question | Agent proactively identifies gaps in its own data |
| Document Upload | Full-paycheck journal entries capture compensation, not just deposits |
| Gap Analysis | Cross-referencing paystub deductions with transaction history is uniquely powerful |
| Gap Analysis | 401k match gap is concrete, actionable, and high-impact |
| Full Picture | Total compensation view reframes how the user thinks about their job |
| Action Plan | $2,080/yr in concrete value from 15 minutes of action |
| Ongoing | Year-over-year W-2 comparison closes the loop and validates decisions |
