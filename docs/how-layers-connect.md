# How the Layers Connect

[← Back to Overview](http://github.com/pivotworks/ai-engineering-metrics/blob/main/README.md)

The stack is diagnostic. When something breaks, you trace through the layers to find the cause.

---

## The Diagnostic Flow

```
Customer bugs spiking (L4)
         │
         ▼
Defect escape rate up (L2) ──► Code churn up (L2)
         │
         ▼
Review depth down (L3) ──► AI override rate down (L3)
         │
         ▼
    DIAGNOSIS: Rubber-stamping AI output
         │
         ▼
    FIX: Restore review process rigor
```

---

## Layer Relationships

| When This Moves... | Check This... | Because... |
|:-------------------|:--------------|:-----------|
| L4 outcomes degrade | L2 quality metrics | Quality problems cause outcome problems |
| L2 quality degrades | L3 process metrics | Process breakdown causes quality problems |
| L3 process degrades | L1 output metrics | Volume pressure causes process shortcuts |
| L1 output spikes | L3 process metrics | More output requires more review capacity |

---

## Reading the Signals

**Top-down (reactive):** Start at L4 when something breaks. Trace backward to find root cause.

**Bottom-up (predictive):** Monitor L3 for early warnings. Process problems predict quality problems before they hit production.

**Cross-layer validation:** L1 and L4 should move together. If output is up but outcomes are flat, something in L2 or L3 is broken.

---

## Navigation

[← Layer 4: Outcome](layer-4-outcome.md) · [Diagnostic Patterns →](diagnostic-patterns.md)
