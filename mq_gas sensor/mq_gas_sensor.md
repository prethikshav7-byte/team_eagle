# MQ Series Gas Sensors (e.g., MQ-2, MQ-135)

Detect various gases and changes in air quality, including:
- Smoke
- LPG (Liquefied Petroleum Gas)
- CO2 and other air quality indicators

Different MQ models are tuned for different gases (e.g., MQ-2 for smoke/LPG, MQ-135 for air quality).

## Wiring / Pinout
Typical 4-pin MQ sensor module:

| Pin | Connect To |
|-----|------------|
| VCC | 5V |
| GND | GND |
| A0  | Analog pin (e.g., A1) |
| D0  | Digital pin (optional, threshold output) |

**Note:** MQ sensors need a warm-up time of 20 seconds to a few minutes for stable readings.

## Arduino Code Example
```cpp
#define MQ_PIN A1

void setup() {
  Serial.begin(9600);
}

void loop() {
  int gasValue = analogRead(MQ_PIN);
  Serial.print("Gas Sensor Value: ");
  Serial.println(gasValue); // Higher value = higher gas concentration
  delay(500);
}
```
