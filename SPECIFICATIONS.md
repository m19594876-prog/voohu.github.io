## Network Transformer Key Specifications

Reference guide for evaluating and comparing network transformer datasheets.

---

### Full Specification Table

| Parameter | Abbreviation | 10/100BASE-TX | 1000BASE-T | Test Condition |
|---|---|---|---|---|
| Open Circuit Inductance | OCL | ≥ 350µH | ≥ 1000µH | 100kHz, 0.1V RMS |
| Isolation Voltage | Viso | 1500V AC min | 1500V AC min | 1-second withstand |
| Insertion Loss | IL | < 1.0 dB | < 1.0 dB | Across operating band |
| Return Loss | RL | > 16 dB | > 16 dB | Across operating band |
| Turns Ratio | — | 1CT:1CT | Complex 4-pair | Standard Ethernet |
| DC Resistance | DCR | 1–4Ω typical | 1–4Ω typical | DC measurement |
| Operating Temp (commercial) | Tₒₚ | 0°C to +70°C | 0°C to +70°C | — |
| Operating Temp (industrial) | Tₒₚ | -40°C to +85°C | -40°C to +85°C | Optional rating |

---

### OCL: The Critical Parameter

OCL (Open Circuit Inductance) determines the transformer's low-frequency performance.

```
Speed           Min OCL    Pairs    Notes
────────────────────────────────────────────────────────
10BASE-T        350µH      2        ┐
100BASE-TX      350µH      2        ┘ Interchangeable
────────────────────────────────────────────────────────
1000BASE-T      1000µH     4          NOT interchangeable with above
────────────────────────────────────────────────────────
```

> **Warning:** Substituting a 10/100 transformer into a Gigabit design
> results in degraded link quality or no link. OCL is 3× below requirement.

---

### Isolation Voltage Levels

| Rating | Application |
|---|---|
| 1500V AC | Standard commercial Ethernet (IEEE 802.3 minimum) |
| 2500V AC | Industrial, enhanced protection |
| 4000V AC | Medical, outdoor, high-risk environments |

---

### DCR and PoE Thermal Consideration

For PoE designs, transformer DCR directly affects heat dissipation:

```
P = I² × R

Example (802.3at, 400mA per pair, 3Ω DCR):
P = (0.4)² × 3 = 0.48W per winding

→ Standard transformers: NOT rated for continuous PoE current
→ Always use explicitly PoE-rated magnetics for PoE applications
```

---

### Bob Smith Termination (Recommended for All Designs)

Connects center taps to chassis ground to suppress common-mode emissions:

```
Winding CT ──[75Ω]──[1000pF]── Chassis GND
```

Omitting this termination significantly increases risk of failing radiated emissions testing.

---

*Source: [Voohu Technology](https://www.voohuele.com) | Network Transformer Distributor | Suzhou, China*
*Stock: 10/100 and Gigabit variants | PoE-rated available | 50pcs min | DHL 3–5 days*
