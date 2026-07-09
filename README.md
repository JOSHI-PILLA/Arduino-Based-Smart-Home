# 🏠 Arduino-Based Smart Home Automation System

An automated, sensor-driven home control system built and simulated on Tinkercad using an Arduino UNO as the central controller.

**Project Submitted By:** Pilla Joshi
**Platform:** Arduino UNO (simulated in Tinkercad)

---

## 📋 Overview

This project implements a multi-function Smart Home Automation System that integrates five independent sensing and control modules into a single circuit:

- 🔒 Automatic Door Lock
- 💡 Automatic Light Control
- 🚨 Gas Leak Detection
- 🛡️ Locker Security Alarm
- 🌡️ Temperature-Controlled Fan

All live readings and alerts are displayed on a 16x2 I2C LCD and mirrored on the Arduino Serial Monitor for easy observation and debugging during simulation.

---

## 🎯 Objectives

- Automatically lock/unlock the main door based on the proximity of a person, using an ultrasonic distance sensor and a servo motor.
- Automatically switch the room light ON/OFF based on ambient brightness sensed by an LDR.
- Continuously monitor for gas leaks using an MQ gas sensor and trigger a buzzer + LCD warning when gas is detected.
- Detect unauthorized motion near a locker/cabinet using a PIR sensor and raise a security alarm.
- Monitor room temperature with a TMP36 sensor and regulate an exhaust fan's speed (PWM) accordingly.
- Display all live sensor data centrally on an I2C 16x2 LCD and on the Serial Monitor.

---

## 🔧 Components Used

| Component | Reference | Function |
|---|---|---|
| Arduino UNO | U1 | Main microcontroller; reads all sensors and drives all outputs |
| Ultrasonic Distance Sensor | DIST1 | Measures distance at the door to detect an approaching person |
| Micro Servo Motor | U3 | Acts as the electronic door lock (locks/unlocks) |
| LDR (Light Dependent Resistor) | R2 | Detects ambient light level for automatic lighting |
| LED (White) | LED2 | Represents the room light, switched automatically |
| MQ Gas Sensor | GAS1 | Detects LPG / smoke / gas leakage |
| DC Motor | M1 | Represents the exhaust fan, speed-controlled by PWM |
| Diode | D1 | Flyback protection diode across the motor |
| PIR Motion Sensor | PIR1 | Detects motion near the locker/cabinet for security |
| Piezo Buzzer | U2 | Sounds audible alerts for gas leak and intrusion |
| TMP36 Temperature Sensor | U5 | Monitors room temperature to control the fan |
| 16x2 I2C LCD Display | U4 | Displays live sensor readings and system status |
| Red Alarm LED | LED2 (bottom) | Visual alarm indicator |
| Resistors | R1, R3, R4 | Current-limiting resistors for LED/transistor circuits |
| NPN Transistor | Q1 | Switches the PIR/buzzer stage |

---

## 🔌 Key Pin Connections

| Signal | Arduino Pin | Purpose |
|---|---|---|
| trigPin | 9 | Ultrasonic sensor trigger (door distance) |
| echoPin | 10 | Ultrasonic sensor echo (door distance) |
| servoPin | 6 | Controls the door-lock servo motor |
| LDR | Analog pin | Reads ambient light level |
| Gas sensor | Analog pin | Reads MQ gas sensor value |
| TMP36 | Analog pin | Reads temperature for fan PWM control |
| PIR | Digital pin | Detects locker motion |
| Buzzer / LEDs | Digital pin(s) | Drives audible and visual alarms |
| I2C (SDA/SCL) | A4 / A5 | Communicates with the 16x2 LCD (address 0x27) |

---

## ⚙️ Working Principle

### 1. Automatic Door Lock
The HC-SR04 ultrasonic sensor continuously measures the distance of any object/person approaching the door. When the measured distance falls below a preset threshold, the Arduino commands the servo motor to rotate to the "unlocked" position; otherwise the door remains "locked." Live distance and lock status are printed on both the LCD and Serial Monitor.

### 2. Automatic Light Control
The LDR produces a varying analog voltage depending on surrounding light intensity. The Arduino reads this value and switches the room LED ON when it's dark (low LDR value) and OFF when bright, keeping the room lit automatically.

### 3. Gas Leak Detection
The MQ gas sensor outputs an analog value proportional to combustible gas/smoke concentration. When this crosses the safety threshold, the system flags "GAS LEAK DETECTED," sounds the buzzer in a repeating beep pattern, and displays a warning on the LCD.

### 4. Locker Security (PIR Motion Sensing)
A PIR sensor watches for motion near a protected locker or cabinet. Detected motion is treated as a potential intrusion: the system logs "Locker Motion: DETECTED! ALARM," sounds the buzzer, and updates the LCD/Serial Monitor.

### 5. Temperature-Controlled Fan
The TMP36 sensor reports ambient temperature in °C. The Arduino maps this reading to a PWM value that drives the DC motor (exhaust fan) — the higher the temperature, the faster the fan spins.

### 6. Centralized Status Display
All five modules share one 16x2 I2C LCD (address 0x27). The display cycles through door status/distance, light status, temperature/fan PWM, gas status, and locker motion status, while the same info streams continuously to the Serial Monitor.

---

## 🖥️ Simulation Outputs

| Test | Result |
|---|---|
| **Door Unlocked** | Distance ≈41–42 cm (within threshold) → LCD: "Door: UNLOCKED, Dist: 41 cm" |
| **Light ON** | LDR value 323 (low light) → LCD: "Light: ON, LDR Val: 323" |
| **Gas Leak Detected** | Gas value 1023 (max) → LCD: "Gas Value: 1023, LEAK DETECTED!" + 2 beeps |
| **Locker Motion Detected** | PIR triggers → LCD: "Locker Motion: DETECTED! ALARM" + 1 beep |
| **Temperature & Fan** | Temp 39.04°C → LCD: "Temp: 39.04C, Fan PWM: 255" (full speed) |

*(See the original circuit diagram and simulation screenshots in the full documentation for visual reference.)*

---

## ✅ Conclusion

The Arduino-based Smart Home system successfully demonstrates how a single microcontroller can coordinate multiple independent sensors and actuators to automate everyday home functions — secure entry, lighting, safety monitoring, and climate control. Simulation results confirm that each module responds correctly to its respective sensor input, with all statuses consistently reflected on both the LCD display and Serial Monitor.

---

## 🚀 Future Scope

- **IoT & Remote Monitoring** — Wi-Fi (ESP8266/ESP32) or Bluetooth module for remote monitoring/control via smartphone app or cloud dashboard.
- **Mobile App / Voice Control** — Google Assistant, Amazon Alexa, or a dedicated app for voice/UI-based control.
- **SMS/Email/Push Notifications** — Instant alerts via GSM module or cloud services (Twilio, Firebase) during gas leaks or intrusions.
- **Camera-Based Security** — ESP32-CAM integration with the PIR sensor for visual verification of intrusions.
- **Biometric / RFID Door Access** — RFID cards, fingerprint sensors, or keypad PIN access for stronger door security.
- **Data Logging & Analytics** — SD card or cloud database storage of sensor readings for trend analysis.
- **Solar-Powered / Energy-Efficient Design** — Solar panel with battery backup for energy independence.
- **Multi-Room Scalability** — Distributed system with multiple Arduino/ESP nodes networked for whole-house automation.
- **AI-Based Predictive Automation** — ML models to predict user patterns and proactively adjust lighting, locks, and fan speed.
- **Enhanced Gas Safety Response** — Automatic gas valve shutoff (solenoid valve) and ventilation activation on leak detection.

---

## 🛠️ Tools Used

- **Arduino UNO** (microcontroller)
- **Tinkercad** (circuit design & simulation)
- **16x2 I2C LCD**, ultrasonic sensor, servo motor, LDR, MQ gas sensor, PIR sensor, TMP36 sensor, DC motor, piezo buzzer
