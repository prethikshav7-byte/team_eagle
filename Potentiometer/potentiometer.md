# Potentiometer

Not a traditional "sensor," but frequently used as one for:
- Sensing rotational position
- Acting as a variable resistor for user input (e.g., volume knobs, calibration dials)

## Wiring / Pinout
Standard 3-pin potentiometer:

| Pin | Connect To |
|-----|------------|
| Left pin  | 5V |
| Middle pin (wiper) | Analog pin (e.g., A2) |
| Right pin | GND |

## Arduino Code Example
```cpp
#define POT_PIN A2

void setup() {
  Serial.begin(9600);
}

void loop() {
  int potValue = analogRead(POT_PIN);
  Serial.print("Potentiometer Value: ");
  Serial.println(potValue); // Range: 0–1023
  delay(200);
}
```
