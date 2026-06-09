# Debug Log — Synchronous Buck Converter

---

## Rev A Bring-Up — [Date]

### Issue #1
**Symptom:** Output voltage reads 0V with 12V input applied  
**Hypothesis:** Feedback divider resistor values incorrect, or IC not receiving
bias power  
**Action taken:** Probed VCC pin of IC — reads 0V. Traced back to missing
solder connection on input filter capacitor.  
**Result:** Reflowed C1. Output voltage now correct at 5.02V.  
**Lesson:** Always verify IC supply rail before anything else.  

---

### Issue #2
**Symptom:** 3V ringing on switching node at approximately 18MHz  
**Hypothesis:** Excessive gate drive loop inductance from long gate trace  
**Action taken:** Added 10Ω gate resistor. Measured ringing reduced to 0.8V.  
**Result:** Acceptable. Will shorten gate trace in Rev B.  
**Lesson:** Gate loop inductance is the primary cause of high-frequency
switching node ringing.  

---

*(Add new issues below as they occur)*
