#  IoT Smart Watering System

A professional-grade IoT solution for automated plant care using the **ESP32-S3** microcontroller and **MQTT** protocol. This system allows for real-time monitoring and remote manual override via mobile applications.

## Key Features
- **Real-time Monitoring:** Continuous soil moisture data streaming to the cloud.
- **Dual-Mode Operation:**
    - **AUTO Mode:** Intelligent sensor-based watering logic.
    - **MANUAL Mode:** Remote pump control via MQTT commands, bypassing sensors.
- **MQTT Protocol:** Lightweight communication using EMQX/HiveMQ brokers for high reliability.
- **Instant Status Feedback:** Reports pump state (ON/OFF) and active mode back to the user interface.

## Hardware Components
| Component | Description |
| :--- | :--- |
| **ESP32-S3** | Main MCU with integrated Wi-Fi for cloud connectivity. |
| **Soil Moisture Sensor** | Analog sensor to detect water content in the soil. |
| **Relay Module** | Acts as a high-voltage switch for the water pump. |
| **Submersible Pump** | 5V/12V DC pump for water delivery. |
| **Power Supply** | 5V-2A DC adapter or Battery pack. |

## Wiring Diagram
- **Moisture Sensor:** - VCC -> 3V3 | GND -> GND | Signal -> GPIO 3
- **Relay Module:** - VCC -> 3V3/5V | GND -> GND | IN -> GPIO 4
- **Water Pump:** - Connected through the Relay's **COM** and **NO** (Normally Open) terminals.

## Software Setup
### 1. Requirements
- **Arduino IDE**
- **Libraries:** `WiFi.h`, `PubSubClient` (by Nick O'Leary).

### 2. MQTT Architecture
The system communicates via the following topics:
- `myfarm/sensor/moisture`: Publishes raw sensor values.
- `myfarm/pump/status`: Publishes current pump state (e.g., "ON (AUTO)").
- `myfarm/pump/command`: Subscribes to commands (`ON`, `OFF`, `AUTO`).

## Getting Started
1. **Wi-Fi Config:** Update `ssid` and `password` in the source code.
2. **Upload:** Flash the code to the ESP32-S3 via USB.
3. **Mobile Setup:**
   - Install an MQTT client (e.g., **MyMQTT**).
   - Connect to Host: `broker.emqx.io` (Port: `1883`).
   - Subscribe to moisture and status topics to monitor live data.
   - Publish strings to the command topic to control the pump.

---
*Developed for educational purposes in Embedded Systems and IoT.*
