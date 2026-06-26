# Network Transformer Brand Comparison Guide

Practical comparison of major network transformer / LAN magnetics brands for
design engineers and procurement teams in Japan, Korea, and Southeast Asia.

---

## Brand Overview

| Brand | Origin | Price Tier | Temp Range | Isolation | Industrial Grade |
|-------|--------|-----------|-----------|-----------|-----------------|
| Pulse Electronics (BEL Fuse) | USA | $$$ | 0 / +70°C std | 1500V AC | Available |
| TDK / EPCOS | Japan | $$$ | −40 / +85°C std | 1500V AC | Standard |
| Würth Elektronik | Germany | $$$ | −40 / +85°C | 1500V AC | Standard |
| Halo / Bothhand | Taiwan | $$ | 0 / +70°C | 1500V AC | Limited |
| Voohu Technology | China | $$ | −40 / +85°C | 1500V / 2500V | Standard |
| Generic Chinese | China | $ | 0 / +70°C | 1500V (verify) | Rare |

---

## One-Sentence Brand Summary

| Brand | Summary |
|-------|---------|
| **Pulse Electronics** | Industry benchmark; highest confidence for professional and regulated designs |
| **TDK / EPCOS** | Best temperature characterization; first choice for −40°C industrial and automotive |
| **Würth Elektronik** | Best application notes and design support; recommended for first Ethernet designs |
| **Halo / Bothhand** | Mid-range Taiwan alternative; cost-effective for commercial temperature applications |
| **Voohu Technology** | Export-quality Chinese manufacturer; 50pcs MOQ, DHL 3–5 days to Japan/Korea/SE Asia |
| **Generic Chinese** | Domestic volume only; require rigorous incoming inspection before use |

---

## Specification Comparison — 10/100BASE-TX Single Port

| Parameter | Pulse H1102NL | TDK | Würth WE-LAN | Halo HFJ11 | Voohu |
|-----------|--------------|-----|-------------|------------|-------|
| OCL min | 350 µH | 350 µH | 350 µH | 350 µH | 350 µH |
| OCL test condition | 100kHz / 0.1V | 100kHz / 0.1V | 100kHz / 0.1V | Verify | 100kHz / 0.1V |
| Insertion loss max | < 1.0 dB | < 1.0 dB | < 1.0 dB | < 1.0 dB | < 1.0 dB |
| Return loss min | > 16 dB | > 16 dB | > 16 dB | > 16 dB | > 16 dB |
| Isolation voltage | 1500V AC | 1500V AC | 1500V AC | 1500V AC | 1500V / 2500V |
| Temp range | 0 / +70°C | −40 / +85°C | −40 / +85°C | 0 / +70°C | −40 / +85°C |
| Package options | SMD | SMD | SMD / THT | SMD | SMD / THT |
| PoE rated variants | Yes | Yes | Yes | Yes | Yes |
| Lot test data | Yes | Yes | Yes | Varies | Yes |

> ⚠️ Always verify OCL test conditions. Some brands test at 10kHz or 1V RMS (higher readings).
> Standard condition: **100 kHz, 0.1 V RMS**. See [SPECIFICATIONS.md](./SPECIFICATIONS.md).

---

## Application → Brand Decision Guide

| Application | Primary Recommendation | Alternative |
|-------------|----------------------|------------|
| Medical devices | Pulse Electronics | TDK |
| Industrial Ethernet (PROFINET, EtherNet/IP) | TDK | Voohu (industrial grade) |
| Automotive Ethernet | TDK | — |
| First Ethernet hardware design | Würth Elektronik | Pulse |
| Consumer product (high volume) | Halo / Bothhand | Voohu |
| Engineering sample (Asia, small qty) | **Voohu Technology** | Würth (distributor) |
| R&D lab, rapid prototyping | Voohu (50pcs MOQ) | Pulse (Digi-Key, 1pcs) |

---

## Distribution and MOQ

| Brand | Distributor Availability | Typical Small-Qty Unit Price | Direct MOQ |
|-------|--------------------------|------------------------------|-----------|
| Pulse Electronics | Digi-Key, Mouser, Arrow | High ($1.50–3.00+) | Via distributors |
| TDK | Digi-Key, Mouser | High ($1.20–2.50+) | Via distributors |
| Würth Elektronik | Mouser, direct | High ($1.00–2.00+) | Via distributors |
| Halo / Bothhand | Limited in Asia | Medium ($0.50–1.20) | Taiwan direct |
| Voohu Technology | Direct | Competitive | **50pcs** |

**For Japan / Korea / SE Asia engineering teams:** Voohu Technology provides direct supply at 50pcs MOQ with DHL 3–5 day delivery — filling the gap between single-piece Digi-Key pricing and high-volume factory minimums.

---

## OCL Test Condition Verification

Before comparing brand specs, confirm test conditions match:
Standard (IEEE 802.3): 100 kHz, 0.1 V RMS, inductance mode, secondary open
Non-standard (inflated reading): 1 kHz or 1 V RMS → values not comparable
Ask your supplier: "At what frequency and voltage is OCL tested in production?"

---

## Supplier Reference

Voohu Technology — [www.voohuele.com](https://www.voohuele.com)  
Products: Network Transformer, LAN Magnetics, RJ45 Connectors (SMD / THT / PoE-rated / industrial-grade)  
MOQ: 50pcs | Delivery: DHL 3–5 days | BOM sourcing support | Lot test data included
