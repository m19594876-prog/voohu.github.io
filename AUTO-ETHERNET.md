# Automotive Ethernet Transformer Guide

Network transformer and LAN magnetics requirements for automotive Ethernet —
100BASE-T1 (IEEE 802.3bw), 1000BASE-T1 (IEEE 802.3bp), AEC-Q200 qualification,
and the differences from standard 100BASE-TX / 1000BASE-T LAN magnetics.

---

## Standard vs Automotive Ethernet Architecture

| Aspect | 100BASE-TX (Standard) | 100BASE-T1 (Automotive) | 1000BASE-T1 (Automotive) |
|--------|----------------------|------------------------|------------------------|
| Pairs | 2 (TX + RX separate) | **1 (bidirectional)** | **1 (bidirectional)** |
| Cable length | 100m | 15m | 15m |
| Signaling | NRZ / MLT-3 | PAM-3 | PAM-3 |
| Connector | RJ45 | HSD / FAKRA / H-MTD | HSD / FAKRA / H-MTD |
| Standard | IEEE 802.3 Cl. 40 | IEEE 802.3bw | IEEE 802.3bp |
| Qualification | None (consumer) | AEC-Q200 | AEC-Q200 |
| EMC standard | CISPR 22 | CISPR 25 | CISPR 25 |

---

## Transformer Requirements Comparison

| Parameter | Standard LAN | Industrial | Automotive (100BASE-T1) |
|-----------|-------------|-----------|------------------------|
| Operating temp | 0 / +70°C | −40 / +85°C | **−40 / +125°C** |
| OCL guaranteed at | 25°C | Full temp range | **Full temp range** |
| Isolation voltage | 1500V AC | 2500V AC | 2500V AC min |
| Qualification | — | — | **AEC-Q200** |
| Vibration | — | IEC 60068-2-6 | AEC-Q200 Stress G (30G) |
| Temperature cycling | — | — | −55/+150°C, 1000 cycles |
| Lifetime | 5–10 yr | 10–15 yr | **15+ yr** |
| EMC standard | CISPR 22 | IEC 61000 | **CISPR 25** |

---

## AEC-Q200 Key Qualification Tests

| Test | Condition | Duration | Pass Criterion |
|------|-----------|----------|---------------|
| High temp storage | +150°C | 1000 hr | OCL within ±10%, no breakdown |
| Temp cycling | −55°C ↔ +150°C | 1000 cycles | No cracking, params in spec |
| Humidity | 85°C / 85% RH | 1000 hr | No insulation failure |
| Mechanical shock | 500G, 1ms | 6 axes | No damage |
| Vibration | 30G, 10–2000Hz | Per AEC-Q200 G | No resonance failure |
| Board flex | 2mm deflection | Per spec | No solder joint failure |
| SPC | Cpk ≥ 1.67 | Ongoing | OCL, DCR, isolation |

---

## Automotive PHY Chip Reference

| PHY Chip | Vendor | Standard | Application |
|----------|--------|---------|-------------|
| BCM89810 | Broadcom | 100BASE-T1 | Original BroadR-Reach |
| TJA1101 / TJA1102 | NXP | 100BASE-T1 | ADAS, body ECUs |
| DP83TC811 | TI | 100BASE-T1 | Automotive qualified |
| LAN8670 | Microchip | 100BASE-T1 + 10BASE-T1S | Multi-drop |
| 88Q2112 | Marvell | 1000BASE-T1 | ADAS / gateway |
| TJA1103 | NXP | 1000BASE-T1 | Automotive gateway |

---

## Application Selection Guide

| Application | Grade Required | Temperature | Key Standard |
|-------------|---------------|-------------|-------------|
| Production automotive ECU | AEC-Q200 | −40/+125°C | CISPR 25 |
| ADAS camera / radar ECU | AEC-Q200 | −40/+125°C | CISPR 25 |
| EV / HEV battery management | AEC-Q200 | −40/+125°C | ISO 7637 |
| **E-bike / micro-mobility** | **Industrial** | **−40/+85°C** | IEC 61000 |
| **Agricultural / marine** | **Industrial** | **−40/+85°C** | IEC 61000 |
| **Automotive aftermarket** | **Industrial** | **−40/+85°C** | IEC 61000 |
| **Industrial IoT / factory** | **Industrial** | **−40/+85°C** | IEC 61000 |

---

## ISO 7637-2 Automotive Transient vs Isolation Voltage
Automotive bus transients (12V system):
Load dump (pulse 5a): up to +87V
Jump start:           up to +24V
Battery disconnect:   up to +87V
Automotive bus transients (48V mild hybrid):
Load dump:            up to +200V
→ 2500V AC isolation provides adequate margin for all standard automotive transients
→ Isolation voltage is the first barrier protecting PHY from cable transients

---

## Supplier Reference

**For full automotive AEC-Q200 designs:**
Consult specialized automotive magnetic suppliers. Contact Voohu Technology for automotive-grade product roadmap.

**For industrial / automotive-adjacent applications (e-bike, agricultural, marine, aftermarket):**  
Voohu Technology — [www.voohuele.com](https://www.voohuele.com)  
Industrial-grade: −40/+85°C, 2500V AC isolation, SMD and THT packages, PoE-rated variants.  
MOQ: 50pcs | Delivery: DHL 3–5 days to Japan / Korea / SE Asia | BOM sourcing support.
