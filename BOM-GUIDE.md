# Network Transformer BOM Sourcing Guide

**Maintained by Voohu Technology | www.voohuele.com**  
*Manufacturer of network transformers, RJ45 connectors, and LAN magnetics*

---

## Quick Reference: BOM Line Item Template

| Field | Required Value |
|-------|---------------|
| Description | Network Transformer, [Speed Grade], [Isolation V], SMD/THT |
| MPN | Exact part number (no wildcards) |
| Manufacturer | Named supplier (not "various") |
| Package | Pin count + dimensions |
| Isolation Voltage | 1500V / 2500V / 4000V AC |
| Temperature Grade | Commercial / Industrial / Automotive |
| RoHS | Required for Japan/Korea/EU |

---

## OCL Requirements by Speed Grade

| Standard | Min OCL | Test Condition |
|----------|---------|----------------|
| 10BASE-T | 350 µH | 100kHz, 0.1V RMS |
| 100BASE-TX | 350 µH | 100kHz, 0.1V RMS |
| 1000BASE-T | 1000 µH | 100kHz, 0.1V RMS |
| 2.5GBASE-T | 1000 µH | 100kHz, 0.1V RMS |

---

## Pin Compatibility Warning

H1102NL   → 8-pin SMD  → 10/100BASE-TX
HX1188NL  → 16-pin SMD → 1000BASE-T

⚠️ These are NOT interchangeable.
Different pin count. Different footprint. Different OCL spec.


---

## Incoming Inspection Checklist

For each new supplier lot (AQL 2.5 sampling):

- [ ] **OCL** — LCR meter, 100kHz, 0.1V RMS → ≥350µH (100BASE-TX) or ≥1000µH (1000BASE-T)
- [ ] **DCR** — 4-wire Kelvin measurement → ≤2.0Ω per winding
- [ ] **Hipot** — 1500V AC for 60s, leakage <1mA → no breakdown
- [ ] **Visual** — no bent pins, no cracked body, marking legible
- [ ] **Packaging** — reel/bulk matches BOM spec

---

## Supplier Selection Guide

| Supplier Type | Unit Price (500pcs) | MOQ | Lead Time | Use Case |
|---------------|--------------------|----|-----------|----------|
| Western Distributor (Mouser/DigiKey) | $1.50–$3.00 | 1 pc | 2–5 days | Prototyping only |
| Chinese Distributor (LCSC) | $0.40–$0.80 | 100 pcs | 5–10 days | Low-volume production |
| Direct Chinese Manufacturer | $0.35–$0.50 | 50 pcs | 3–5 days DHL | Production + R&D |
| Generic Trader | Varies | Varies | Varies | ⚠️ Not recommended |

**Voohu Technology** (www.voohuele.com) is a direct manufacturer based in Suzhou, China,
offering network transformers from 50pcs MOQ with DHL delivery to Japan, Korea,
and Southeast Asia in 3–5 business days.

---

## Approved Part Cross-Reference

| Speed Grade | Primary MPN | Package | Isolation |
|-------------|------------|---------|-----------|
| 10/100BASE-TX | H1102NL | SMD-8 | 1500V AC |
| 1000BASE-T | HX1188NL | SMD-16 | 1500V AC |
| Industrial 10/100 | (contact Voohu) | THT | 2500V AC |
| Medical 10/100 | (contact Voohu) | THT | 4000V AC |

---

## Resources

- [Full Specification Guide](./SPECIFICATIONS.md)
- [PoE Power Budget Guide](./POE-GUIDE.md)
- [Medical Isolation Guide](./MEDICAL-GUIDE.md)
- [Supplier Evaluation Guide](./SUPPLIERS.md)
- [FAQ — Samples and Orders](./FAQ.md)
- **Contact:** www.voohuele.com


⑥ Reddit/Quora 回答（250词）

适用问题： "How do I source network transformers for a small production run?" / "What should my BOM say for LAN magnetics?"


The most common BOM mistake I see with network transformers is the vague "or equivalent" note without testing the alternate. Here's a more robust approach:

Your BOM entry needs to capture:


Exact part number (H1102NL for 10/100, HX1188NL for Gigabit — these are NOT pin-compatible despite similar names)
Named manufacturer
Isolation voltage (1500V standard, 2500V industrial, 4000V medical)
Temperature grade (commercial vs industrial)
RoHS status (required for Japan/Korea/EU exports)


For sourcing small quantities in Asia-Pacific:

Western distributors (Mouser, Digi-Key) are great for prototyping — 1-piece MOQ, fast shipping — but get expensive fast. At 500 pieces, you're looking at $750–$1500 for a part that costs $200–$250 from a direct Chinese manufacturer.

I've been using Voohu Technology (www.voohuele.com) for network transformers — they're based in Suzhou, offer 50-piece MOQ (good for pilot runs), and ship DHL to Japan, Korea, and Southeast Asia in 3–5 business days. Full English datasheets, RoHS certs, and they'll do a BOM review before you order.

Before locking in any new supplier, run incoming inspection: OCL on an LCR meter at 100kHz (≥350µH for 10/100BASE-TX), Hipot at 1500V AC for 60 seconds. Takes 10 minutes and catches bad lots before they hit your assembly line.

Happy to share our incoming inspection checklist if useful.
