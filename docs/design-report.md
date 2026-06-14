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
| L Ripple Ratio | 30% | Standard balance for core size vs AC core |
| Operating Temp | -40°C to +85°C | Industrial grade boundary |

---

## 2. Topology Selection

*(Write 2–3 sentences explaining why synchronous buck was chosen over
async buck, boost, or other topologies for this application.
Fill this in during Phase 1.)*

---

## 3. Design Calculations

### Duty Cycle

Dideal = Vout / Vin = 5 / 12 = 0.4167

Dideal = 41.67 %

Loss-Corrected Duty Cycle (Assuming n = 0.90) : D = Vout / (Vin * n) 

Min Input (7V): Dmax = 5.0 / (7.0 * 0.90) * 100 = 79.37 %

Nomial Input (12V): Dnom = 5.0 / (12.0 * 0.90) * 100 = 46.30 %

Maximum Input (18V): Dmin = 5.0 / (18.0 * 0.90) * 100 = 30.86 %

### Inductor Selection
Target Ripple Current (r = 0.30 & Iout = 3 A) : ILf - ILi = r * Iout(max) = 0.30 * 3.0 A = 0.9 A

L = ((Vin(nom) - Vout) * Dideal) / (f * (ILf- ILi))

L = ((12.0 - 5.0) * 0.4167) / (400000 * 0.90) = 2.9169 / 360000 = 8.10 * 10^-6 H

Not a common manufactured component value: Pick between 6.8 microH or 10 microH 

Worst-Case Inductor Currents: deltaI(Lmax) = ((Vin(max) - Vout) * (Vout / Vin(max))) / (f * L) 

deltaI(Lmax) = ((18.0 - 5.0) * 0.2778) / (400000 * (6.8 * 10^-6)) = 3.611 / 2.72 = 1.328 A

Max Current Ripple = 1.328 A 

Peak Current: Ipeak = Iout(max) + (deltaI(Lmax) / 2) = 3.0 + 1.328 / 2 = 3.664 A

RMS Current: Irms = ((I^2out(max) + (deltaI^2(Lmax) / 12))^0.5 = (3.0^2 + (1.328^2 / 12))^0.5 = 3.024 A

### Output Capacitor Selection

Cout(min) = deltaI(Lmax) / (8 * f * deltaVout)

Cout(min) = 1.328 / (8 * 400000 * 0.050) = 1.328 / 160000 

Cout(min) = 8.3 * 10^-6 F

### Feedback Resistor Divider
*(Fill in during Phase 1)*

---

## 4. Simulation Results

<img width="1182" height="656" alt="image" src="https://github.com/user-attachments/assets/eeba40b7-eca0-4495-9cbf-8682892d1928" />

Behavioral Simulation of 12V-5V buck conveter with LT8610A

<img width="599" height="525" alt="image" src="https://github.com/user-attachments/assets/4aace38f-7b19-4ce2-bc4d-7a26b5d53427" />

Schematic of 12V-5V buck conveter with LT8610A




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
