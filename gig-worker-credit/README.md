# Designing Credit Access for India's Gig Workforce

*A product case study from my own independent research and proposal.*

🖼️ [Original one-pager](./gig_worker_credit.png)

*Figures are taken from public reports on India's gig economy; a full source list will be added.*

## Problem

India's gig workforce grew from roughly **77 lakh workers in FY2021 to about 1.2 crore in FY2025**, and is projected to reach **6.7% of the non-agricultural workforce by 2029–30**. Yet nearly **40% of these workers earn under ₹15,000 a month**. Volatile income and no traditional credit history ("thin file") shut most of them out of formal lending. Without credit, they can't invest in the vehicles, equipment or working capital they need to earn more, and the exclusion feeds itself.

## Why now

- **Account Aggregator (AA)** lets lenders see verified income and transaction data with the customer's consent, which solves the missing-data problem that made this segment hard to underwrite.
- **Gig platforms already hold behavioural data** (order history, ratings, completed tasks, how regular earnings are) that can stand in for creditworthiness where bureau data is thin.
- **The segment is big enough** that even a modest, well-targeted product reaches a large, underserved market.

## Who I designed for

A delivery or ride-hailing worker, 22–35, 1–3 years on the platform, no formal credit history, comfortable on a smartphone, paid daily or weekly rather than monthly.

**Pain points:** turned away by traditional lenders for lack of salary slips or a credit score; the informal alternatives (moneylenders, platform advances) are expensive; unpredictable income makes a fixed EMI a poor fit; low trust in banks after past rejections and heavy paperwork.

## What to build first

I compared three interventions on impact against effort:

| Intervention | Role |
|---|---|
| 1. **Alternative credit scoring** (platform + AA data) | **Build first.** It makes the whole segment eligible and the other two depend on it |
| 2. Income-linked flexible repayment | Builds on the scoring model |
| 3. Embedded micro-loans in the platform's app | Distribution, once underwriting is proven |

## Proposed solution

- **Alternative credit scoring engine:** AA-consented bank data plus the platform's earnings and rating history, **weighted toward how regular income is rather than how high**
- **Income-linked repayment** that follows weekly earning cycles instead of a fixed monthly EMI
- **In-app distribution:** a pre-qualified offer appears inside the gig platform at the moment of need, instead of a cold application at a bank
- **A credit ladder:** start small; repaying on time unlocks a higher limit next cycle, building a track record where none existed

## Success metrics

- **Approval rate** for AA-consented applicants, compared with bureau-only approval rates for this segment
- **30/60/90-day delinquency** against fixed-EMI groups, to test the flexible-repayment hypothesis
- **Activation:** share of eligible workers who apply within 90 days of launch
- **Ladder graduation:** repeat borrowers moving to higher limits over 2–3 cycles

## Risks & mitigations

| Risk | Mitigation |
|---|---|
| A new scoring approach could be wrong | Start with small loans and collect 2–3 repayment cycles of first-party data before raising limits |
| Customers may hesitate to share data | Clear consent flows and a plain explanation of how the data is used at the AA sharing step |
| Platform income shocks (demand slowdowns) | Build flexibility into repayment (not payment holidays) so the product holds up in downturns |

## Skills shown

Problem framing for an underserved segment · user research synthesis · impact-vs-effort prioritisation · alternative-data underwriting · risk thinking · success metrics
