## SCHEMATIC 4: LDR (Light Dependent Resistor) - Voltage Divider

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
             |      |  Pin A0------------+
             |      |                   |
             |      +-------------------+
             |              |
             |              |
             |      +-------+-------+
             |      |                 |
             |      |     5V          |
             |      |     |           |
             |      |     |           |
             |      |   [LDR]         |
             |      |     |           |
             |      |     +-----> Pin A0
             |      |     |           |
             |      |   [10kΩ]        |
             |      |     |           |
             |      |    GND          |
             |      |                 |
             |      |   LDR CIRCUIT   |
             |      |  (VOLTAGE DIVIDER)
             |      +-----------------+
             |              |
             +------+-------+
                    |
                    |
                   GND
```

### Wiring Table

| **Component** | **Connection** | **Note** |
| :--- | :--- | :--- |
| **LDR** (One leg) | Arduino **5V** | - |
| **LDR** (Other leg) | Arduino **A0** AND 10kΩ to GND | Forms voltage divider |
| **10kΩ Resistor** | Between A0 and GND | Fixed resistor |

### Physical Circuit Layout

```
         +-----[ 5V ]-----+
         |                 |
         |                +++
         |                |L|  ← Light Dependent Resistor
         |                |D|     (Resistance decreases in light)
         |                |R|
         |                +++
         |                 |
         +-----[ A0 ]-----+  ← Analog reading (0-1023)
         |                 |
         |                +++
         |                | |  ← 10kΩ Fixed Resistor
         |                | |
         |                +++
         |                 |
         +-----[ GND ]----+
```

### Critical Callouts

```
┌─────────────────────────────────────────────┐
│ ⚠️ LDR CHARACTERISTICS:                    │
│ - Resistance DARK: ~1MΩ (very high)        │
│ - Resistance LIGHT: ~1kΩ (very low)        │
│ - Non-linear response                      │
├─────────────────────────────────────────────┤
│ ⚠️ ANALOG READING:                         │
│ - Dark:  Reading near 0                    │
│ - Light: Reading near 1023                │
│ - Formula: Voltage = (R_fixed)/(R_ldr+    │
│              R_fixed) × 5V                 │
└─────────────────────────────────────────────┘
```

