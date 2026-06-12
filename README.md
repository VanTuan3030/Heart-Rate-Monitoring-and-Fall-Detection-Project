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

### Data Flow Breakdown:
1.  **Sensors (MAX30102 & MPU6050):** Capture physiological metrics and movement data, transferring raw digital signals via **I2C** to the central controller.
2.  **Central MCU (STM8):** Acts as the main brain, filtering background noise, processing the signals, and forwarding clean data packets via **UART**.
3.  **Wireless Core (ESP32):** Receives the compiled packets and advertises them over **BLE Notify** directly to the user's mobile device.
4.  **Android App:** Decodes the BLE data stream, displays the metrics instantly, and pushes historical logs onto **Firebase** via an Internet connection.

---

## 🔌 Hardware Specifications

| Component | Model / Type | Role in System | Key Technical Specs |
| :--- | :--- | :--- | :--- |
| **Central MCU** | STM8S103F3P6 | Data processing & sensor acquisition| 8-bit Harvard core, 16 MHz, 8KB Flash |
| **Wireless Core** | ESP32-WROOM-32D | BLE transmission & WiFi gateway | 32-bit dual-core, 240MHz, BLE 4.2 & WiFi |
| **Heart Rate Sensor**| MAX30102 | Optical pulse oximeter & heart-rate monitor | PPG method, 18-bit ADC, I2C interface |
| **Motion Sensor** | MPU6050 | 6-DOF Accelerometer + Gyroscope | 16-bit ADC, I2C interface, fall detection |
| **Power Management**| Li-ion Battery / AMS1117| Rechargeable power source | 3.7V Li-ion battery, regulated down to 3.3V |

---

## ⚙️ Firmware Architecture & Implementation

### 1. STM8 Core: Sensor Acquisition & Algorithmic Processing
The primary firmware running on the **STM8S103F3P6** manages raw sensor polling, digital signal processing (DSP) for pulse tracking, and the safety state machine.

* **Peripheral Allocation:** Driven by an 8-bit **TIM4** configured to trigger a periodic overflow every 1 ms (`current_millis`) for exact scheduling. Upstream transmission utilizes **UART1** initialized at `9600 bps (8N1)`.
* **PPG Signal Processing (MAX30102):**
    * *Proximity Boundary:* Enforces a finger-detection constraint (`FINGER_DETECT_THRESHOLD = 30000`). Falling below this resets all pipeline filters.
    * *Dual-Stage Smoothing:* Runs high-frequency noise suppression combined with a moving DC baseline tracker to isolate the heartbeat signal.
    * *Adaptive Peak Detection & Validation:* A pulse is registered via hysteresis thresholding. The system accepts Inter-Beat Intervals (IBI) only between 375 ms and 1350 ms (~44 to 160 BPM), rejecting sudden physiological anomalies.
* **Fall Assessment State Machine (MPU6050):**
    * *State 0 (NORMAL):* Continuously evaluates the squared vector magnitude. If an impact pierces the threshold (`ACCEL_IMPACT_THRESHOLD_SQ = 500,000,000`), it fires a `"PHAT_HIEN_NGA"` token and shifts to State 1.
    * *State 1 (SUSPECT):* Starts a 10-second verification timer. If vital recovery is recorded ($\ge$ 40 BPM), it restores normalcy. If the timer expires without valid vitals, it escalates to State 2.
    * *State 2 (ALARM):* Confirms an emergency scenario, broadcasting a looping `"DANG_BAO_DONG"` stream upstream until recovery metrics are established.

### 2. ESP32 Core: BLE & UART Wireless Gateway
The firmware on the **ESP32** functions as an asynchronous data bridge, wrapping raw wired serial telemetry into standard wireless low-energy profiles.

* **Asynchronous Bridging:** Continuously scans incoming packets from the STM8 over HardwareSerial, cleans them, and logs metrics to the hardware Serial monitor for debugging.
* **Nordic UART Service (NUS) Emulation:** Implements a custom BLE profile optimized for zero-latency data streaming:
    * **UART Service UUID:** `6E400001-B5A3-F393-E0A9-E50E24DCCA9E`
    * **TX Characteristic (`6E400003-...`):** Mode configured strictly to **NOTIFY** to stream cleaned sensor metrics directly to the app without acknowledgment overhead.
    * **RX Characteristic (`6E400002-...`):** Mode configured to **WRITE**, handling incoming handshake verification data from the mobile client.

---

## 💻 Software Stack

* **ST Visual Develop (STVD):** Used for coding, compiling, and flashing the firmware onto the STM8 microcontroller.
* **Arduino IDE:** Employed for prototyping and developing the ESP32 BLE firmware.
* **Android Studio:** Used to build the mobile interface that connects via BLE and manages cloud data streams.
* **Firebase Realtime Database:** Cloud backend utilized for immediate data synchronization and historical logs.

---

## ⚠️ Limitations & Future Enhancements

* **Precision Constraints:** Low-cost commercial sensors were selected due to budget limits, making the device susceptible to noise during high-intensity movements.
* **Basic Analytics:** The current mobile application acts as a real-time monitor and logger, without advanced predictive healthcare AI or smart anomaly alerts.
* **Data Security:** The Firebase implementation relies on standard rules, requiring future encryption updates for production safety.

---

## 👥 Authors

* **Võ Văn Tuấn** - *University of Transport and Communications (HCMC Campus)*
* **Project Advisors:** TS. Nguyễn Văn Trung / TS. Lê Tiến Lộc
