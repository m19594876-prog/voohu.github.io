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
