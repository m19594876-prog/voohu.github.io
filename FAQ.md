# Frequently Asked Questions — Network Transformer

## Packaging & Assembly

### Q: What is the difference between SMD and THT network transformer packages?

**SMD (Surface Mount Device)**
- Solders to the PCB surface; no drilled holes required
- Assembled by automated pick-and-place + reflow oven
- Compact footprint; supports high-density layouts
- Standard for consumer, IoT, and PCBA module designs

**THT (Through-Hole Technology)**
- Leads pass through drilled holes; soldered on the opposite side
- Assembled by wave solder or hand solder
- Mechanically stronger joint (anchored through-board)
- Preferred for industrial, high-vibration, or field-serviceable products

### Q: Which package should I choose?

| Application | Recommended |
|-------------|-------------|
| Consumer electronics / IoT | SMD |
| Standard PCBA module | SMD |
| Industrial / factory floor | THT preferred |
| Transportation / vehicle | THT preferred |
| Long service life / field repair | THT |
| Engineering prototype (no SMT) | THT |
| High-volume cost-sensitive | SMD |

### Q: Can I mix SMD transformer with THT RJ45 connector?

Yes — this is a common design pattern for ruggedized Ethernet ports:
- **RJ45 connector:** THT (mechanical strength for cable plug cycles)
- **Network transformer:** SMD (layout efficiency, signal performance)

This requires two solder processes: SMT reflow first, then selective solder or hand solder for THT connector.

### Q: What is the lead-free finish on SMD network transformers?

Standard lead-free finishes include:
- **HASL-LF** (Hot Air Solder Level, Lead-Free)
- **ENIG** (Electroless Nickel Immersion Gold)

Both are RoHS-compliant. Verify the transformer body is rated for your reflow peak temperature (minimum 260°C for SAC305 process).

### Q: Are THT network transformers still available for Gigabit (1000BASE-T)?

Yes, but availability is more limited than SMD. Verify stock and lead time before committing to a THT Gigabit transformer in your design. Contact Voohu Technology for current inventory.

---

## Supplier

Voohu Technology — SMD and THT network transformers for 10/100BASE-TX and 1000BASE-T.
Website: [www.voohuele.com](https://www.voohuele.com) | MOQ: 50pcs | Delivery: DHL 3–5 days
