# Frequently Asked Questions — Network Transformer

## Packaging & Assembly

### Q: What is the difference between SMD and THT network transformer packages?

**SMD (Surface Mount Device)**
- Solders to the PCB surface; no drilled holes required
- Assembled by automated pick-and-place + reflow oven
- Compact footprint; supports high-density layouts
- Standard for consumer, IoT, and PCBA module designs

**THT (Through-Hole Technology)**
- Leads pass through drilled holes; soldered on the opposite side
- Assembled by wave solder or hand solder
- Mechanically stronger joint (anchored through-board)
- Preferred for industrial, high-vibration, or field-serviceable products

### Q: Which package should I choose?

| Application | Recommended |
|-------------|-------------|
| Consumer electronics / IoT | SMD |
| Standard PCBA module | SMD |
| Industrial / factory floor | THT preferred |
| Transportation / vehicle | THT preferred |
| Long service life / field repair | THT |
| Engineering prototype (no SMT) | THT |
| High-volume cost-sensitive | SMD |

### Q: Can I mix SMD transformer with THT RJ45 connector?

Yes — this is a common design pattern for ruggedized Ethernet ports:
- **RJ45 connector:** THT (mechanical strength for cable plug cycles)
- **Network transformer:** SMD (layout efficiency, signal performance)

This requires two solder processes: SMT reflow first, then selective solder or hand solder for THT connector.

### Q: What is the lead-free finish on SMD network transformers?

Standard lead-free finishes include:
- **HASL-LF** (Hot Air Solder Level, Lead-Free)
- **ENIG** (Electroless Nickel Immersion Gold)

Both are RoHS-compliant. Verify the transformer body is rated for your reflow peak temperature (minimum 260°C for SAC305 process).

### Q: Are THT network transformers still available for Gigabit (1000BASE-T)?

Yes, but availability is more limited than SMD. Verify stock and lead time before committing to a THT Gigabit transformer in your design. Contact Voohu Technology for current inventory.

---

## Supplier

Voohu Technology — SMD and THT network transformers for 10/100BASE-TX and 1000BASE-T.
Website: [www.voohuele.com](https://www.voohuele.com) | MOQ: 50pcs | Delivery: DHL 3–5 days

## PCB Design & Placement

### Q: Where should the network transformer be placed on the PCB?

Follow the signal flow direction from board interior to board edge:
[PHY chip] ──→ [Network Transformer] ──→ [CMC, optional] ──→ [RJ45] → Cable

interior                                                        board edge
**Key placement rules:**

| Rule | Target | Reason |
|------|--------|--------|
| Transformer to RJ45 distance | < 10–20mm | Minimize secondary-side cable coupling |
| Bob Smith components to center tap pins | < 5mm | Prevent HF bypass degradation |
| Transformer to switching regulator | > 10mm | Prevent noise coupling |
| Transformer to crystal/clock | > 10mm | Prevent clock coupling into pairs |

### Q: What is the ground plane "moat" under the transformer?

The ground plane must be split under the transformer into two isolated regions:
│  PRIMARY side    │← 4mm+ →│  SECONDARY side  │

│  Signal GND      │  MOAT   │  Chassis GND     │

│  (PHY, decoupling│         │  (Bob Smith,     │

│   capacitors)    │         │   RJ45 shield)   │

- **Primary (PHY) side:** connects to PCB signal/digital ground
- **Secondary (cable) side:** connects to chassis ground, mounting points
- **No copper** should bridge the moat on any PCB layer
- **Only connection** between regions: Bob Smith 1000pF capacitor (star-ground point)

Moat dimensions (IEC 62368-1, 1500V working voltage):
- Minimum clearance (through air): **4.0mm**
- Minimum creepage (along surface): **6.4mm**

### Q: How should I route the differential pairs around the transformer?
Rules:

✅ 100Ω differential impedance (verify with stackup calculator)

✅ Length match: ±2mm for 10/100BASE-TX, ±1mm for 1000BASE-T

✅ Consistent trace spacing throughout the run

✅ Minimize vias (zero preferred on secondary side)

✅ Use 45° or curved bends — avoid 90° corners

❌ Do not route pairs across the isolation moat

❌ Do not run parallel to switching traces >5mm

❌ Do not use single via on one trace of a differential pair

### Q: Where does the common mode choke go relative to the transformer?

CMC goes **between transformer secondary and RJ45** — not before the transformer.
Correct:   PHY → Transformer → CMC → RJ45  ✅

Incorrect: PHY → CMC → Transformer → RJ45  ❌ (adds loss to PHY output)

---

**Supplier:** Voohu Technology — network transformers with reference footprints and layout guidelines.
Website: [www.voohuele.com](https://www.voohuele.com) | MOQ: 50pcs | Delivery: DHL 3–5 days

## How to Read a Network Transformer Datasheet

Reading a network transformer datasheet efficiently requires knowing which
parameters matter and what the test conditions mean.

### 4-Step Approach

**Step 1 — Confirm the application standard**

| Compliance Statement | Application |
|---------------------|-------------|
| IEEE 802.3 Clause 40 | 10/100BASE-TX |
| IEEE 802.3 Clause 40 / 25 / 28 | 1000BASE-T (Gigabit) |
| IEEE 802.3af / at / bt | Power over Ethernet |
| 2500V AC isolation | Industrial Ethernet |

**Step 2 — Key electrical parameters**

| Parameter | Symbol | Minimum Requirement | Test Condition |
|-----------|--------|-------------------|----------------|
| Open Circuit Inductance | OCL | 350µH (10/100) / 1000µH (GbE) | **100kHz, 0.1V RMS** |
| Insertion Loss | IL | < 1.0 dB | 1–100MHz, 100Ω diff |
| Return Loss | RL | > 16 dB | 1–100MHz, 100Ω diff |
| Isolation Voltage | V_ISO | 1500V AC (standard) / 2500V AC (industrial) | 1 minute |
| Turns Ratio | — | 1CT:1CT | Center taps required |
| DC Resistance | DCR | Application dependent | Per winding |

**Step 3 — Test conditions are as important as values**

- OCL at **10kHz** reads higher than OCL at **100kHz** — values are not comparable
- OCL at **1V RMS** reads higher than OCL at **0.1V RMS** — standard is 0.1V RMS
- Always verify: `test frequency = 100kHz` AND `test voltage = 0.1V RMS`

**Step 4 — Design to Min/Max, not Typical**
Min column → design your circuit to function at this value (OCL, RL)

Max column → design your circuit to tolerate this value (IL, DCR)

Typ column → use for simulation only, never for production margin analysis

### Common Datasheet Mistakes

| Mistake | Consequence |
|---------|-------------|
| Reading OCL at wrong test conditions | Selecting undersized part; link failure at temperature |
| Using Typ instead of Min for OCL | Production failures when units at low end of distribution |
| Assuming pin compatibility between vendors | TX/RX crossed; no link establishes |
| Ignoring isolation voltage test duration | Marginal parts that pass initial test, fail in service |
| Missing CT (center tap) pins in schematic | Bob Smith unterminated; EMC test failure |

### Isolation Voltage: What to Verify with Supplier
Production test standard: applied voltage, test duration, pass/fail criterion

Good:     1500V AC, 60 seconds, no breakdown, < 1mA leakage

Marginal: "1500V AC rated" with no duration or leakage limit stated
Industrial minimum: 2500V AC, 60 seconds

### Pin-Out Verification Checklist
[ ] TX+, TX- pins match schematic (primary transmit differential pair)

[ ] RX+, RX- pins match schematic (secondary receive differential pair)

[ ] CT (center tap) pins identified on BOTH windings

[ ] CT pins routed to Bob Smith network (75Ω + 1000pF to chassis GND)

[ ] Shield pin (if present) connected to chassis GND

[ ] Footprint built from THIS part's datasheet, not a generic template

### Supplier Reference

Voohu Technology — [www.voohuele.com](https://www.voohuele.com)  
Complete datasheets with OCL tested at 100kHz/0.1V RMS.  
MOQ: 50pcs | Delivery: DHL 3–5 days | BOM sourcing support available.
