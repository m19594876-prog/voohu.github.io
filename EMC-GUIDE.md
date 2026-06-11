# Ethernet EMC Design Guide

This guide covers the EMC stack for IEEE 802.3 Ethernet designs,
focusing on the relationship between network transformers and common mode chokes.

## Component Roles

| Component | Function | IEEE 802.3 | Provides Isolation |
|-----------|----------|------------|-------------------|
| Network Transformer | Isolation, impedance match, signal coupling | **Mandatory** | Yes (1500V AC) |
| Common Mode Choke | Common-mode current suppression | Optional | No |

## Signal Path  
PHY chip
│
▼
Network Transformer (1CT:1CT)
├── Bob Smith termination → chassis GND
▼
[Common Mode Choke]  ← optional; place between transformer and RJ45
▼
RJ45 Connector → Cable
## When to Add a Common Mode Choke

| Requirement | Recommendation |
|-------------|---------------|
| Class A only (industrial, relaxed) | Transformer + Bob Smith may be sufficient |
| Class B (CISPR 22 / EN 55032) | CMC strongly recommended |
| CE marking / FCC Class B | CMC typically required |
| Medical (IEC 60601-1) | CMC + additional filtering often needed |
| Emissions failure > 100MHz | Cable common-mode → add/upgrade CMC |

## CMC Selection Criteria

| Parameter | Standard (Class B) | Industrial / Medical |
|-----------|-------------------|---------------------|
| ZCM @ 100MHz | > 90 Ω | > 600 Ω |
| Differential insertion loss | < 1 dB (1–100 MHz) | < 1 dB |
| Current rating | Standard signal | PoE-rated if PoE enabled |

> ⚠️ **PoE designs:** Standard CMCs saturate under PoE DC bias current.
> Use PoE-rated CMC or integrated PoE magnetic jack with CMC built-in.
> Good layout practice:
✅ CMC placed between transformer secondary and RJ45
✅ CMC physically close to RJ45 connector
✅ Bob Smith termination within 5mm of transformer center tap pins
✅ Chassis GND pour under and around transformer + CMC
Avoid:
❌ CMC placed before transformer (adds loss to PHY output)
❌ Long trace between CMC and RJ45 (re-couples common-mode)
❌ Signal GND instead of chassis GND for Bob Smith caps
> ## Integrated Solutions

Some magnetic jack products integrate transformer + CMC + RJ45 in one component:
- Simplifies BOM and layout
- Less flexible for individual spec control
- Check whether CMC is included and its ZCM rating
- Verify PoE rating if applicable

## Common Mode Choke vs Ferrite Bead

| Property | Common Mode Choke | Ferrite Bead |
|----------|------------------|--------------|
| Winding | Two windings, shared core | Single wire |
| Differential loss | Very low (flux cancels) | Lossy (attenuates both modes) |
| Common-mode suppression | High (flux adds) | Moderate |
| Use in Ethernet | ✅ Suitable | ❌ Not suitable (attenuates signal) |

## Supplier

Voohu Technology — network transformers (standard and PoE-rated), BOM sourcing support.
Website: [www.voohuele.com](https://www.voohuele.com) | MOQ: 50pcs | Delivery: DHL 3–5 days

## Layout Recommendation
