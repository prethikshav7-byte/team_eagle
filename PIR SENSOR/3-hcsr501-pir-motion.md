## SCHEMATIC 3: PIR Motion Sensor (HC-SR501)

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
             |      |  Pin 2-------------+
             |      |                   |
             |      +-------------------+
             |              |
             |              |
             |      +-------+-------+
             |      |   PIR MOTION  |
             |      |   SENSOR      |
             |      |   HC-SR501    |
             |      |               |
             |      |  +---------+  |
             |      |  |  FRESNEL|  |
             |      |  |  LENS   |  |
             |      |  |   ██    |  |
             |      |  +---------+  |
             |      |               |
             |      |  VCC  5V      |
             |      |  GND  GND     |
             |      |  OUT  Pin 2   |
             |      +---------------+
             |              |
             +------+-------+
                    |
                    |
                   GND
```

### Wiring Table

| **PIR Pin** | **Connection** | **Note** |
| :--- | :--- | :--- |
| **VCC** | Arduino **5V** | - |
| **GND** | Arduino **GND** | - |
| **OUT** | Arduino **Pin 2** | Digital input (HIGH = motion detected) |

### Critical Callouts

```
┌─────────────────────────────────────────────┐
│ ⚠️ ON-BOARD CONTROLS:                      │
│ - Time adjust: Sets output duration        │
│ - Sensitivity adjust: Sets detection range │
├─────────────────────────────────────────────┤
│ ⚠️ BEHAVIOR NOTE:                          │
│ - Output: HIGH (3.3V/5V) when motion      │
│ - Output: LOW when no motion              │
│ - Warm-up time: 10-60 seconds on power-up │
└─────────────────────────────────────────────┘
```

