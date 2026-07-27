## SCHEMATIC 2: Ultrasonic Sensor (HC-SR04)

### Circuit Diagram

```
                    +-------------------+
                    |    ARDUINO UNO    |
                    |                   |
                    |   +-----------+   |
                    |   |           |   |
                    |   |  +-----+  |   |
                    |   |  |     |  |   |
                    |   +--+     +--+   |
                    |      |     |      |
             +------+      |     |      |
             |      |      |     |      |
             |      |  5V--+     |      |
             |      |  GND-------+      |
             |      |  Pin 9-------------+    (TRIG)
             |      |  Pin 10------------+    (ECHO)
             |      |                   |
             |      +-------------------+
             |              |
             |              |
             |      +-------+-------+
             |      |   HC-SR04     |
             |      |  ULTRASONIC   |
             |      |    SENSOR     |
             |      |               |
             |      |  +---------+  |
             |      |  |  EYES   |  |
             |      |  |   ██    |  |
             |      |  |   ██    |  |
             |      |  +---------+  |
             |      |               |
             |      |  VCC  5V      |
             |      |  GND  GND     |
             |      |  TRIG Pin 9   |
             |      |  ECHO Pin 10  |
             |      +---------------+
             |              |
             +------+-------+
                    |
                    |
                   GND
```

### Wiring Table

| **HC-SR04 Pin** | **Connection** | **Note** |
| :--- | :--- | :--- |
| **VCC** | Arduino **5V** | - |
| **GND** | Arduino **GND** | - |
| **TRIG** | Arduino **Pin 9** | Output pin (sends ping) |
| **ECHO** | Arduino **Pin 10** | Input pin (listens for return) |

### Critical Callouts

```
┌─────────────────────────────────────────────┐
│ ⚠️ TIMING CONSTRAINT:                      │
│ - TRIG pulse: 10µs HIGH                    │
│ - ECHO duration: measures distance         │
│ - Formula: distance = duration*0.034/2 cm │
├─────────────────────────────────────────────┤
│ ⚠️ VOLTAGE WARNING:                        │
│ - ECHO outputs 5V (Safe for Arduino 5V)    │
│ - For 3.3V boards (ESP32): Use voltage     │
│   divider (2x resistors) on ECHO pin      │
└─────────────────────────────────────────────┘
```
