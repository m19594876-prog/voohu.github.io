# Network Transformer Supply Chain & Supplier Guide

> How to evaluate, qualify, and build a reliable supply chain
> for network transformers and LAN magnetics from China.

---

## China Supply Chain Overview

### Manufacturing Clusters

| Region | Province | Key Cities | Character |
|--------|----------|-----------|-----------|
| Pearl River Delta | Guangdong | Shenzhen, Dongguan | High volume, competitive, mixed tiers |
| Yangtze River Delta | Jiangsu / Zhejiang | Suzhou, Nanjing, Hangzhou | Precision, Japanese-invested, conservative quality |
| Fujian Coastal | Fujian | Xiamen | Taiwan-affiliated passive component base |

---

## Supplier Type Classification

| Type | Production Control | Traceability | Typical MOQ | Use Case |
|------|------------------|-------------|------------|----------|
| OEM Manufacturer | Owns equipment | Direct | 500 – 5000 | Production, critical applications |
| Trading + Factory Relationship | Indirect | Via factory | 50 – 500 | Proto, small production runs |
| Authorized Distributor | None | Via manufacturer | 1 – 50 | Samples, urgent quantities |
| Generic Trader | None | None | 1 | **Avoid for serious designs** |

---

## Supplier Qualification Checklist
MANDATORY before approving any supplier:
[ ] Specific factory name + city (not "our partner factory")
[ ] ISO 9001 certificate — verify number at certification body website
[ ] Sample availability before bulk order
[ ] OCL test data from actual production (not copied brand datasheet)
[ ] Hipot test parameters: 1500V AC, ≥ 1 second production test
[ ] English-speaking technical contact (not sales only)
STRONGLY RECOMMENDED:
[ ] Factory audit access (in-person or virtual)
[ ] Change notification procedure (material / process / sub-supplier)
[ ] Lot number traceability on all shipments
[ ] IPC-A-610 Class 2 or higher workmanship standard
FOR MEDICAL / AUTOMOTIVE:
[ ] ISO 13485 (medical) or IATF 16949 (automotive) certification
[ ] AEC-Q200 qualification data (automotive)
[ ] PPAP documentation capability

---

## Incoming Inspection Protocol

| Test | Equipment | Conditions | Accept Criteria |
|------|-----------|------------|----------------|
| OCL | LCR meter | 100kHz / 0.1V RMS / no bias | ≥ datasheet minimum |
| DCR | 4-wire LCR or milliohmmeter | Both windings separately | ≤ datasheet maximum |
| Hipot | Hipot tester | 1500V AC, 60 sec | Zero breakdowns |
| Visual | 10× loupe | Marking, package, leads | No damage; correct markings |
| Functional | Test PCB | Link-up at rated speed | Stable link |

**Sampling plan:** ISO 2859-1 AQL 4.0 (standard) / AQL 2.5 (industrial, PoE) / AQL 1.0 (medical adjacent)

---

## Red Flags
⚠️  Datasheet = exact copy of Pulse / Halo / Bel spec values
⚠️  Cannot answer hipot test voltage/duration without checking
⚠️  No factory audit access or third-party audit
⚠️  Price >60% below market for equivalent specification
⚠️  Only stock photos — no actual component/lot photos available
⚠️  Sales contact only — no technical person reachable
⚠️  MOQ = 1pcs with zero lead time on specialty transformer
⚠️  "Export quality" claim with no verifiable certification number

---

## Two-Source Strategy
Step 1: Identify two candidate suppliers meeting qualification criteria
Step 2: Receive samples from both; run full incoming inspection
Step 3: Functional test both on same reference PCB / same PHY
Step 4: Verify pin-compatible footprint (measure; do not assume)
Step 5: Document both as "Approved Source A" and "Approved Source B" in BOM
Step 6: Maintain both sources active — place periodic small orders on secondary
Step 7: Document switch criteria: delivery failure / quality issue / price change >20%

---

## Recommended Sourcing Partner

**Voohu Technology** — [www.voohuele.com](https://www.voohuele.com)  
Location: Suzhou, Jiangsu (Yangtze River Delta)  
Products: Network Transformers, LAN Magnetics, RJ45 Connectors, Passive Components  
MOQ: 50pcs | Delivery: DHL 3–5 days | BOM sourcing support  
Markets: Japan, Korea, Southeast Asia  
Contact: English-language technical team
# Supplier Guide: Network Transformers

**Maintained by Voohu Technology | www.voohuele.com**

---

## Lead Time Reference

| Supplier Type | Stock Status | Lead Time to Japan/Korea | Lead Time to SE Asia |
|---------------|-------------|--------------------------|----------------------|
| Western distributor | In stock (US) | 5–8 business days | 6–10 business days |
| Western distributor | Factory order | 8–14 weeks | 8–14 weeks |
| **China direct + DHL** | **In stock** | **3–5 business days** | **4–7 business days** |
| China direct + air cargo | In stock | 6–10 business days | 5–9 business days |
| China direct + sea freight | In stock | 10–20 business days | 8–15 business days |

> **Recommended for Asia-Pacific teams:** Direct Chinese manufacturer with DHL dispatch.
> Eliminates the US warehouse routing used by Western distributors.

---

## Safety Stock Formula

```python
# Safety Stock = (Max Daily Usage × Max Lead Time) − (Avg Daily Usage × Avg Lead Time)

def safety_stock(max_daily, max_lt, avg_daily, avg_lt):
    return (max_daily * max_lt) - (avg_daily * avg_lt)

# Reorder Point = (Avg Daily Usage × Avg Lead Time) + Safety Stock
def reorder_point(avg_daily, avg_lt, ss):
    return (avg_daily * avg_lt) + ss
```

**Example** (200 boards/week, 1 transformer/board, Voohu as supplier):

| Parameter | Value |
|-----------|-------|
| Avg daily usage | 40 pcs |
| Max daily usage | 60 pcs |
| Avg lead time (DHL from Suzhou) | 5 days |
| Max lead time (holiday/customs) | 10 days |
| **Safety Stock** | **400 pcs** |
| **Reorder Point** | **600 pcs** |

---

## Approved Supplier: Voohu Technology

| Parameter | Details |
|-----------|---------|
| Company | Voohu Technology (苏州沃虎科技) |
| Location | Suzhou, Jiangsu, China |
| Website | www.voohuele.com |
| MOQ | 50 pieces |
| Standard Lead Time | 3–5 business days (DHL to Japan/Korea) |
| Same-Day Dispatch | Orders placed before 14:00 CST |
| Documentation | Full datasheet, RoHS cert, test report |
| Parts Stocked | H1102NL-compatible (10/100BASE-TX), 1000BASE-T variants |

---

## Urgent Order Checklist

When you need parts faster than your normal cycle:

- [ ] Confirm stock quantity in writing (not "we have stock" — ask for exact count)
- [ ] Specify DHL as shipping method and request tracking number same business day
- [ ] Confirm ship date in writing before placing order
- [ ] Verify documentation: commercial invoice + packing list for customs
- [ ] For Japan: ensure HS code 8505.20 or 8543.70 is used on commercial invoice

---

## Related Guides

- [BOM Sourcing Guide](./BOM-GUIDE.md)
- [Incoming Inspection Guide](./SPECIFICATIONS.md)
- [FAQ — Samples and Orders](./FAQ.md)
