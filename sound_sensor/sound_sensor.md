---
name: sound_sensor
description: Guidelines for using the sound sensor (microphone module) for sound intensity measurement and clap/sound‑activated projects.
---

# Sound Sensor (Microphone Module)

## Pin Connections
- VCC → 3.3V or 5V (check your module's tolerance – most are 3.3V–5V compatible)
- GND → Ground
- AO → Analog input pin (e.g., A0) – outputs a voltage proportional to sound intensity (0 to VCC)
- DO → Digital input pin (e.g., D3) – outputs HIGH when sound exceeds the set threshold

## Threshold Adjustment (CRITICAL)
- The onboard **blue potentiometer** sets the reference voltage for the comparator.
- Turn it **slowly** with a small screwdriver:
  - **Clockwise** → less sensitive (only loud sounds trigger DO)
  - **Counter‑clockwise** → more sensitive (quiet sounds trigger DO)
- Use the onboard LED (usually tied to DO) to visually tune the sensitivity without writing code.

## Two Output Modes – Usage Guide
- **Analog Output (AO):** Connect to an ADC pin. Use `analogRead()` to get a continuous loudness value (e.g., 0–1023 on Arduino). Perfect for sound level meters, FFT analysis, or volume‑based effects.
- **Digital Output (DO):** Connect to a GPIO pin. Use `digitalRead()` to get a simple HIGH/LOW trigger. Perfect for clap‑activated switches, voice‑controlled relays, or wake‑on‑sound systems.

## Reading Sequence
1. **For Analog:** Call `analogRead(AO_pin)` repeatedly. Apply a moving average (e.g., 5–10 samples) to smooth out noise.
2. **For Digital:** Call `digitalRead(DO_pin)`. It returns `HIGH` (sound detected) or `LOW` (quiet). Add a debounce delay (50–100 ms) to avoid multiple triggers from a single clap.
3. Both outputs can be used **simultaneously** – the module outputs both AO and DO at the same time.

## Noise Reduction (CRITICAL for AO)
- The analog output can be noisy due to ambient electrical interference.
- **Hardware fix:** Place a **0.1 µF ceramic capacitor** between AO and GND near the MCU side.
- **Software fix:** Average multiple readings in code, or implement a simple low‑pass filter:
  `filtered = (filtered * 0.7) + (new_reading * 0.3);`

## Common Failure Modes
- **Failure:** DO is always HIGH or always LOW regardless of sound.
  **Fix:** Adjust the onboard potentiometer until the LED flickers when you clap. If it never triggers, the threshold is too high – turn counter‑clockwise.
- **Failure:** AO reading is stuck at 0 or maximum (1023).
  **Fix:** Check VCC and GND connections. Ensure the microphone is not covered and is facing the sound source.
- **Failure:** AO fluctuates wildly even in a silent room.
  **Fix:** Add the 0.1 µF capacitor as described above. Alternatively, increase your moving average window in software.
- **Failure:** DO triggers multiple times for a single clap.
  **Fix:** Implement a simple debounce: ignore any new DO triggers for **100 ms** after the first detection.

## Platform‑Specific Notes
- **Arduino (Uno/Nano):** Use `analogRead(A0)` for AO and `digitalRead(D3)` for DO. The onboard LED on the module serves as a handy visual indicator for the digital state.
- **ESP32 (3.3V logic):** The AO output ranges from 0 to 3.3V. Use `analogRead()` but note that ESP32 ADC has non‑linearity – calibrate if measuring absolute decibels. DO outputs 3.3V – safe for GPIO.
- **Raspberry Pi (no ADC):** The Pi does not have built‑in analog inputs. For AO, you **must** use an external ADC chip (e.g., MCP3008 or ADS1115). For DO, connect to any GPIO and use `gpiozero` or `RPi.GPIO` to detect claps.
- **STM32 (HAL):** Use the ADC in continuous conversion mode to sample AO at high speed (useful for audio spectrum analysis). Use EXTI interrupts on the DO pin for instantaneous trigger responses (e.g., wake‑on‑sound).