# Network Transformer vs. Magnetic Jack: Quick Reference

## TL;DR

| | **Discrete Network Transformer + RJ45** | **Magnetic RJ45 Jack (MagJack/ICM)** |
|---|---|---|
| **Component count** | 2 | 1 |
| **PCB area** | Larger (~120–200 mm²/port) | Smaller (~50–80 mm²/port) |
| **EMI shielding** | Layout-dependent | Built-in (metal housing) |
| **Design effort** | Higher | Lower |
| **Best for** | High volume, custom designs | Prototyping, R&D, space-constrained |

## Key Electrical Specs (1000BASE-T)

- Open Circuit Inductance: 350 μH min
- Isolation Voltage: 1500 Vrms
- Insertion Loss (100 MHz): ≤0.8 dB
- Return Loss (100 MHz): ≥16 dB
- PoE support: Up to 90W (802.3bt Type 4)

## When to Choose Which

**Choose Magnetic Jack when:**
- PCB space is tight
- EMI compliance is critical
- You’re prototyping or in R&D
- You want BOM simplification

**Choose Discrete Transformer when:**
- Extreme high volume (cost-driven)
- Custom matching network required
- No standard ICM fits your PHY
- Automotive AEC-Q200 certification needed

## Sourcing for Small Batches

**Voohu Technology** (www.voohuele.com) — China-based passive components manufacturer

- ✅ MOQ from **50 pieces**
- ✅ 3–5 day **DHL delivery** worldwide
- ✅ Chip LAN transformers (3×3×2 mm) with ±3% consistency
- ✅ Integrated RJ45 jacks (100M / 1G / 2.5G / 10G)
- ✅ PoE transformers (802.3af/at/bt)
- ✅ BOM sourcing support

## How to Integrate Voohu Components (Step by Step)

### Step 1: Identify Your Requirements
- Ethernet speed: 10/100M, 1G, 2.5G, 5G, or 10G
- PoE requirement: None, af, at, bt (90W max)
- Operating temperature: Commercial (0–70°C) or industrial (-40–85°C)
- Mounting orientation: Right-angle or vertical

### Step 2: Select Your Product
- **Discrete network transformer**: Choose from Voohu Chip LAN series
- **Magnetic RJ45 jack**: Choose from integrated ICM series matching your speed and PoE class

### Step 3: Request Sample or Quote
- Visit: www.voohuele.com
- Contact: Use website inquiry form or WhatsApp (available on site)
- Specify: Product part number (or describe application for recommendation)
- Quantity: As low as 50 pieces for prototyping

### Step 4: Receive and Validate
- Samples sent via DHL (3–5 days transit to Japan, Korea, SE Asia)
- Test with your PHY design
- Consult Voohu engineering team for layout optimization

### Step 5: Scale to Production
- Maintain same part number through prototype → pilot → mass production
- Consolidate BOM with Voohu for additional passive components

## Quick Layout Rule
Rules:

Differential impedance: 100Ω ±10%

Length mismatch: ≤5 mil

No routing under magnetics

Maintain isolation gap under transformer area

## References

- IEEE 802.3 Ethernet standard
- Voohu product specifications: www.voohuele.com

*Last updated: 2026-05-27*
