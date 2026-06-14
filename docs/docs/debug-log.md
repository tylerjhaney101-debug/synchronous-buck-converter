# Debug Log — Synchronous Buck Converter

---

## Rev A Phase 2 - LTspice Ideal Switch Simulation — [ 06 - 13 - 2026 ]

### Issue #1
**Symptom:** Simulation runs but waveform window is completely black
**Hypothesis:** No nodes probed — LTspice requires manual node selection
**Action taken:** Clicked VOUT wire on schematic to probe node
**Result:** Waveform appeared immediately
**Lesson:** LTspice does not auto-display waveforms — you must click 
each wire you want to measure

---

### Issue #2
**Symptom:** VOUT reads 0V to 6mV, decaying slowly to negative voltage
**Hypothesis:** Switch control sources not connected or not switching
**Action taken:** Verified PULSE syntax on V2 and V3, checked pin connections
**Result:** Identified V2/V3 had extra 0.417 ncycles parameter — removed
**Lesson:** PULSE syntax takes exactly 7 parameters. ncycles field 
should be left blank

---

### Issue #3
**Symptom:** Undefined model "sw" error on simulation run
**Hypothesis:** LTspice SW component requires an explicit .model directive
**Action taken:** Added .model SW SW(Ron=0.01 Roff=1Meg Vt=0.5 Vh=0) 
as SPICE directive on schematic
**Result:** Error resolved, simulation runs
**Lesson:** Voltage-controlled switch in LTspice is not self-contained — 
always requires a .model statement defining Ron, Roff, and threshold voltage

---

### Issue #4
**Symptom:** VOUT climbing in slow staircase pattern, reaching only 
~190mV at 100µs
**Hypothesis:** S2 (bottom switch) not conducting — inductor has no 
freewheel path
**Action taken:** Probed V(sw), V(vout), V(n002), V(n003) simultaneously
**Result:** VSW showed −350kV spikes — confirmed S2 output pins were 
floating with no GND return path
**Lesson:** When the inductor freewheel path is missing, energy has 
nowhere to go and generates massive voltage spikes. S2 must connect 
SW node to GND to give inductor current a return path

---

### Issue #5
**Symptom:** S2 pin connections repeatedly incorrect despite multiple 
rotation attempts
**Hypothesis:** SW component pin labeling in LTspice is ambiguous 
for beginners — pole/throw/control pins easily confused
**Action taken:** Replaced S2 and V3 entirely with 1N4148 freewheeling 
diode (non-synchronous topology) to establish working baseline
**Result:** Circuit operated correctly. VOUT ramped toward target. 
VSW switching confirmed at 400kHz
**Lesson:** Non-synchronous (diode) version is a valid debugging 
intermediate step. Diode self-commutates with no control signal needed, 
eliminating pin connection ambiguity

---

### Issue #6
**Symptom:** VOUT settling at 4.56V instead of 5.0V target
**Hypothesis:** 1N4148 forward voltage drop reducing output
**Action taken:** Measured VSW negative swing at −853mV confirming 
diode conduction. Recalculated duty cycle using:
VOUT = VIN × D − Vf × (1−D) → D = 0.449 → Ton = 1.12µs
**Result:** VOUT improved toward 5V
**Lesson:** Non-synchronous buck loses Vf (~0.44V) from output during 
freewheel phase. Duty cycle must be corrected to compensate. 
Synchronous switch eliminates this loss entirely

---

### Issue #7
**Symptom:** Output ripple measured at 120mV p-p, exceeding <50mV spec
**Hypothesis:** Insufficient output capacitance
**Action taken:** Increased C1 from 100µF to 470µF
**Result:** Ripple increased to 340mV — capacitor increase made it worse
**Root cause:** Ripple not capacitor-limited. Caused by open-loop 
operation with no feedback. Larger C changed LC resonant frequency 
and increased oscillation
**Lesson:** In an open-loop simulation without feedback, output ripple 
cannot be corrected by capacitor alone. A closed feedback loop is 
required to regulate VOUT against component drops and load variation

---

### Phase 2 Summary
**Non-synchronous simulation results (D=0.449, 1N4148):**
- VOUT steady state: 4.56V (target 5.0V — delta = diode Vf drop)
- Ripple: 120mV p-p (target <50mV — open loop limitation)
- VSW: −853mV to +12.0V (diode conduction signature confirmed)
- Switching frequency: 400kHz confirmed ✓
- Inductor current freewheeling: confirmed ✓

**Decision:** Revert C1 to 100µF. Proceed to synchronous switch 
implementation with MOSFET symbols (unambiguous pin labeling) and 
closed-loop feedback network.

---

*(Add new issues below as they occur)*
