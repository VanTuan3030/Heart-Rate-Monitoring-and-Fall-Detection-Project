# Heart Rate Monitoring and Fall Detection Project

An IoT-based smart wearable device designed for real-time health tracking and fall detection. The system continuously monitors the user's heart rate to prevent cardiovascular risks and tracks body movements to detect sudden falls, providing immediate alerts through a mobile application.

---

## 🚀 Key Features

* **Continuous Heart Rate Tracking:** Utilizes optical PPG technology via the MAX30102 sensor to track heart rate in real-time.
* **Intelligent Fall Detection:** Uses the MPU6050 6-DOF accelerometer and gyroscope to recognize sudden orientation and acceleration changes.
* **Low Energy Wireless Communication:** Transmits processed health data seamlessly to smartphones using Bluetooth Low Energy (BLE).
* **Cloud Synchronization:** Real-time data logging and synchronization with Firebase Realtime Database.
* **Ultra-low Cost Design:** Hardware architecture optimized around an affordable 8-bit MCU to minimize overall production costs.

---

## 🛠️ System Architecture & Data Flow

The system architecture is split into data collection, local preprocessing, wireless bridging, and cloud monitoring.

```text
[ Sensors: MAX30102 / MPU6050 ]
               │
               ▼ (I2C Bus)
  [ Central MCU: STM8S103F3 ]  <-- (Low-level filtering & State Machine)
               │
               ▼ (UART @ 9600 bps)
 [ Wireless Core: ESP32-WROOM ] <-- (BLE Gateway & NUS Emulation)
               │
               ▼ (BLE Notify Stream)
    [ Android Application ]    <-- (UI Display & Threshold Checking)
               │
               ▼ (WiFi / Cellular Link)
 [ Firebase Realtime Database ] <-- (Cloud Logs & History Tracking)
