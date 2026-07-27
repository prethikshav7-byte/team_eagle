# IR (Infrared) Sensor

Detects infrared light. Commonly used in:
- Line-following robots
- Object detection and obstacle avoidance
- Proximity sensing

## Wiring / Pinout
Most IR modules (e.g., generic 3-pin IR obstacle sensor) have 3 pins:

| Pin | Connect To |
|-----|------------|
| VCC | 5V |
| GND | GND |
| OUT | Digital pin (e.g., D2) |

## Arduino Code Example
```cpp
#define IR_PIN 2

void setup() {
  pinMode(IR_PIN, INPUT);
  Serial.begin(9600);
}

void loop() {
  int irValue = digitalRead(IR_PIN);
  if (irValue == LOW) { // LOW usually means object detected
    Serial.println("Object detected!");
  } else {
    Serial.println("No object detected.");
  }
  delay(200);
}
```
