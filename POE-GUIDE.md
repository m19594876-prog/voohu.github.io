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

## IEEE 802.3bt PoE++ (Type 3 / Type 4)

### PoE Standard Summary

| Standard | Type | PSE Max | PD Max | Max I/Pair | Pairs Used | Transformer |
|----------|------|---------|--------|-----------|------------|------------|
| 802.3af | 1 | 15.4W | 12.95W | 350 mA | 2 | 100BASE-TX |
| 802.3at | 2 | 30W | 25.5W | 600 mA | 2 | 100BASE-TX or GbE |
| 802.3bt | 3 | 60W | 51W | 600 mA | **4** | **GbE 4-pair** |
| 802.3bt | 4 | 90W+ | 71.3W | **960 mA** | **4** | **GbE 4-pair** |

### Key Changes from 802.3at to 802.3bt

**Architecture change:** 802.3bt Type 3/4 delivers power over all 4 pairs simultaneously.
→ Requires Gigabit (4-pair) transformer. 100BASE-TX transformer cannot support full Type 3/4.

**Current increase (Type 4):** 600mA → 960mA per pair.
→ DCR and thermal requirements become critical.

### DCR Requirement by PoE Type

| PoE Type | Max DC Current | Max DCR/Winding | Thermal Budget Basis |
|----------|---------------|----------------|---------------------|
| Type 1 (802.3af) | 350 mA | < 2.0Ω | Low concern |
| Type 2 (802.3at) | 600 mA | < 0.8Ω | Moderate concern |
| Type 3 (802.3bt) | 600 mA | < 0.8Ω | Moderate concern |
| **Type 4 (802.3bt)** | **960 mA** | **< 0.3Ω** | **Critical** |

### Thermal Calculation — Type 4
Copper loss per winding:   P = I² × DCR = (0.96)² × DCR_winding
Total loss (4 windings):   P_total = 4 × (0.96)² × DCR_winding
Temperature rise:          ΔT = P_total × Rth_ja
Target: P_total < 1.0W for typical SMD package (Rth_ja ≈ 60°C/W → ΔT < 60°C)
Maximum acceptable DCR for Type 4:
P_total = 1.0W → DCR_winding = 1.0 / (4 × 0.96²) = 0.27Ω
→ Target DCR per winding: ≤ 0.25–0.30Ω for 802.3bt Type 4

### OCL Under DC Bias — Specification Requirements
Standard transformers:    OCL measured at 0mA DC bias
PoE-rated transformers:   OCL must hold at OPERATING DC bias current
Minimum OCL at operating bias:
100BASE-TX PoE: ≥ 350µH  at 350mA (Type 1) / 600mA (Type 2/3) / 960mA (Type 4)
1000BASE-T PoE: ≥ 1000µH at 350mA (Type 1) / 600mA (Type 2/3) / 960mA (Type 4)
Request from supplier: OCL vs DC current curve, confirmed at:
350mA, 600mA, 960mA data points

### Center Tap Design for High-Current PoE

| Parameter | 802.3at | 802.3bt Type 4 |
|-----------|---------|---------------|
| CT current | 600 mA | 960 mA |
| CT pin rating needed | ≥ 700mA | **≥ 1000mA** |
| PCB trace (1oz, 10°C rise) | ≥ 0.4mm | **≥ 0.5mm** |
| Vias at CT | 1 via OK | **≥ 2 vias parallel** |

### 802.3bt Design Checklist
Transformer selection:
[ ] 4-pair Gigabit transformer (not 2-pair 100BASE-TX)
[ ] OCL ≥ 1000µH at 960mA DC bias (Type 4) or 600mA (Type 3)
[ ] DCR per winding ≤ 0.30Ω (Type 4) or ≤ 0.80Ω (Type 3)
[ ] Center tap current rating ≥ 1000mA (Type 4)
[ ] PoE-rated part number (air-gapped core confirmed)
Thermal verification:
[ ] Calculate total copper loss: P = 4 × I² × DCR_winding
[ ] Estimate junction temperature: Tj = Ta + P × Rth_ja
[ ] Verify Tj < rated maximum at worst-case Ta
PCB design:
[ ] CT trace width meets current capacity requirement
[ ] ≥ 2 vias in parallel for CT connections (Type 4)
[ ] Copper pour under transformer for thermal dissipation

### Compatible PSE / PD Controllers

| Role | Part | Vendor | Type |
|------|------|--------|------|
| PSE | TPS23880 / TPS23882 | TI | 802.3bt Type 3/4 |
| PSE | PD69208 | Microchip | 802.3bt managed |
| PSE | AG9900M | Silvertel | 802.3bt |
| PD | TPS2373 | TI | 802.3bt Type 3/4 |
| PD | PD69100 | Microchip | PoE PD |
| PD | Ag5450A | Silvertel | 802.3bt PD |

### Supplier Reference

Voohu Technology — [www.voohuele.com](https://www.voohuele.com)  
PoE-rated transformers for 802.3af / 802.3at / 802.3bt.  
Includes OCL vs DC bias curves and DCR thermal data for Type 3/4 designs.  
MOQ: 50pcs | Delivery: DHL 3–5 days | BOM sourcing support.
