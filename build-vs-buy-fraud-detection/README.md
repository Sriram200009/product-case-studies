# Build vs. Buy: Scaling Fraud Detection in Digital Lending

*A product decision framework, from my own independent research. It describes no specific company's systems.*

📄 [Full case study (PDF)](./build_vs_buy_fraud_detection.pdf)

## The decision

As a digital lending product grows, new kinds of fraud appear faster than manual review can keep up. Every lending team reaches the same fork: **build fraud detection in-house, or buy a third-party solution?**

This is usually treated as an engineering call, but it's really a product and business one. Both wrong answers are expensive. Buying ties you to a vendor's roadmap and blind spots. Building takes 2–3 quarters of engineering on a problem vendors have already solved, and delays the work that actually sets the product apart.

## How I evaluate it

| Criterion | The real question |
|---|---|
| **Time to market** | How fast must fraud losses be contained, compared with how long a build would really take? |
| **Cost of ownership** | Vendor licence and integration, or a fully loaded build (engineering, maintenance, model retraining)? |
| **Compliance & data control** | Can the vendor *prove* data residency and an audit trail, not just claim them? |
| **Strategic differentiation** | Does fraud detection set this product apart, or is it table stakes? |
| **Engineering opportunity cost** | What does a 2–3 quarter build push off the roadmap? |
| **Vendor lock-in** | How hard is it to leave once transaction history and models live in the vendor's system? |

## Recommendation: a staged hybrid

**Buy** a proven rules-based engine as the baseline. It's solved, well-audited technology, and building it mostly delays launch without adding anything distinctive.

**Build** a thin proprietary layer on top, using the product's own behavioural and transaction data. That's where the real differentiation is, and it's a much smaller build than a full engine.

| Phase | Months | What happens |
|---|---|---|
| 1 | 0–3 | Launch on the vendor baseline; record every decision so the data can be used later |
| 2 | 3–9 | Ship the proprietary behavioural layer as a second signal and measure the lift over the vendor alone |
| 3 | 9–18 | If the proprietary layer keeps catching more fraud than the vendor, start a staged move away from the vendor, based on real data rather than up-front assumptions |

## Getting each stakeholder on board

- **Engineering:** frees 2–3 quarters for differentiated work instead of rebuilding commodity infrastructure
- **Compliance & risk:** a vendor with an existing audit trail and certifications carries less regulatory risk than an unproven in-house model
- **Finance:** licence costs are predictable; a full build's opportunity cost is harder to see but very real
- **Leadership:** fraud protection ships in weeks, not quarters, and the long-term path to differentiation stays open

## Success metrics

- **Fraud catch rate:** share of confirmed fraud caught before any loss, tracked separately for the vendor baseline and the in-house layer
- **False-positive rate:** genuine customers wrongly flagged, which is the hidden cost of an over-aggressive model
- **Time to decision:** from transaction to a fraud/no-fraud verdict, because delay hurts the customer experience
- **Cost per transaction reviewed:** vendor fees plus engineering, tracked over time to check the phased plan is paying off

## Skills shown

Strategic trade-offs · build-vs-buy and vendor evaluation · getting stakeholders aligned · phased roadmapping · ML product thinking (baseline vs proprietary signal, catch rate vs false positives)
