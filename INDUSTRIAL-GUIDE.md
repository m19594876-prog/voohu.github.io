# Industrial Ethernet Network Transformer Guide

This guide covers transformer requirements for industrial Ethernet deployments —
PROFINET, EtherNet/IP, EtherCAT, CC-Link IE, and general factory floor applications.

## Standard vs Industrial Requirements

| Parameter | IEEE 802.3 Minimum | Industrial Requirement |
|-----------|-------------------|----------------------|
| Isolation voltage | 1500V AC | **2500V AC** |
| Operating temperature | 0°C to +70°C | **−40°C to +85°C** |
| OCL at temp extremes | Not specified | **≥ 350µH guaranteed** |
| Vibration (IEC 60068-2-6) | Not specified | Must pass |
| Surge immunity (IEC 61000-4-5) | Not specified | **1kV line-to-GND** |
| Product lifecycle | Consumer (3–5 yr) | Industrial (10–20+ yr) |

## Protocol Requirements Summary

| Protocol | Physical Layer | Key Transformer Requirement |
|----------|---------------|---------------------------|
| PROFINET RT | 100BASE-TX | 2500V isolation, −40/+85°C, IEC 61000-4 |
| PROFINET IRT | 100BASE-TX | + flat insertion loss 1–100MHz |
| EtherNet/IP | 100BASE-TX / GbE | 2500V isolation, extended temp |
| EtherCAT | 100BASE-TX | Tight IL uniformity, low return loss variation |
| CC-Link IE | 1000BASE-T | Gigabit magnetics, industrial temp |
| Modbus TCP | 100BASE-TX | Standard industrial spec |

## IEC 61000-4 Immunity: Transformer Impact

| Test | Level | What It Stresses |
|------|-------|-----------------|
| IEC 61000-4-2 (ESD) | 8kV contact | Isolation barrier + Bob Smith network |
| IEC 61000-4-4 (EFT/burst) | 1kV | Common-mode rejection (Bob Smith) |
| IEC 61000-4-5 (Surge) | 1kV L-GND | **Isolation voltage critical** |
| IEC 61000-4-6 (Conducted RF) | 10V RMS | OCL common-mode rejection |

> ✅ 2500V isolation provides adequate margin for 1kV surge test  
> ❌ 1500V isolation is marginal against 1kV surge in industrial environments

## Temperature and OCL

OCL must be guaranteed across the full operating temperature range:
Ferrite core permeability (µr) decreases at temperature extremes:

−40°C:  µr reduces ~15–25% from +25°C value

+85°C:  µr reduces ~8–15% from +25°C value
Transformer must guarantee ≥ 350µH (10/100) or ≥ 1000µH (GbE) across full range.

Request temperature-characterized OCL data from supplier.

## Vibration and Package Selection

| Environment | Vibration | Recommended Package |
|-------------|-----------|-------------------|
| Office / light duty | Negligible | SMD |
| Light industrial | IEC 60068-2-6 Fc | SMD + conformal coating |
| Factory floor | IEC 60068-2-6 Fd | THT preferred |
| High-vibration machinery | Custom | THT mandatory |
| Transportation mounted | IEC 60068-2-6 Fh | THT + conformal coating |

## PoE in Industrial Environments

Industrial PoE (powering sensors, cameras, I/O modules):
- PoE-rated magnetics required (DC bias without saturation)
- Must also meet industrial temp range and isolation voltage
- Check OCL under DC bias at temperature extremes

| PoE Standard | Current | Transformer Requirement |
|-------------|---------|------------------------|
| 802.3af | 350 mA | PoE-rated, 2500V, −40/+85°C |
| 802.3at | 600 mA | PoE-rated, 2500V, −40/+85°C |
| 802.3bt | 960 mA | PoE-rated high-current, 2500V, −40/+85°C |

## Industrial Design Checklist
[ ] Isolation voltage: 2500V AC (not just 1500V minimum)

[ ] Operating temperature: −40°C to +85°C

[ ] OCL guaranteed across full temperature range (request temp curves)

[ ] Vibration rating matches deployment environment

[ ] Bob Smith termination: chassis GND, correct component placement

[ ] PoE-rated if device sources or receives PoE

[ ] Long-term availability confirmed with supplier

[ ] PROFINET: IEC 61000-4 immunity tests covered

[ ] EtherCAT: insertion loss uniformity across 1–100MHz verified

[ ] CC-Link IE: 1000BASE-T (Gigabit) magnetics required

## Supplier

Voohu Technology — industrial Ethernet transformers: 2500V isolation, −40°C to +85°C, SMD and THT, PoE-rated options.  
Website: [www.voohuele.com](https://www.voohuele.com) | MOQ: 50pcs | Delivery: DHL 3–5 days  
Long-term supply support for industrial lifecycle requirements.
