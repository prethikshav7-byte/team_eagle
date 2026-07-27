# Soil Moisture Sensor

Measures the water content in soil. Commonly used in:
- Automated plant-watering systems
- Smart agriculture / irrigation control
- Environmental monitoring

## Wiring / Pinout
Typical analog soil moisture sensor module:

| Pin | Connect To |
|-----|------------|
| VCC | 5V |
| GND | GND |
| A0  | Analog pin (e.g., A0) |

## Arduino Code Example
```cpp
#define SOIL_PIN A0

void setup() {
  Serial.begin(9600);
}

void loop() {
  int moistureValue = analogRead(SOIL_PIN);
  Serial.print("Soil Moisture Value: ");
  Serial.println(moistureValue); // Lower value = wetter soil (varies by module)
  delay(500);
}
```
