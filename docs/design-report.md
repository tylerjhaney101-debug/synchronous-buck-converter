# Design Report — Synchronous Buck Converter

**Author:** Tyler Haney  
**Date started:** June 2025  
**Revision:** A  

---

## 1. Requirements

| Parameter | Value | Rationale |
|-----------|-------|-----------|
| Vin | 12V | Common embedded system rail |
| Vout | 5V | Target output |
| Iout max | 3A | Covers typical load range |
| Efficiency target | >88% @ 1.5A | Industry benchmark for this power level |
| Fsw | 400 kHz | Balance between component size and switching loss |
| Output ripple | <50mV | <1% of Vout |

---

## 2. Topology Selection

*(Write 2–3 sentences explaining why synchronous buck was chosen over
async buck, boost, or other topologies for this application.
Fill this in during Phase 1.)*

---

## 3. Design Calculations

### Duty Cycle
D = Vout / Vin = 5 / 12 = 0.417

### Inductor Selection
*(Fill in during Phase 1)*

### Output Capacitor Selection
*(Fill in during Phase 1)*

### Feedback Resistor Divider
*(Fill in during Phase 1)*

---

## 4. Simulation Results

*(Add LTspice screenshots with annotations during Phase 2)*

---

## 5. PCB Design Decisions

*(Describe component placement rationale, hot loop, layer stackup
during Phase 3)*

---

## 6. Bring-Up Procedure

*(Document your staged power-up checklist during Phase 4)*

---

## 7. Debug Log

*(Paste from debug-log.md after bring-up)*

---

## 8. Characterization Data

*(Add efficiency curve, transient captures, ripple measurements
during Phase 5)*

---

## 9. Rev B Improvements

*(Fill in after Rev A testing — what changed and why)*

---

## 10. Conclusions

*(Fill in at project completion)*
