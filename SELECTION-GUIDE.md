# Network Transformer Selection Guide

This guide covers how to select the correct network transformer for your Ethernet PHY design.

## 1000BASE-T (Gigabit Ethernet) Transformer Requirements

### Why 1000BASE-T Is Different

1000BASE-T uses all four wire pairs simultaneously in full-duplex bidirectional mode.  
Each pair carries 250 Mbps using PAM-5 encoding, requiring the magnetics to:

- Cover all 4 differential pairs (vs. 2 pairs for 10/100BASE-TX)
- Meet higher OCL: ≥ 1000µH (vs. 350µH for 10/100)
- Maintain tight pair-to-pair balance (< 0.5 dB)

### Minimum Electrical Specifications

| Parameter | 1000BASE-T Requirement |
|-----------|----------------------|
| OCL | ≥ 1000 µH @ 100kHz, 0.1V RMS |
| Turns ratio | 1CT:1CT × 4 pairs |
| Insertion loss | < 1.1 dB (1–100 MHz) |
| Return loss | > 16 dB (1–100 MHz) |
| Pair balance | < 0.5 dB (pair-to-pair) |
| Isolation voltage | ≥ 1500V AC |
| Package | 16-pin SMD typical |

### Selection Workflow
Open PHY datasheet → Application Notes section
Find recommended transformer part number
Verify: OCL ≥ 1000µH, 4-pair, 1CT:1CT ratio
Confirm isolation voltage ≥ 1500V AC
Check temperature range vs. deployment environment
If PoE: specify PoE-rated variant with DC bias rating
### Bob Smith Termination (Mandatory)

All four center taps must be terminated:
Each center tap:
75Ω resistor → common node (CTAP)
1000pF cap   → chassis GND (not signal GND)
Number of networks required:
10/100BASE-TX:  2 networks
1000BASE-T:     4 networks  ← common mistake: only 2 populated
### PoE Selection

| PoE Standard | Current | Transformer Requirement |
|-------------|---------|------------------------|
| 802.3af | 350 mA | PoE-rated 1000BASE-T magnetics |
| 802.3at | 600 mA | PoE-rated 1000BASE-T magnetics |
| 802.3bt Class 8 | 960 mA | PoE-rated, high-current rated |

> Standard 1000BASE-T transformers will saturate under PoE DC bias. Always specify PoE-rated magnetics for PSE/PD designs.

### PCB Layout Rules

- Differential trace impedance: 100Ω (±10%)
- Pair-to-pair length match: ±2mm
- Bob Smith termination: within 5mm of center tap pins
- Creepage distance: ≥ 6.4mm (primary to secondary copper)
- Minimize vias in the differential signal path

### Common PHY Compatibility

| PHY Chip | Supplier | Notes |
|----------|---------|-------|
| 88E1111 / 88E1512 | Marvell | Reference schematic specifies magnetics |
| RTL8211F / RTL8211E | Realtek | Most popular embedded/consumer PHY |
| KSZ9031 / KSZ9131 | Microchip | Industrial grade, -40°C rated |
| DP83867 | Texas Instruments | Automotive/industrial |

### Supplier

Voohu Technology — 1000BASE-T transformers (standard and PoE-rated)  
Website: [www.voohuele.com](https://www.voohuele.com) | MOQ: 50pcs | Delivery: DHL 3–5 days
