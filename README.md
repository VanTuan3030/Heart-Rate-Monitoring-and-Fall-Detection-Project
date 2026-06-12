# Heart Rate Monitoring and Fall Detection Project

An IoT-based smart wearable device designed for real-time health tracking and fall detection. The system continuously monitors the user's heart rate to prevent cardiovascular risks and tracks body movements to detect sudden falls, providing immediate alerts through a mobile application.

---

## 🚀 Key Features

*   **Continuous Heart Rate Tracking:** Utilizes optical PPG technology via the MAX30102 sensor to track heart rate in real-time.
*   **Intelligent Fall Detection:** Uses the MPU6050 6-DOF accelerometer and gyroscope to recognize sudden orientation and acceleration changes.
*   **Low Energy Wireless Communication:** Transmits processed health data seamlessly to smartphones using Bluetooth Low Energy (BLE).
*   **Cloud Synchronization:** Real-time data logging and synchronization with Firebase Realtime Database.
*   **Ultra-low Cost Design:** Hardware architecture optimized around an affordable 8-bit MCU to minimize overall production costs.

---

## 🛠️ System Architecture

The overall hardware communication and data flow of the project can be referenced in the system block diagram below:

> For a visual representation of the hardware connections, please refer to the architecture diagram file named **"image_76413c.png"**.

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

## 💻 Software Stack

*   **ST Visual Develop (STVD):** Used for coding, compiling, and flashing the firmware onto the STM8 microcontroller.
*   **Arduino IDE:** Employed for prototyping and developing the ESP32 BLE firmware.
*   **Android Studio:** Used to build the mobile interface that connects via BLE and manages cloud data streams.
*   **Firebase Realtime Database:** Cloud backend utilized for immediate data synchronization and historical logs.

---

## 📝 Project Documentation

The complete project reporting, measurement analysis, and presentation slides can be found in the following files included in this repository:
*   Detailed project reports and final metrics are located in the document **"Baocao_IOT_Cuoiki.docx"**.
*   Presentation slides and system demonstrations are available in **"Baocao_DOLUONG_Cuoiki.pptx"** and **"Baocao_IOT_Cuoiki.pptx"**.

---

## ⚠️ Limitations & Future Enhancements

*   **Precision Constraints:** Low-cost commercial sensors were selected due to budget limits, making the device susceptible to noise during high-intensity movements.
*   **Basic Analytics:** The current mobile application acts as a real-time monitor and logger, without advanced predictive healthcare AI or smart anomaly alerts.
*   **Data Security:** The Firebase implementation relies on standard rules, requiring future encryption updates for production safety.

---

## 👥 Authors

*   **Võ Văn Tuấn** - *University of Transport and Communications (HCMC Campus)*
*   **Project Advisors:** TS. Nguyễn Văn Trung / TS. Lê Tiến Lộc
