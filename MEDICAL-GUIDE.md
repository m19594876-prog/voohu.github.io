# Network Transformer for Medical Devices

> IEC 60601-1 isolation requirements, MOPP levels, creepage tables,
> and documentation checklist for medical electrical equipment.

---

## Governing Standard

**IEC 60601-1:2005+AMD1:2012** — Medical Electrical Equipment, General Requirements  
US equivalent: UL 60601-1  
Quality system: ISO 13485:2016

---

## MOPP / MOOP Isolation Levels

| Protection Level | Test Voltage | Duration | Use Case |
|-----------------|-------------|----------|----------|
| 1 MOOP | 1500V AC rms | 60 sec | Operator ports, hospital IT |
| 1 MOPP | 1500V AC rms | 60 sec | Basic patient circuit isolation |
| **2 MOPP** | **4000V AC peak** | **60 sec** | Reinforced, BF/CF applied parts |
| 2 MOPP (DC) | 5656V DC | 60 sec | DC equivalent of 4000V AC peak |

**Standard IEEE 802.3 transformer hipot: 1500V AC — meets 1 MOOP / 1 MOPP only.**  
**For 2 MOPP, a medical-grade transformer is required.**

---

## Isolation Decision: Which Level Does Your Ethernet Port Need?
Ethernet port connects to hospital IT only, no patient circuit?
└─ 1 MOOP required → Standard 1500V transformer ✅
Patient circuit shares any electrical path with Ethernet interface?
└─ 2 MOPP required → 4000V medical transformer ⚠️
Applied part type CF (direct cardiac connection)?
└─ 2 MOPP, strictest requirements → consult safety certification body ⚠️
RULE: Draw isolation diagram before choosing components.

---

## Creepage and Clearance Requirements

**IEC 60601-1 Table 14 — 250V rms working voltage, Pollution Degree 2:**

| Insulation Class | Clearance | Creepage | Package Impact |
|-----------------|-----------|----------|---------------|
| Basic (1 MOPP) | 4.0 mm | 6.4 mm | Standard SMD packages OK |
| Reinforced (2 MOPP) | 8.0 mm | **12.8 mm** | Requires larger body — typically THT |

---

## Medical Component Documentation Checklist
Mandatory per ISO 13485 / FDA 21 CFR Part 820:
[ ] Full datasheet (all specs at rated conditions)
[ ] Declaration of Conformity (IEC/UL 60601-1)
[ ] Hipot test report at correct MOPP voltage (4000V AC / 5656V DC, 60 sec)
[ ] Creepage/clearance confirmation (IEC 60601-1 Table 14)
[ ] Lot number traceability (every shipment)
[ ] Change notification agreement with supplier
[ ] Supplier ISO 13485 or ISO 9001 certificate
[ ] IPC-A-610 Class 3 workmanship (production grade)

---

## Key Standards Reference

| Standard | Scope |
|----------|-------|
| IEC 60601-1:2005+AMD1:2012 | General safety and isolation |
| IEC 60601-1-2:2014 | EMC requirements |
| ISO 13485:2016 | Medical device quality management |
| IEEE 802.3 | Network transformer electrical specifications |
| IPC-A-610 Class 3 | Workmanship standard for medical/high-rel |

---

## Supplier Reference

Voohu Technology — [www.voohuele.com](https://www.voohuele.com)  
Network transformers and LAN magnetics for medical device R&D and production.  
Documentation package (datasheet + compliance declarations) available.  
MOQ: 50pcs | Delivery: DHL 3–5 days | Markets: Japan, Korea, SE Asia
