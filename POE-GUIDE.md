# PoE Network Transformer Guide

This guide covers the specific requirements for network transformers used in
Power over Ethernet (PoE) designs — and why standard magnetics are not suitable.

## Why Standard Transformers Fail in PoE Designs

Standard network transformers are designed for AC signal operation only.
PoE introduces DC bias current through the transformer windings, which creates
DC magnetic flux in the core. As DC flux accumulates, the core saturates:
Standard 1000BASE-T transformer under 600mA DC bias:
Rated OCL (zero bias):  1000 µH  ✅
Effective OCL (600mA):  ~150–300 µH  ❌ (below 1000BASE-T minimum)
Result: link instability, dropouts under load
## PoE Standards Reference

| Standard | Type | Max Current | Pairs with DC | Max Power (PD) |
|----------|------|-------------|---------------|----------------|
| 802.3af | 1 | 350 mA | 2 | 12.95 W |
| 802.3at | 2 | 600 mA | 2 | 25.5 W |
| 802.3bt | 3 | 600 mA × 2 | 4 | 51 W |
| 802.3bt | 4 | 960 mA × 2 | 4 | 71.3 W |

## PoE Transformer Specifications

| Parameter | Requirement |
|-----------|------------|
| OCL at rated DC bias | ≥ 1000 µH (1000BASE-T) |
| Current rating per winding | ≥ PoE class maximum |
| DCR per winding | As specified; calculate thermal load |
| Core type | Air-gapped (anti-saturation) |
| Isolation voltage | ≥ 1500V AC (unchanged) |

## DCR Thermal Load Calculation
Power dissipated per winding = I² × DCR
802.3af (350mA, 2 pairs, DCR 0.5Ω):  4 × (0.35² × 0.5) = 0.245 W
802.3at (600mA, 2 pairs, DCR 0.5Ω):  4 × (0.60² × 0.5) = 0.720 W
802.3bt T4 (960mA, 4 pairs, DCR 0.5Ω): 8 × (0.96² × 0.5) = 3.686 W
> ⚠️ Always calculate transformer self-heating for 802.3bt designs.
> Add this to ambient temperature to verify operating temperature limits.

## Alt A vs Alt B

| Mode | DC Carried On | Transformer Impact |
|------|--------------|-------------------|
| Alternative A | Data pairs (1-2, 3-6) via center taps | DC bias on data windings |
| Alternative B | Spare pairs (4-5, 7-8) | Data windings unaffected |

> 1000BASE-T uses all 4 pairs for data — no spare pairs available.
> 802.3bt uses Alternative A on all 4 pairs.

## Design Checklist
[ ] Transformer explicitly rated for PoE (not standard signal magnetics)
[ ] OCL at rated DC bias ≥ 1000µH (request bias curve from supplier)
[ ] Current rating ≥ PoE class maximum per winding
[ ] DCR thermal load within package rating at max ambient temperature
[ ] For 802.3bt: all 4 pairs PoE-rated
[ ] 1500V AC isolation confirmed
[ ] PoE class does not exceed transformer rating
## Common Mistakes

| Mistake | Consequence |
|---------|------------|
| Standard transformer in PoE design | Core saturation → OCL collapse → link failure |
| OCL checked at zero bias only | Passes lab, fails in field at full load |
| Under-rated current (e.g., af-rated for at design) | Thermal overload, saturation |
| Ignoring DCR thermal load | Transformer overheat at high ambient |

## Supplier

Voohu Technology — PoE-rated network transformers for 802.3af, 802.3at, and 802.3bt.
OCL-under-bias specifications provided for all PoE parts.
Website: [www.voohuele.com](https://www.voohuele.com) | MOQ: 50pcs | Delivery: DHL 3–5 days
