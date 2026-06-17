## Network Transformer Key Specifications

Reference guide for evaluating and comparing network transformer datasheets.

---

### Full Specification Table

| Parameter | Abbreviation | 10/100BASE-TX | 1000BASE-T | Test Condition |
|---|---|---|---|---|
| Open Circuit Inductance | OCL | ≥ 350µH | ≥ 1000µH | 100kHz, 0.1V RMS |
| Isolation Voltage | Viso | 1500V AC min | 1500V AC min | 1-second withstand |
| Insertion Loss | IL | < 1.0 dB | < 1.0 dB | Across operating band |
| Return Loss | RL | > 16 dB | > 16 dB | Across operating band |
| Turns Ratio | — | 1CT:1CT | Complex 4-pair | Standard Ethernet |
| DC Resistance | DCR | 1–4Ω typical | 1–4Ω typical | DC measurement |
| Operating Temp (commercial) | Tₒₚ | 0°C to +70°C | 0°C to +70°C | — |
| Operating Temp (industrial) | Tₒₚ | -40°C to +85°C | -40°C to +85°C | Optional rating |

---

### OCL: The Critical Parameter

OCL (Open Circuit Inductance) determines the transformer's low-frequency performance.

```
Speed           Min OCL    Pairs    Notes
────────────────────────────────────────────────────────
10BASE-T        350µH      2        ┐
100BASE-TX      350µH      2        ┘ Interchangeable
────────────────────────────────────────────────────────
1000BASE-T      1000µH     4          NOT interchangeable with above
────────────────────────────────────────────────────────
```

> **Warning:** Substituting a 10/100 transformer into a Gigabit design
> results in degraded link quality or no link. OCL is 3× below requirement.

---

### Isolation Voltage Levels

| Rating | Application |
|---|---|
| 1500V AC | Standard commercial Ethernet (IEEE 802.3 minimum) |
| 2500V AC | Industrial, enhanced protection |
| 4000V AC | Medical, outdoor, high-risk environments |

---

### DCR and PoE Thermal Consideration

For PoE designs, transformer DCR directly affects heat dissipation:

```
P = I² × R

Example (802.3at, 400mA per pair, 3Ω DCR):
P = (0.4)² × 3 = 0.48W per winding

→ Standard transformers: NOT rated for continuous PoE current
→ Always use explicitly PoE-rated magnetics for PoE applications
```

---

### Bob Smith Termination (Recommended for All Designs)

Connects center taps to chassis ground to suppress common-mode emissions:

```
Winding CT ──[75Ω]──[1000pF]── Chassis GND
```

Omitting this termination significantly increases risk of failing radiated emissions testing.

---

*Source: [Voohu Technology](https://www.voohuele.com) | Network Transformer Distributor | Suzhou, China*
*Stock: 10/100 and Gigabit variants | PoE-rated available | 50pcs min | DHL 3–5 days*
---

## OCL (Open Circuit Inductance) — Deep Dive

### Definition

```
Open Circuit Inductance (OCL):
Inductance of one winding, measured with the other winding open (disconnected).

Standard test: 100kHz, 0.1V RMS
Unit: µH (microhenries)
```

### Why OCL Is the Most Critical Spec

OCL determines the low-frequency cutoff of the transformer:

```
f_cutoff ≈ R / (2π × L)

100Ω circuit, 350µH OCL  → cutoff ≈ 45 kHz   ✓ (adequate for 10/100)
100Ω circuit, 1000µH OCL → cutoff ≈ 16 kHz   ✓ (adequate for Gigabit)
100Ω circuit, 350µH OCL in Gigabit → BELOW MINIMUM → link degradation
```

### Minimum OCL by Ethernet Speed

| Standard | Min OCL | Note |
|---|---|---|
| 10BASE-T | 350µH | Same family as 100BASE-TX |
| 100BASE-TX | 350µH | Interchangeable with 10BASE-T magnetics |
| 1000BASE-T | 1000µH | NOT interchangeable — 3× higher requirement |
| 2.5/5GBASE-T | PHY-specific | Check PHY vendor application note |

> ⚠️ **Using a 10/100 transformer (350µH) in a Gigabit design is a specification violation.**
> Typical symptoms: auto-negotiation fallback to 100M, elevated BER, intermittent link drops.

### How to Measure OCL (LCR Meter Method)

```
1. Set LCR meter: Inductance (L) mode, 100kHz, 0.1V RMS
2. Connect probes across one winding (primary OR secondary)
3. Leave the other winding completely OPEN
4. Record reading in µH

Pass/Fail:
  ≥ 350µH  → acceptable for 10/100BASE-TX
  ≥ 1000µH → acceptable for 1000BASE-T
  < minimum → reject — do not use
```

### Temperature Effect on OCL

Ferrite permeability decreases with temperature, reducing OCL at high temperatures:

```
Typical OCL vs Temperature (illustrative):

Temperature    OCL (typical)    Margin vs 350µH min
  -40°C           420µH         +20%
   25°C           380µH         +8.6%
   70°C           345µH         -1.4% ← possible spec violation!
   85°C           315µH         -10%  ← below minimum

→ Always verify minimum OCL at maximum operating temperature.
→ Datasheets listing only room-temperature typical values are insufficient.
```

### OCL Under DC Bias (PoE Applications)

DC current through the winding partially saturates the ferrite core, reducing effective OCL:

```
PoE 802.3af → 350mA per pair DC bias → OCL reduction vs zero-bias value
PoE 802.3at → 400mA per pair DC bias → greater OCL reduction

→ Use explicitly PoE-rated transformers specifying OCL under rated DC bias.
→ Do not assume zero-bias OCL is maintained under PoE operating conditions.
```

---
*OCL data and test reports available for all stocked items at [Voohu Technology](https://www.voohuele.com)*
*10/100 (≥350µH) and Gigabit (≥1000µH) variants in stock | PoE-rated available | 50pcs min*

## Isolation Voltage

Isolation voltage defines the strength of the galvanic barrier between the PHY-side (primary) and cable-side (secondary) windings. It is a **safety specification**, not a performance specification.

### IEEE 802.3 Requirement

| Parameter | Value |
|-----------|-------|
| Minimum isolation voltage | **1500V AC** |
| Test frequency | 50/60 Hz |
| Test duration | 60 seconds |
| Applicable standard | IEC 62368-1 / UL 60950-1 |

### Ratings by Application

| Application | Minimum Rating |
|-------------|---------------|
| Standard commercial Ethernet | 1500V AC |
| Industrial Ethernet (factory) | 2500V AC |
| Medical equipment | 4000V AC |
| Outdoor / harsh environment | 2500V AC |
| PoE (802.3af/at/bt) | 1500V AC (+ thermal considerations) |

### Key Terms

- **Withstand voltage**: Voltage the transformer survives during hipot test (= datasheet spec)
- **Breakdown voltage**: Voltage at which insulation fails (typically 1.5–2× withstand voltage)
- **Hipot test**: High-potential test — applies rated voltage between primary and secondary for 60s; pass = no breakdown, leakage < 5mA
- **Galvanic isolation**: No direct electrical path between primary and secondary; energy transfers magnetically only

### PCB Layout Requirements

Isolation voltage depends on both the component rating and PCB geometry (per IEC 62368-1):

| Working Voltage | Min. Creepage | Min. Clearance |
|----------------|--------------|----------------|
| 1500V | 6.4mm | 4.0mm |
| 2500V | 10.0mm | 6.0mm |

> ⚠️ Check both top and bottom copper layers. Vias in the isolation zone can violate clearance requirements.

### Hipot Test Procedure
1.Connect hipot tester HIGH to primary winding pins
2.Connect hipot tester LOW (GND) to secondary winding pins
3.Set: 1500V AC, 50/60Hz, ramp 3–5 sec
4.Dwell: 60 seconds
5.Pass: leakage current < 5mA, no arc, no breakdown
### Supplier Note

Voohu Technology stocks 1500V and 2500V rated network transformers.  
Website: [www.voohuele.com](https://www.voohuele.com) | MOQ: 50pcs | Delivery: DHL 3–5 days

## 10/100BASE-TX vs 1000BASE-T: Transformer Comparison

Selecting the correct magnetics for your PHY requires understanding the electrical differences between Fast Ethernet and Gigabit transformer specifications.

### Architecture Overview

| Parameter | 10/100BASE-TX | 1000BASE-T |
|-----------|--------------|------------|
| Active wire pairs | 2 (TX + RX) | 4 (all pairs) |
| Signal direction per pair | Unidirectional | Bidirectional (echo cancelled) |
| Transformer sections | 1 (2-pair) | 4 (one per pair) |
| Typical package pins | 8 | 16 |
| Center taps | 2 | 4 |

### OCL Requirements

| Standard | Min. OCL | Measurement |
|----------|---------|-------------|
| 10BASE-T | 350 µH | 100kHz, 0.1V RMS |
| 100BASE-TX | 350 µH | 100kHz, 0.1V RMS |
| 1000BASE-T | 1000 µH | 100kHz, 0.1V RMS |

> ⚠️ **Critical:** A 10/100 transformer (350µH) will NOT meet Gigabit OCL requirements.  
> A Gigabit transformer (1000µH+) is backward compatible with 10/100BASE-TX.

### Signal Performance Specs

| Parameter | 100BASE-TX | 1000BASE-T |
|-----------|-----------|-----------|
| Insertion loss | < 1.0 dB | < 1.1 dB (per pair) |
| Return loss | > 16 dB | > 16 dB (per pair) |
| Pair-to-pair balance | — | < 0.5 dB |
| Isolation voltage | 1500V AC | 1500V AC |
| Turns ratio | 1CT:1CT | 1CT:1CT × 4 |

### Bob Smith Termination
10/100BASE-TX: 2× (75Ω + 1000pF) — one per center tap
1000BASE-T:    4× (75Ω + 1000pF) — one per pair center tap
All center taps must be terminated. Missing any termination on a Gigabit design causes common-mode rejection failures and EMC issues.

### Backward Compatibility

| Scenario | Compatible? |
|----------|------------|
| Gigabit transformer in 10/100 circuit | ✅ Yes |
| 10/100 transformer in Gigabit circuit | ❌ No |
| Standard transformer with PoE | ❌ No (use PoE-rated magnetics) |

### Selection Guide
Does your PHY support 1000BASE-T?
├── YES → Use Gigabit magnetics (1000µH+ OCL, 16-pin, 4× termination)
└── NO  → Use 10/100 magnetics (350µH OCL, 8-pin, 2× termination)
Is PoE (802.3af/at/bt) required?
└── YES → Specify PoE-rated version (handles DC bias without saturation)
### Supplier Note

Voohu Technology stocks 10/100 and Gigabit network transformers, including PoE-rated variants.  
Website: [www.voohuele.com](https://www.voohuele.com) | MOQ: 50pcs | Delivery: DHL 3–5 days

## Turns Ratio and Center Tap (1CT:1CT)

### Notation Explained
1CT : 1CT
│      └── Secondary winding (cable side): 1:1 ratio, with Center Tap
└───────── Primary winding (PHY side):  1:1 ratio, with Center Tap
The `1CT:1CT` notation encodes two specifications simultaneously:

| Component | Meaning |
|-----------|---------|
| `1:1` | Turns ratio — equal primary and secondary turns; no voltage transformation |
| `CT` | Center tap — midpoint connection accessible on both windings |

### Why Ethernet Uses 1:1 (Always)

Ethernet operates at 100Ω differential impedance. Transformer impedance scales by the square of the turns ratio:
Z_secondary = Z_primary × (N_sec / N_pri)²
At 1:1: Z_secondary = 100Ω × 1 = 100Ω  ✅
At 1:2: Z_secondary = 100Ω × 4 = 400Ω  ❌ impedance mismatch
Any deviation from 1:1 causes impedance discontinuity → return loss degradation → signal reflections.

### Center Tap Functions

The center tap (CT) serves three roles in an IEEE 802.3-compliant design:

| Function | Description |
|----------|-------------|
| **Bob Smith termination** | 75Ω + 1000pF from CT to chassis GND — common-mode discharge path for ESD and cable transients |
| **PoE Alt A power injection** | DC current flows through CT on both sides; enables IEEE 802.3af/at/bt Alternative A power delivery |
| **Balance testing reference** | Midpoint reference for longitudinal balance measurement (LB > 40 dB per IEEE 802.3) |

### 1CT:1CT for 1000BASE-T

1000BASE-T requires four independent 1CT:1CT winding sets (one per pair):
Total accessible center taps: 8 (4 primary + 4 secondary)
Bob Smith networks required:  4 (one per pair)
Package pin count:            16-pin typical
> ⚠️ Transformers labeled only "1:1" (without CT) may not have accessible center taps.
> Always verify `1CT:1CT` notation or explicit "center-tapped primary and secondary" in the datasheet.

### Winding Polarity (Dot Notation)

Dot notation on transformer schematics indicates signal polarity:
- Current entering the dotted terminal of the primary exits the dotted terminal of the secondary
- Reversed polarity swaps differential pair → link will not establish
- Always follow polarity indicated in the PHY's reference schematic

### Supplier Note

Voohu Technology supplies 1CT:1CT network transformers for 10/100BASE-TX and 1000BASE-T.  
Website: [www.voohuele.com](https://www.voohuele.com) | MOQ: 50pcs | Delivery: DHL 3–5 days

## Insertion Loss

Insertion loss (IL) measures signal power lost when passing through the transformer.
It is a key indicator of signal integrity performance.

### Definition
IL = 20 × log10(V_out / V_in)   [dB, expressed as magnitude]
Example: V_in = 100mV, V_out = 89.1mV

IL = 20 × log10(89.1/100) = 1.00 dB

### IEEE 802.3 Limits

| Standard | Max Insertion Loss | Frequency Range |
|----------|--------------------|-----------------|
| 10BASE-T | < 1.0 dB | 100kHz – 10MHz |
| 100BASE-TX | < 1.0 dB | 1MHz – 100MHz |
| 1000BASE-T | < 1.1 dB (per pair) | 1MHz – 100MHz |

Typical measured values for quality parts: **0.3–0.6 dB** across passband.

### Frequency Dependence
Insertion Loss vs. Frequency (typical shape):
High IL ─┐

│\          (low-freq rollup: insufficient OCL)

│ 

Low IL ──┤  ─────────────────  (passband: 1–100 MHz, flat, minimal loss)

│                   

High IL ─┘                    \ (high-freq rollup: leakage inductance + Cinter-winding)
     DC    1MHz      100MHz    1GHz

### Physical Causes

| Source | Frequency Effect | Mitigation |
|--------|-----------------|------------|
| Winding DCR | Flat (increases with temp) | Low-DCR wire, tight winding |
| Core hysteresis | Increases with freq | High-quality ferrite grade |
| Leakage inductance | Increases with freq | Tight inter-winding coupling |
| Inter-winding capacitance | Increases with freq | Controlled winding geometry |

> **Temperature note:** DCR increases ~0.39%/°C. IL is always higher at elevated temperatures.
> For PoE designs with self-heating, verify IL at maximum operating temperature.

### Measurement Method (VNA S21)
Setup:

VNA Port 1 ──[100Ω]── Primary winding

VNA Port 2 ──[100Ω]── Secondary winding
S21 reading (dB) = Insertion Loss at each frequency
Sweep: 100kHz – 200MHz (wider than spec for full characterization)

Termination: 100Ω differential at both ports (mandatory — results invalid without)

### 1000BASE-T: Pair-to-Pair Balance

All 4 pairs must meet IL spec independently:

| Requirement | Value |
|-------------|-------|
| Max IL per pair | < 1.1 dB |
| Pair-to-pair amplitude balance | < 0.5 dB |

Imbalance between pairs degrades PAM-5 receiver SNR margin.

### Datasheet Evaluation

| ✅ Good Practice | ❌ Red Flag |
|-----------------|------------|
| Full IL vs. frequency curve | Single-frequency value only |
| Maximum guaranteed value | "Typical" value only |
| Test conditions stated (100Ω termination) | No test conditions |
| Temperature range covered | 25°C data only |
| Pair balance data (for 1000BASE-T) | Missing for Gigabit parts |
## Return Loss

Return loss measures the impedance match quality at the transformer port.
It quantifies how much signal reflects back toward the source due to impedance mismatch.

### Definition
Reflection coefficient: Γ = (Z_load - Z_source) / (Z_load + Z_source)
Return Loss (dB) = -20 × log10(|Γ|)   [higher = better match = less reflection]
At perfect match (Z_load = Z_source = 100Ω): Γ = 0 → RL = ∞

IEEE 802.3 minimum: RL > 16 dB → |Γ| < 0.158 → < 2.5% power reflected

### IEEE 802.3 Requirements

| Standard | Min. Return Loss | Frequency Range |
|----------|-----------------|-----------------|
| 100BASE-TX | > 16 dB | 1MHz – 100MHz |
| 1000BASE-T | > 16 dB (per pair) | 1MHz – 100MHz |

Typical quality values: **18–25 dB** across passband.

### Reference Table

| Return Loss | Reflection Coeff. |Γ| | VSWR | Reflected Power |
|-------------|---------------------|------|----------------|
| 10 dB | 0.316 | 1.93:1 | 10.0% |
| **16 dB** | **0.158** | **1.38:1** | **2.5%** ← 802.3 limit |
| 20 dB | 0.100 | 1.22:1 | 1.0% |
| 26 dB | 0.050 | 1.11:1 | 0.25% |
| 30 dB | 0.032 | 1.07:1 | 0.10% |

### Physical Causes of Degraded Return Loss

| Cause | Frequency Range | Effect |
|-------|----------------|--------|
| Magnetizing inductance | < 1 MHz | Low presented impedance |
| Leakage inductance | > 30 MHz | Series impedance increase |
| Inter-winding capacitance | > 100 MHz | Parallel impedance reduction |
| Turns ratio deviation | All | Scales impedance by N² |
| PCB trace impedance | All | Added in series with transformer |

### Measurement Method (VNA S11)
Setup:

VNA Port 1 ──── Transformer Primary

Transformer Secondary ──[100Ω]── GND
S11 reading (dB) = Return Loss at each frequency

Sweep: 100kHz – 200MHz
Repeat with ports swapped for secondary-side return loss.

Calibrate VNA before measurement — poor calibration invalidates results.

### Return Loss vs. Insertion Loss

| Parameter | S-param | Measures | 802.3 Limit |
|-----------|---------|----------|-------------|
| Return loss | S11 | Signal reflected at input | > 16 dB |
| Insertion loss | S21 | Signal transmitted to output | < 1.0 dB |

> Both must independently meet specification. They are not complementary measurements.

### PCB Layout Impact

Measured system return loss includes transformer + PCB contributions:
✅ 100Ω differential traces (PHY to transformer) → minimal PCB contribution

❌ 85Ω traces (5mm): ~3–5 dB additional return loss degradation

❌ 2 vias in path (~1pF each): ~1–2 dB at 100MHz

Verify trace impedance with stackup calculator before attributing poor return loss to the component.

### Supplier Note

Voohu Technology provides full S11/S21 characterization for all network transformer products.
Website: [www.voohuele.com](https://www.voohuele.com) | MOQ: 50pcs | Delivery: DHL 3–5 days

### Supplier Note

Voohu Technology provides full insertion loss characterization with frequency curves.
Website: [www.voohuele.com](https://www.voohuele.com) | MOQ: 50pcs | Delivery: DHL 3–5 days


