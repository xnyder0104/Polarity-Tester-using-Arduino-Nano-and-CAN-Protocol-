# Polarity Tester using Arduino Nano and CAN Protocol


# Polarity Tester using Arduino Nano and CAN Protocol

## Project Overview

This project is an automated polarity tester designed specifically for high-voltage battery systems, such as 51.2V 16S LiFePO4 (LFP) battery packs. Connecting batteries in reverse polarity can lead to dangerous consequences, including short circuits, permanent damage to the Battery Management System (BMS) and downstream circuits, spark hazards, and severe user safety risks.

To overcome the inefficiency and human error associated with manual multimeter checks , this system uses an Arduino Nano and optocouplers to automatically validate polarity. The status is communicated via LED indicators and the CAN protocol, ensuring a safe, real-time, and reliable solution for industrial and testing setups.

---

## Key Features & Results

* 
**Safe Voltage Isolation:** The circuit uses optocouplers to isolate the high-voltage battery side from the low-voltage control circuitry.


* 
**Clear Visual Indicators:** Three LEDs provide immediate status identification without the need for additional tools: Green for correct polarity, Red for reverse polarity, and Orange for no valid input.


* 
**Audible Alerts:** A buzzer activates to immediately alert the user if a reverse polarity connection is detected, which is useful in noisy or low-visibility environments.


* 
**Remote Monitoring:** Polarity data is transmitted over a CAN network, allowing seamless integration with broader Battery Management Systems (BMS) or remote monitoring stations.


* 
**Hardware Debugging:** The custom PCB design includes onboard test points for critical signals, such as analog lines and optocoupler outputs, to simplify debugging.



---

## Working Principle

* 
**Voltage Sensing:** Two PC817 optocouplers (U1 and U2) are connected across the battery input. U1 activates under correct polarity , while U2 activates under reverse polarity.


* 
**Microcontroller Logic:** The analog outputs from U1 and U2 are fed to pins A2 and A3 on the Arduino Nano, which reads them using the `analogRead()` function.


* 
**Right Polarity Event:** If only U1 is active, the system triggers the Green LED (D5) to indicate correct polarity.


* 
**Reverse Polarity Event:** If only U2 is active, the system triggers the Red LED (D4) and activates a buzzer via a BC-547 transistor switch circuit on digital pin D5.


* 
**Fail-Safe Mechanism:** If both optocouplers conduct simultaneously (due to a fault or noise), or neither conducts, the system defaults to a "no valid input" state and activates the Orange LED (D10) to prevent false positives.


* 
**CAN Bus Transmission:** The determined polarity status is encoded into a CAN frame and broadcasted over the CAN bus utilizing an MCP2515 CAN controller and a TJA1050 transceiver.



---

## Hardware Design & PCB Layout

* The PCB routing was carefully calculated, utilizing a 12 mil trace width to safely accommodate the necessary current and voltage.


* Teardrops were implemented on the PCB to strengthen solder joints and reduce mechanical stress at the pad connections.


* To accommodate the MCP2515 CAN controller and TJA1050 transceiver modules lacking standard footprints, 7 header pins were manually routed and placed, allowing the preassembled modules to be directly soldered onto the zero PCB.



---

## Applications

* Automotive polarity testing setups.


* Industrial battery diagnostics and validation.


* Laboratory equipment and testing station verification.


* Electrical maintenance and field troubleshooting.



---

## Future Scope

* 
**Wireless Data Transmission:** Integrating BLE modules or an ESP32 to wirelessly transmit polarity data to a centralized monitoring dashboard.


* 
**Automatic Shutdown/Relay Control:** Adding a relay-based cutoff system that automatically disconnects the electrical load if a reverse connection is detected for enhanced physical safety.


* 
**Multi-Channel Testing Support:** Scaling the hardware and software logic to evaluate multiple battery packs or channels simultaneously for large-scale industrial operations.
