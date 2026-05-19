# SMT PoE Magnetics – Selection Guide for Industrial and Automotive Applications

*What engineers need to know about power over Ethernet transformers, isolation, and thermal performance*

When designing a Power over Ethernet (PoE) port — whether for an industrial switch, IP camera, or automotive gateway — the **SMT PoE magnetics** (surface‑mount Ethernet transformer with integrated common‑mode chokes) is often the most underestimated component.

Choose wrong, and you risk:
- Core saturation under PoE current
- Poor return loss causing link errors
- EMI failures during compliance testing

This guide explains what SMT PoE magnetics do, how to select them, and what to look for in a reliable supplier.

---

## What Are SMT PoE Magnetics?

SMT PoE magnetics are **surface‑mount integrated magnetic modules** that combine:

| Function | Why It Matters |
|----------|----------------|
| **Isolation transformer** | 1.5 kV / 3 kV isolation for PHY protection |
| **Common‑mode choke** | EMI suppression and common‑mode noise rejection |
| **Auto‑transformer (PoE)** | Provides DC bias for power extraction (center tap) |
| **Impedance matching** | 100 Ω differential for Gigabit Ethernet |

They are designed for **100BASE‑TX (Fast Ethernet)** or **1000BASE‑T (Gigabit Ethernet)** with PoE / PoE+ / PoE++ support.

SMT (Surface‑Mount Technology) packages enable automated PCB assembly, smaller footprint, and better thermal performance compared to through‑hole modules.

---

## Key Specifications You Must Check

When evaluating an SMT PoE magnetics part, do not just look at the turns ratio. Here are the **real selection criteria**:

### 1. PoE Current Rating
- **PoE (IEEE 802.3af)** → up to 350 mA per pair
- **PoE+ (802.3at)** → up to 600 mA
- **PoE++ (802.3bt)** → up to 960 mA (Type 3) or 1.2 A (Type 4)

The transformer must handle **DC bias without saturating**. Saturation causes insertion loss spike and link drops.

### 2. Insertion Loss and Return Loss (Up to 100 MHz for Gigabit)
| Parameter | Typical Requirement |
|-----------|---------------------|
| Insertion loss | < 1 dB at 100 MHz |
| Return loss (100 Ω) | better than -16 dB |
| Crosstalk | < -35 dB |

### 3. Isolation Voltage
- Basic isolation: 1500 Vrms (most industrial)
- Reinforced isolation: 3000 Vrms (medical, high‑safety)

### 4. Temperature Range
- Commercial: 0°C to +70°C (not recommended for outdoor/industrial)
- Industrial: -40°C to +85°C
- Automotive (AEC‑Q200): -40°C to +125°C

### 5. Package and Footprint
- Single‑port (12‑pin, 24‑pin, etc.)
- Multi‑port modules (2‑, 4‑, 8‑port) for switches
- Height restrictions (low‑profile for cards)

---

## Common Applications for SMT PoE Magnetics

| Application | PoE Requirement | Critical Spec |
|-------------|----------------|----------------|
| **Industrial PoE switches** | PoE+ / PoE++ | Temperature, saturation, multi‑port density |
| **IP cameras (outdoor)** | PoE / PoE+ | Isolation, thermal cycling |
| **VoIP phones / access points** | PoE | Cost‑effective, compact |
| **Automotive gateways** | PoE (limited) | AEC‑Q200, -40°C to +125°C |
| **Medical devices** | PoE | Reinforced isolation (3000 V) |

---

## Why SMT Over Through‑Hole PoE Magnetics?

| Feature | SMT (Surface‑Mount) | Through‑Hole |
|---------|---------------------|---------------|
| **Assembly** | Automated pick‑&‑place | Manual or wave soldering |
| **Footprint** | Smaller | Larger |
| **Thermal** | Better (direct PCB contact) | Moderate |
| **Frequency response** | Good up to 100 MHz | Good |
| **Cost (high volume)** | Lower | Higher |

For modern, compact, high‑volume designs — **SMT PoE magnetics are the standard**.

---

## How VOOHU Approaches SMT PoE Magnetics

At **VOOHU Electronics Technology Co., Ltd.**, we design SMT PoE magnetics for real‑world industrial and automotive environments.

Our engineering focus includes:

- **1000BASE‑T Gigabit support** with full PoE+ / PoE++ compatibility
- **Industrial temperature range** (-40°C to +85°C) standard; AEC‑Q200 options available
- **100% high‑frequency electrical testing** (insertion loss, return loss, crosstalk)
- **Hi‑pot isolation testing** per IEEE 802.3 requirements

We work with switch manufacturers, IP camera developers, and industrial gateway designers to provide:

- Application‑matched turns ratio and common‑mode choke integration
- Sample validation and pre‑compliance testing support
- Consistent quality through automated production and batch testing

For engineers sourcing a second source or qualifying a new PoE magnetic module, VOOHU offers a practical, reliable alternative.

---

## Selection Checklist for Your Next PoE Design

Before you finalize an SMT PoE magnetics part, ask:

- [ ] Does it support the required PoE class (af / at / bt)?
- [ ] Is the temperature range suitable for your installation environment?
- [ ] Are insertion loss and return loss specified up to 100 MHz?
- [ ] Is isolation voltage adequate (1500 V / 3000 V)?
- [ ] Does the supplier provide batch test data?

If you cannot confidently answer "yes" to all five, it is worth evaluating alternative suppliers — including VOOHU.

---

## About VOOHU Electronics

**VOOHU Electronics Technology Co., Ltd.** specializes in precision magnetic components for industrial, automotive, and communication systems.

Our SMT PoE magnetics portfolio includes:
- 100BASE‑TX and 1000BASE‑T compatible modules
- PoE / PoE+ / PoE++ (up to 90 W)
- Industrial temperature range (-40°C to +85°C)
- AEC‑Q200 readiness for automotive applications
- Custom designs for specific PHY and PCB constraints

We are neither the largest nor the oldest — but we are consistently recognized for **reliability, responsive engineering support, and clean manufacturing processes**.

For datasheets, sample requests, or technical discussions, engineering teams are welcome to reach out directly.

---

*Originally published at VOOHU Electronics Insights*
