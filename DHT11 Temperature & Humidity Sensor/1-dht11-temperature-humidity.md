

## SCHEMATIC 1: DHT11 Temperature & Humidity Sensor

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
             |      |  Pin 7-------------+
             |      |                   |
             |      +-------------------+
             |              |
             |              |
             |      +-------+-------+
             |      |    DHT11      |
             |      |   SENSOR      |
             |      |               |
             |      |  +---------+  |
             |      |  |         |  |
             |      |  | +---+   |  |
             |      |  | |   |   |  |
             |      |  | +---+   |  |
             |      |  |         |  |
             |      |  +---------+  |
             |      |               |
             |      |  VCC  5V      |
             |      |  GND  GND     |
             |      |  DATA Pin 7   |
             |      +---------------+
             |              |
             |              |
             |        [10kΩ]
             |         PULL-UP
             |         RESISTOR
             |              |
             +------+-------+
                    |
                    |
                   GND
```

### Wiring Table

| **DHT11 Pin** | **Connection** | **Note** |
| :--- | :--- | :--- |
| **VCC** | Arduino **5V** | Can also use 3.3V on 3.3V boards |
| **GND** | Arduino **GND** | - |
| **DATA** | Arduino **Pin 7** | With **10kΩ pull-up** to 5V |

### Critical Callouts

```
┌─────────────────────────────────────────────┐
│ ⚠️ TIMING CONSTRAINT (CRITICAL)            │
│ - Minimum 1-second delay between readings  │
│ - Protocol: 18ms LOW start signal          │
│ - 40-bit data: 16-bit humidity + temp      │
│ - Checksum validation required             │
├─────────────────────────────────────────────┤
│ ⚠️ PLATFORM-SPECIFIC NOTES:                │
│ - Arduino:   INPUT_PULLUP                   │
│ - ESP-IDF:   GPIO_PULLUP_ONLY              │
│ - Zephyr:    Configure in devicetree       │
├─────────────────────────────────────────────┤
│ ⚠️ FAILURE MODES:                          │
│ - All zeros → Reading too fast             │
│ - No response → Missing pull-up resistor   │
└─────────────────────────────────────────────┘
```
