# Revision History — Synchronous Buck Converter

---

## Rev A — [Date ordered]
Initial design. Based on LTspice-validated schematic using MP2307.
4-layer PCB, first fabrication.

**Known issues going into Rev A:**
- Gate trace length longer than ideal (routing constraint)
- No snubber footprint included

---

## Rev A.1 — [Date]
Rework performed on populated Rev A board:
- Added 10Ω gate resistor (bodge wire) to reduce switching node ringing
- Result: ringing reduced from 3V to 0.8V amplitude

---

## Rev B — [Date ordered]
PCB revision based on Rev A findings:
- Shortened high-side gate trace from 8mm to 2mm
- Added RC snubber footprint across low-side FET (0Ω default)
- Moved input bulk capacitor 1.5mm closer to drain of high-side FET
- Added thermal vias under both MOSFETs (6 vias each)

**Expected improvements:**
- Reduced switching node ringing
- Lower thermal resistance for MOSFETs at full load

*(Fill in measured results after Rev B bring-up)*
