# Layer 4: Outcome Metrics

[← Back to Overview](../README.md)

**Purpose:** Connect engineering work to business results. This is ground truth. Everything else is proxy.

---

## Why Outcome Metrics Matter

Outcome metrics are the only metrics that actually matter. Everything else is a leading indicator or diagnostic tool. If outcomes aren't improving, nothing else matters.

---

## Metrics

| Metric | What It Measures | How to Track | Target |
|:-------|:-----------------|:-------------|:-------|
| **Customer-reported bugs** | Quality as experienced by users | Support tickets tagged as bugs | Trending down |
| **Incident frequency** | Production stability | PagerDuty, Opsgenie | Stable or declining |
| **MTTR** | How quickly you fix production problems | Incident timestamps | <1hr critical, <4hr standard |
| **Feature adoption** | Whether shipped work gets used | Product analytics (Amplitude, Mixpanel) | Meets adoption targets |
| **Time-to-value** | End-to-end from idea to customer value | Ticket lifecycle tracking | Trending down |

---

## Usage Guidelines

Validate that improvements in Layers 1-3 actually translate to outcomes.

> **⚠️ Warning sign:** Layers 1-3 look great, Layer 4 is flat or declining. You're optimizing the wrong things.

---

## The Ground Truth Test

If you could only look at one layer, this is the one. But looking at only this layer means you're always reacting, never predicting. That's why you need all four.

| What Outcome Metrics Tell You | What They Don't Tell You |
|:------------------------------|:-------------------------|
| Whether customers are happy | Why they're unhappy |
| Whether production is stable | What's about to break |
| Whether features get used | Why they're not being built faster |

Use Layer 4 to validate. Use Layers 1-3 to diagnose and predict.

---

## Navigation

← [Layer 3: Process](layer-3-process.md) · [Back to Overview](../README.md)
