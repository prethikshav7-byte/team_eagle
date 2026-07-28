---
name: sound_sensor
description: Guidelines for using a sound sensor / microphone module (analog + digital output)
---

# Sound Sensor (Microphone Module)

## Component Notes
- Most breakout boards (e.g. KY-038) use an **LM393 dual comparator** IC to do two jobs at once: one half amplifies the raw microphone signal for AO, the other half compares the amplified signal against a threshold (set by the onboard pot) to produce DO.
- The electret microphone itself just converts sound pressure into a tiny voltage — all the amplification and thresholding happens on the LM393.

## Pin Connections
- VCC → 3.3V or 5V (check the module's label — most support either)
- GND → Ground
- AO (Analog Out) → Analog input pin (e.g., A0) — raw sound intensity level
- DO (Digital Out) → Digital GPIO pin — pulses HIGH/LOW when sound crosses a threshold

## Wiring Table
| Sensor Pin | Connection | What the signal does |
|---|---|---|
| VCC | Arduino 5V | Powers the module |
| GND | Arduino GND | Common ground reference |
| AO | Arduino A0 | Continuous sound level, 0-1023 |
| DO | Arduino D2 | HIGH pulse when the threshold is crossed |

## Signal Flow
1. **Power up** — VCC/GND bring the module online
2. **Tune** — adjust the onboard potentiometer to set the DO threshold for your environment
3. **Read** — poll A0 for level, or watch D2 for a trigger (debounce ~200-300ms per event)

## Timing & Sensitivity Constraints (CRITICAL)
- The onboard potentiometer sets the DO threshold. Too sensitive → constant false triggers. Too low → missed claps. Tune it to your environment's noise floor.
- AO readings fluctuate rapidly sample-to-sample; average several `analogRead()` calls if you need a stable sound-level reading.
- DO outputs a short pulse per loud event — without debouncing, a single clap can register as multiple triggers.

## Protocol Sequence
1. Power the module (VCC/GND)
2. For simple trigger detection: `digitalRead(DO_PIN)` — HIGH/LOW indicates the threshold was crossed
3. For level sensing: `analogRead(AO_PIN)` — returns 0-1023 proportional to sound amplitude
4. If detecting discrete claps, add a debounce window (roughly 200-300ms) after each trigger before accepting the next one

## Common Failure Modes
- **Failure:** DO never triggers, or triggers constantly on background noise.
  **Fix:** Adjust the onboard potentiometer — it sets the reference voltage on the LM393 comparator's threshold input.
- **Failure:** AO readings jump around unpredictably.
  **Fix:** Average multiple `analogRead()` samples, or add a small delay between reads.
- **Failure:** One clap registers as two or three triggers.
  **Fix:** Add a debounce delay in code after each DO trigger.

## Platform-Specific Notes
- **Arduino:** `analogRead()` for AO, `digitalRead()` for DO; no pull-up needed on either pin.
- **ESP-IDF:** Use the ADC driver for AO (confirm the pin supports ADC input); standard GPIO input for DO.
- **Zephyr:** Use the ADC API for AO; the GPIO driver with an interrupt callback works well for DO edge detection.
