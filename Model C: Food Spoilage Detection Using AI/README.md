# AI-Driven Food Spoilage Detection System

This module acts as a critical preventive safety barrier for vulnerable post-ICU patients. By digitizing environmental variables and identifying invisible biochemical markers of decay, the system detects food spoilage before ingestion occurs, effectively mitigating the risk of complications like dehydration or sepsis.

---

### Hardware Architecture

The system relies on a multi-sensor array deliberately mapped to ADC1 to ensure hardware compatibility with the Wi-Fi stack during active telemetry broadcasts.

| Component | Technical Role & Purpose in Detection |
| :--- | :--- |
| **ESP32 Hub** | Core processing unit orchestrating data acquisition and Port 80 hosting. |
| **ESP32-CAM** | Captures high-definition frames for the Port 81 MJPEG live stream. |
| **IR Sensor** | Verifies tray occupancy to prevent false-positive air quality alerts. |
| **MQ-4 Gas** | Identifies methane (CH4) gaseous markers of organic decomposition. |
| **MQ-135 Gas** | Detects ammonia and Hydrogen Sulfide (H2S), key indicators of rot. |
| **DHT22** | Tracks medical-grade temperature and humidity for environmental context. |
| **16x2 LCD** | Outputs immediate visual feedback and local alerts at the bedside. |

---

### Embedded Decision Logic

To maintain real-time responsiveness, the ESP32 utilizes dual concurrent tracking pathways that isolate video bandwidth from critical sensor data.

*   **Presence Validation:** The IR sensor confirms food is actively on the tray; if empty, the system enters a power-saving "Standby Status".
*   **Asynchronous Processing:** The camera hosts a continuous video stream (Port 81) while the main hub simultaneously polls environmental sensors (Port 80).
*   **Threshold Evaluation:** Upon food detection, ADC values are actively evaluated for dangerous concentration spikes in H2S and CH4.
*   **State Designation:** Safe conditions display "Vegetable is Fresh ✓", while chemical rot signatures instantly trigger a "Spoilage Alert".
*   **Preventive Lead Time:** This logical workflow shifts assessment from subjective human inspection to objective, threshold-based biochemical data.

---

### AI Engine & Web Interfacing

> **Note:** The multi-sensor AI classification engine processes combined environmental readings as a multi-dimensional array, allowing it to identify the complex "chemical spectrogram" of decomposition.

*   **Predictive Diagnostics:** By analyzing relationships between rising humidity and VOC emissions, the AI can detect spoilage up to 24 hours before visual markers appear.
*   **Unified Dashboard:** A Port 80 AJAX web interface seamlessly embeds the live video feed and updates visual telemetry cards instantly without requiring page refreshes.
*   **Network Fail-Safe:** An integrated IP switcher allows caregivers to dynamically reconfigure the camera stream URL in dynamic DHCP environments.
