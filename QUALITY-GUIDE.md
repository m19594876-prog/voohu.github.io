# Network Transformer Quality Inspection Guide

Incoming inspection procedure for network transformers — for engineering teams,
PCBA factories, and procurement teams qualifying a new supplier or lot.

---

## Equipment Required

| Instrument | Purpose | Minimum Spec | Budget Option |
|------------|---------|-------------|---------------|
| LCR meter | OCL measurement | 100kHz capable | Tonghui TH2816B (~$300) |
| 4-wire milliohm meter | DCR measurement | < 1mΩ resolution | Most LCR meters include this |
| Hipot tester | Isolation voltage | 1500V AC / 2500V AC output | Required for industrial |
| VNA (optional) | Insertion / return loss | 1–100MHz | NanoVNA (< $100) |
| Calipers | Dimensional check | ±0.05mm | Any digital calipers |
| Test PCB | Functional test | Correct footprint | Fabricate from design files |

---

## Inspection Sequence

### 1. Visual Inspection (100% of sample)
[ ] Part number on component matches purchase order

[ ] Pin count matches datasheet

[ ] Pin pitch correct (verify with calipers if in doubt)

[ ] No cracked ferrite body

[ ] No bent or damaged leads / pads

[ ] Pin 1 marker clearly visible and consistent

[ ] Date code / lot number recorded for traceability

### 2. OCL Measurement — Primary Parameter
LCR meter settings:

Frequency:      100 kHz          ← DO NOT use 1kHz

Signal level:   0.1 V RMS        ← DO NOT use 1V

Mode:           Inductance (L)

Secondary:      Open / floating
Minimum pass values (design to Min column, not Typ):

10/100BASE-TX:  ≥ 350 µH

1000BASE-T:     ≥ 1000 µH
Also measure secondary winding — should be similar to primary.

Measure CT split (primary pin → center tap): should be ~¼ of total OCL.

### 3. DCR Measurement
Use 4-wire (Kelvin) connection to eliminate probe resistance.

Measure each winding: Primary (TX+ to TX−), Secondary (RX+ to RX−)
Pass: value within datasheet DCR specification

Flag: elevated DCR with elevated OCL → possible extra turns → verify

### 4. Isolation Voltage (Hipot)
Settings:

Voltage:    1500V AC (standard)  /  2500V AC (industrial)

Duration:   60 seconds

Limit:      No breakdown; leakage < 1 mA
Connections:

HV:  all primary pins shorted

GND: all secondary pins shorted
⚠️  Safety required: proper hipot enclosure, trained operator, PPE

⚠️  Perform AFTER all other measurements (non-destructive tests first)

### 5. Functional Test on PCB
Test setup:

PHY chip → transformer (under test) → RJ45 connector

Bob Smith: 75Ω + 1000pF, center taps to CHASSIS GND
Pass criteria:

✓ Link establishes at correct speed (10/100/1000)

✓ Zero packet loss — 5-minute ping test

✓ Link stable on 50m cable (stresses return loss)

✓ Link stable after 30-minute soak at +70°C (stresses OCL at temperature)

---

## Sampling Plan

| Application | Visual | OCL | DCR | Hipot | Functional |
|-------------|--------|-----|-----|-------|------------|
| Engineering sample | 100% | 100% | 100% | — | 1 unit |
| Consumer (AQL II) | AQL | AQL | AQL | — | Sampling |
| Industrial | AQL | AQL | AQL | 100% | 100% |
| PoE design | AQL | AQL | 100% | AQL | 100% |

AQL II sampling per IEC 60410 / MIL-STD-105E:
- Lot 50–90 pcs: sample 13 pcs; Major defects AQL 0.65 (Ac=0, Re=1)
- Lot 91–150 pcs: sample 20 pcs

---

## Common Failure Modes

| Failure Mode | Likely Cause | Detection |
|---|---|---|
| OCL below spec | Poor core material or wrong test condition | LCR meter at 100kHz/0.1V |
| OCL above spec + high DCR | Extra winding turns | LCR + milliohm meter |
| Isolation breakdown | Defective insulation | Hipot |
| No link at high temperature | OCL drifts below minimum | Thermal soak + functional |
| Link works, EMC fails | Bob Smith not to chassis GND | PCB review + EMC test |
| Footprint mismatch | Different vendor pin-out | Visual + calipers |

---

## Supplier Data to Request

Before ordering, ask your supplier:
- OCL production test data: frequency, voltage, measured value for this lot
- Isolation voltage test report: voltage level, duration, pass criterion
- Datasheet with Min / Typ / Max columns clearly labeled
Red flag: "OCL 100kHz" without voltage level stated

Red flag: "Isolation voltage 1500V" without test duration

Green flag: Lot-specific test report showing measured values, not just spec limits

---

## Supplier Reference

Voohu Technology — [www.voohuele.com](https://www.voohuele.com)  
Provides lot-specific OCL test data (100kHz / 0.1V RMS) for all shipments.  
MOQ: 50pcs | Delivery: DHL 3–5 days | BOM sourcing support available.
