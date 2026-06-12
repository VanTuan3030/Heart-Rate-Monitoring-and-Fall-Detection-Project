# Heart Rate Monitoring and Fall Detection Project

An IoT-based smart wearable device designed for real-time health tracking and fall detection[cite: 1, 2, 3]. The system continuously monitors the user's heart rate to prevent cardiovascular risks and tracks body movements to detect sudden falls, providing immediate alerts through a mobile application[cite: 1, 2, 3].

---

## 🚀 Key Features

*   **Continuous Heart Rate Tracking:** Utilizes optical PPG technology via the MAX30102 sensor to track heart rate in real-time[cite: 1, 2, 3].
*   **Intelligent Fall Detection:** Uses the MPU6050 6-DOF accelerometer and gyroscope to recognize sudden orientation and acceleration changes[cite: 1, 2, 3].
*   **Low Energy Wireless Communication:** Transmits processed health data seamlessly to smartphones using Bluetooth Low Energy (BLE)[cite: 1, 2, 3].
*   **Cloud Synchronization:** Real-time data logging and synchronization with Firebase Realtime Database[cite: 1, 2, 3].
*   **Ultra-low Cost Design:** Hardware architecture optimized around an affordable 8-bit MCU to minimize overall production costs[cite: 1, 2, 3].

---

## 🛠️ System Architecture

The overall hardware communication and data flow of the project can be referenced in the system block diagram below:

> For a visual representation of the hardware connections, please refer to the architecture diagram file named **"image_76413c.png"**[cite: 1, 3].

### Data Flow Breakdown:
1.  **Sensors (MAX30102 & MPU6050):** Capture physiological metrics and movement data, transferring raw digital signals via **I2C** to the central controller[cite: 1, 2, 3].
2.  **Central MCU (STM8):** Acts as the main brain, filtering background noise, processing the signals, and forwarding clean data packets via **UART**[cite: 1, 2, 3].
3.  **Wireless Core (ESP32):** Receives the compiled packets and advertises them over **BLE Notify** directly to the user's mobile device[cite: 1, 2, 3].
4.  **Android App:** Decodes the BLE data stream, displays the metrics instantly, and pushes historical logs onto **Firebase** via an Internet connection[cite: 1, 2, 3].

---

## 🔌 Hardware Specifications

| Component | Model / Type | Role in System | Key Technical Specs |
| :--- | :--- | :--- | :--- |
| **Central MCU** | STM8S103F3P6 | Data processing & sensor acquisition[cite: 1, 2, 3] | 8-bit Harvard core, 16 MHz, 8KB Flash[cite: 2, 3] |
| **Wireless Core** | ESP32-WROOM-32D | BLE transmission & WiFi gateway[cite: 1, 3] | 32-bit dual-core, 240MHz, BLE 4.2 & WiFi[cite: 1, 2, 3] |
| **Heart Rate Sensor**| MAX30102 | Optical pulse oximeter & heart-rate monitor[cite: 2, 3] | PPG method, 18-bit ADC, I2C interface[cite: 1, 2, 3] |
| **Motion Sensor** | MPU6050 | 6-DOF Accelerometer + Gyroscope[cite: 2, 3] | 16-bit ADC, I2C interface, fall detection[cite: 1, 2, 3] |
| **Power Management**| Li-ion Battery / AMS1117| Rechargeable power source[cite: 1, 2, 3] | 3.7V Li-ion battery, regulated down to 3.3V[cite: 1, 2, 3] |

---

## 💻 Software Stack

*   **ST Visual Develop (STVD):** Used for coding, compiling, and flashing the firmware onto the STM8 microcontroller[cite: 1, 2, 3].
*   **Arduino IDE:** Employed for prototyping and developing the ESP32 BLE firmware[cite: 1, 2, 3].
*   **Android Studio:** Used to build the mobile interface that connects via BLE and manages cloud data streams[cite: 1, 2, 3].
*   **Firebase Realtime Database:** Cloud backend utilized for immediate data synchronization and historical logs[cite: 1, 2, 3].

---

## 📝 Project Documentation

The complete project reporting, measurement analysis, and presentation slides can be found in the following files included in this repository:
*   Detailed project reports and final metrics are located in the document **"Baocao_IOT_Cuoiki.docx"**[cite: 2].
*   Presentation slides and system demonstrations are available in **"Baocao_DOLUONG_Cuoiki.pptx"**[cite: 1] and **"Baocao_IOT_Cuoiki.pptx"**[cite: 3].

---

## ⚠️ Limitations & Future Enhancements

*   **Precision Constraints:** Low-cost commercial sensors were selected due to budget limits, making the device susceptible to noise during high-intensity movements[cite: 1, 3].
*   **Basic Analytics:** The current mobile application acts as a real-time monitor and logger, without advanced predictive healthcare AI or smart anomaly alerts[cite: 1, 3].
*   **Data Security:** The Firebase implementation relies on standard rules, requiring future encryption updates for production safety[cite: 1, 3].

---

## 👥 Authors

*   **Võ Văn Tuấn** - *University of Transport and Communications (HCMC Campus)*[cite: 1, 2, 3]
*   **Ngô Huỳnh Quốc Huy** - *University of Transport and Communications (HCMC Campus)*[cite: 1, 2, 3]
*   **Project Advisors:** TS. Nguyễn Văn Trung / TS. Lê Tiến Lộc[cite: 1, 2, 3]
