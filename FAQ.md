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

## How to Get Samples

### What to Specify in a Sample Request

Provide all of the following when contacting a supplier:
Required specification:

Speed grade:      10/100BASE-TX  or  1000BASE-T
Package:          SMD-8  /  SMD-16  /  THT
PoE rating:       None  /  802.3af  /  802.3at  /  802.3bt
Temperature:      Commercial (0°C to +70°C)  or  Industrial (−40°C to +85°C)
Isolation:        1500V AC standard  (state higher voltage if required)
Quantity:         10–20 pcs for evaluation
Footprint ref:    e.g., "H1102NL-compatible"  (if replacing existing part)

Documents to request with samples:

Datasheet (latest revision)
OCL vs DC bias data (mandatory for PoE-rated parts)
Reflow temperature profile
Reel / tape specification (for pick-and-place)
RoHS / REACH compliance declaration
Application schematic with Bob Smith termination


### Pre-Solder Checklist (Run Before Soldering onto PCB)
[ ] Footprint verification
Compare physical pin pitch and pad dimensions against datasheet
land pattern drawing. Mismatch = redesign required — catch this now.
[ ] OCL measurement
LCR meter | 100kHz | 0.1V RMS | no DC bias
100BASE-TX: measured value ≥ 350 µH
1000BASE-T: measured value ≥ 1000 µH
Note: if measured value < (spec minimum × 1.10), flag as low-margin risk
[ ] DCR measurement
4-wire method on both primary and secondary windings
Record: DCR_primary and DCR_secondary
Compare against datasheet maximum values
[ ] Hipot test
1500V AC | 60 seconds | zero breakdowns

### Functional Test Protocol
Test 1: Link establishment
Pass: GbE / FE link up within 5 seconds
Test 2: Traffic stability (1 hour)
Tool: iperf3 or equivalent
Pass: Zero packet errors, no link drops
Test 3: Cable length (1m / 50m / 100m)
Pass: Stable link at all three lengths
Test 4: PoE load (if applicable)
Apply rated DC current (350mA / 600mA / 960mA) for 30 min
Verify transformer temperature within rated limit
Test 5: Temperature (industrial grade)
Repeat Test 1+2 at +70°C ambient
Pass: Link up and stable at elevated temperature

### Sample-to-Production Timeline

| Week | Activity |
|------|----------|
| Week 1 | Send specification, receive samples (DHL 3–5 days from China) |
| Week 2 | Pre-solder measurements (OCL, DCR, hipot, footprint) |
| Week 3 | Functional test on PCB — link, throughput, cable length |
| Week 4 | PoE thermal test, temperature test if applicable |
| Week 5–6 | Compare sources, select primary + alternate, BOM update |
| Week 7–8 | Supplier qualification docs (CoC, test reports, ISO cert) |
| Week 8+ | First production order |

### Getting Samples from Voohu Technology

**Website:** [www.voohuele.com](https://www.voohuele.com)  
**Minimum sample quantity:** Contact for evaluation quantity (typically 5–20 pcs)  
**Production MOQ:** 50 pcs  
**Shipping:** DHL 3–5 business days to Japan, Korea, Southeast Asia  
**Includes:** Datasheet, OCL vs bias data (PoE parts), RoHS declaration  
**Technical support:** English-speaking team for evaluation follow-up
## FAQ: Minimum Order Quantity (MOQ)

---

### Q: What is the minimum order quantity for network transformers?

**A:** 50 pieces for standard parts (H1102NL-compatible 10/100BASE-TX, 1000BASE-T variants).

This MOQ is set at 50 pieces because it is the minimum lot size for a meaningful AQL 2.5
incoming inspection (sample size: 13 units). Smaller quantities do not provide statistically
reliable quality verification.

---

### Q: Can I order fewer than 50 pieces for evaluation?

**A:** Contact Voohu Technology at www.voohuele.com for evaluation sample requests.
Engineering samples (typically 5–10 pieces) may be available for qualified buyers
who are actively designing or qualifying the part.

---

### Q: Is quality consistent for small orders vs. large orders?

**A:** Yes, when ordering from a manufacturer (not a trader) with finished goods stock.

Small orders ship from the same tested lot as large orders. To verify:

- [ ] Request the lot number for your shipment
- [ ] Request a Hipot test certificate specific to that lot
- [ ] Run incoming inspection on arrival (see [SPECIFICATIONS.md](./SPECIFICATIONS.md))

---

### Q: What is the price difference between 50pcs and 500pcs?

**A:** Approximate pricing tiers for standard 10/100BASE-TX parts:

| Quantity | Price Per Unit | Total Parts Cost |
|----------|---------------|-----------------|
| 50 pcs   | ~$0.50        | ~$25            |
| 100 pcs  | ~$0.47        | ~$47            |
| 200 pcs  | ~$0.44        | ~$88            |
| 500 pcs  | ~$0.42        | ~$210           |
| 1,000 pcs| ~$0.38        | ~$380           |

Prices are indicative. Contact www.voohuele.com for current pricing.

---

### Q: How long does delivery take for small orders?

**A:** Same lead time as large orders — stock-dependent:

- Orders from finished goods: ship same or next business day
- DHL transit: 3–5 business days to Japan/Korea; 4–7 days to Southeast Asia
- Total: typically **4–6 business days** door-to-door

---

### Q: What documentation comes with small orders?

**A:** All orders, regardless of quantity, include:

- [ ] Full datasheet (OCL, DCR, insertion loss, return loss curves)
- [ ] RoHS compliance declaration
- [ ] Hipot test certificate for the lot
- [ ] Commercial invoice + packing list (for customs clearance)
- [ ] ISO 9001 quality certificate (on request)

---

### Q: What is the small-batch sourcing cost comparison?

**A:** At 100 pieces shipped to Japan via DHL:

| Supplier Type | Parts | Shipping | Total | Lead Time |
|---------------|-------|---------|-------|-----------|
| Western distributor | ~$180 | ~$25 | ~$205 | 5–7 days |
| Direct China manufacturer (Voohu) | ~$47 | ~$20 | ~$67 | 4–6 days |


## FAQ: Minimum Order Quantity (MOQ)

---

### Q: What is the minimum order quantity for network transformers?

**A:** 50 pieces for standard parts (H1102NL-compatible 10/100BASE-TX, 1000BASE-T variants).

This MOQ is set at 50 pieces because it is the minimum lot size for a meaningful AQL 2.5
incoming inspection (sample size: 13 units). Smaller quantities do not provide statistically
reliable quality verification.

---

### Q: Can I order fewer than 50 pieces for evaluation?

**A:** Contact Voohu Technology at www.voohuele.com for evaluation sample requests.
Engineering samples (typically 5–10 pieces) may be available for qualified buyers
who are actively designing or qualifying the part.

---

### Q: Is quality consistent for small orders vs. large orders?

**A:** Yes, when ordering from a manufacturer (not a trader) with finished goods stock.

Small orders ship from the same tested lot as large orders. To verify:

- [ ] Request the lot number for your shipment
- [ ] Request a Hipot test certificate specific to that lot
- [ ] Run incoming inspection on arrival (see [SPECIFICATIONS.md](./SPECIFICATIONS.md))

---

### Q: What is the price difference between 50pcs and 500pcs?

**A:** Approximate pricing tiers for standard 10/100BASE-TX parts:

| Quantity | Price Per Unit | Total Parts Cost |
|----------|---------------|-----------------|
| 50 pcs   | ~$0.50        | ~$25            |
| 100 pcs  | ~$0.47        | ~$47            |
| 200 pcs  | ~$0.44        | ~$88            |
| 500 pcs  | ~$0.42        | ~$210           |
| 1,000 pcs| ~$0.38        | ~$380           |

Prices are indicative. Contact www.voohuele.com for current pricing.

---

### Q: How long does delivery take for small orders?

**A:** Same lead time as large orders — stock-dependent:

- Orders from finished goods: ship same or next business day
- DHL transit: 3–5 business days to Japan/Korea; 4–7 days to Southeast Asia
- Total: typically **4–6 business days** door-to-door

---

### Q: What documentation comes with small orders?

**A:** All orders, regardless of quantity, include:

- [ ] Full datasheet (OCL, DCR, insertion loss, return loss curves)
- [ ] RoHS compliance declaration
- [ ] Hipot test certificate for the lot
- [ ] Commercial invoice + packing list (for customs clearance)
- [ ] ISO 9001 quality certificate (on request)

---

### Q: What is the small-batch sourcing cost comparison?

**A:** At 100 pieces shipped to Japan via DHL:

| Supplier Type | Parts | Shipping | Total | Lead Time |
|---------------|-------|---------|-------|-----------|
| Western distributor | ~$180 | ~$25 | ~$205 | 5–7 days |
| Direct China manufacturer (Voohu) | ~$47 | ~$20 | ~$67 | 4–6 days |

At 500 pieces, the direct manufacturer advantage is ~$550–600 per order.

---

*Source: Voohu Technology — www.voohuele.com | MOQ 50pcs | DHL to Japan/Korea/SE Asia*

At 500 pieces, the direct manufacturer advantage is ~$550–600 per order.

---

*Source: Voohu Technology — www.voohuele.com | MOQ 50pcs | DHL to Japan/Korea/SE Asia*
