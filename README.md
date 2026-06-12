# Heart Rate Monitoring and Fall Detection Project

An IoT-based smart wearable device designed for real-time health tracking and fall detection. The system monitors the user's heart rate continuously to prevent cardiovascular risks and tracks body orientation to detect sudden falls, providing immediate alerts via a mobile application.

---

## 🚀 Key Features

*   **Continuous Heart Rate Tracking:** Utilizes optical PPG technology to track heart rate in real-time.
*   **Intelligent Fall Detection:** Uses a 6-DOF accelerometer and gyroscope to distinguish between normal activities and accidental falls.
*   **Low Energy Wireless Communication:** Transmits data seamlessly to smartphones using Bluetooth Low Energy (BLE).
*   **Cloud Synchronization:** Real-time data logging and synchronization with Firebase Database.
*   **Ultra-low Cost & Compact Design:** Optimized hardware using an 8-bit MCU to minimize production costs and power consumption.

---

## 🛠️ System Architecture

The overall hardware communication and data flow of the project can be referenced in the system block diagram below:

> Please refer to the system block diagram file named **"image_76413c.png"** for a detailed view of the hardware architecture[cite: 1].

### Data Flow Breakdown:
1.  **Sensors (MAX30102 & MPU6050)** capture physiological and motion data, sending raw digital signals via **I2C** to the central MCU[cite: 1, 2].
2.  **MCU (STM8)** filters background noise, processes the signal, and forwards the streamlined health packets to the wireless module via **UART**[cite: 1, 2].
3.  **Wireless Module (ESP32)** advertises and transmits the compiled data over **BLE Notify** directly to the user's smartphone[cite: 1, 2].
4.  **Android App** decodes the BLE stream, displays current metrics, and pushes the history logs to **Firebase Realtime Database** via Internet connection[cite: 1, 2].

---

## 🔌 Hardware Specifications

| Component | Model / Type | Role in System | Key Technical Specs |
| :--- | :--- | :--- | :--- |
| **Central MCU** | STM8S103F3P6 | Data processing & sensor reading[cite: 1, 2] | 8-bit Harvard core, 16 MHz, 8KB Flash[cite: 2, 3] |
| **Wireless Core** | ESP32-WROOM-32D | BLE transmission & WiFi gateway[cite: 1, 3] | 32-bit dual-core, 240MHz, BLE 4.2 & WiFi[cite: 1, 2] |
| **Heart Rate Sensor**| MAX30102 | Optical pulse oximeter & heart-rate[cite: 2, 3] | PPG method, 18-bit ADC, I2C interface[cite: 2, 3] |
| **Motion Sensor** | MPU6050 | 6-DOF Accelerometer + Gyroscope[cite: 2, 3] | 16-bit ADC, I2C interface, fall detection[cite: 2, 3] |
| **Power Management**| Li-ion 3.7V / AMS1117 | Rechargeable power source[cite: 1, 2] | 800mAh battery, regulated down to 3.3V[cite: 1, 2] |

---

## 💻 Software Stack

*   **ST Visual Develop (STVD):** Used for coding and flashing firmware onto the STM8 microcontroller[cite: 1, 2].
*   **Arduino IDE:** Used for prototyping and developing the ESP32 BLE firmware[cite: 1, 2].
*   **Android Studio:** Used to build the mobile interface that connects via BLE and manages cloud streams[cite: 1, 2].
*   **Firebase Realtime Database:** Cloud backend utilized for immediate data synchronization and historical logs[cite: 1, 2].

---

## ⚠️ Limitations & Future Work

> *   **Precision Constraints:** Due to budget limits, commercial-grade low-cost sensors were used, making the device prone to environment noise during heavy movement[cite: 1, 3].
> *   **Basic Analytics:** The current Android application version only acts as a real-time monitor and logger without advanced predictive healthcare AI algorithms[cite: 1, 3].
> *   **Data Security:** Firebase implementation is currently using a default setup, which requires encryption upgrades for production safety[cite: 1, 3].

---

## 👥 Authors

*   **Võ Văn Tuấn** - *University of Transport and Communications (HCMC Campus)*[cite: 1, 2]
*   **Ngô Huỳnh Quốc Huy** - *University of Transport and Communications (HCMC Campus)*[cite: 1, 2]
*   **Advisor:** TS. Nguyễn Văn Trung / TS. Lê Tiến Lộc[cite: 1, 2]
