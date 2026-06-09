# Synchronous Buck Converter — 12V to 5V / 3A

Custom 4-layer PCB power converter designed and characterized from scratch.
Achieved [X]% peak efficiency. Validated with oscilloscope, load transient
testing, and full efficiency sweep.

![PCB photo](media/photos/rev-a-board.jpg)

## Specifications

| Parameter | Target | Measured |
|-----------|--------|----------|
| Input voltage | 12V | — |
| Output voltage | 5V | — |
| Max output current | 3A | — |
| Peak efficiency | >88% | — |
| Switching frequency | 400 kHz | — |
| Output ripple | <50mV | — |

## Key Results
- Peak efficiency: [X]% at [X]A load (fill in after testing)
- Output ripple: [X]mV peak-to-peak at 1.5A
- Load transient: [X]mV droop, [X]µs recovery

## Project Structure
- `/docs` — design report, calculations, thermal analysis
- `/hardware` — schematic, PCB files, Gerbers, BOM
- `/simulation` — LTspice files
- `/validation` — test data, oscilloscope captures
- `/media` — photos, renders

## Tools Used
Altium Designer · LTspice · Python · STM32 · Git

## Design Report
[View full design report](docs/design-report.md)
