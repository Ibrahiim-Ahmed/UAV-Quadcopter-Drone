
# 🛩️  Quadcopter Using ESP32-CAM, Coreless Motors, and MPU6050

This project is a fully functional **quadcopter drone** controlled by a custom-built transmitter using another **ESP32 board**. The drone features four **coreless brushed motors** driven by **MOSFETs**, real-time orientation sensing via **MPU6050 (6-DOF)** IMU, and full control via **Wi-Fi UDP packets**—with no need for commercial radio controllers or NRF24 modules.

It serves as a brilliant demonstration of wireless communication, embedded control, and multi-motor synchronization using simple and cost-effective components.

---

## 🧠 Project Overview

The drone is powered by an **ESP32-CAM**, which controls four motors through MOSFETs based on real-time orientation and joystick commands sent over Wi-Fi from a hand-held ESP32-based transmitter. The MPU6050 IMU provides orientation feedback, enabling future stabilization and auto-leveling features. This project replaces traditional radio modules with **UDP-based wireless control**—a cleaner, faster, and more modern alternative.

The transmitter features two joysticks (4 axes), and its input is transmitted over UDP at regular intervals. The receiver decodes the values and maps them to motor PWM duty cycles for flight control.

---

## 🧩 Component List and Their Functions

| Component                          | Function                                                             |
| ---------------------------------- | -------------------------------------------------------------------- |
| 🔲 **ESP32-CAM**                   | Acts as flight controller and Wi-Fi receiver; controls motor outputs |
| 🧠 **MPU6050 IMU**                 | Provides gyro and accelerometer data for attitude sensing            |
| ⚙️ **4x Coreless DC Motors**       | Provides thrust and direction control                                |
| 🔲 **ESP32 DevKit**                | Transmitter; reads joystick values and sends over Wi-Fi              |
| 🕹 **2x Analog Joysticks**          | Used for pitch, roll, yaw, and throttle control                      |
| 📶  RF (nRF24L01)                  | nRF24 is a series of low-power, 2.4 GHz transceiver                  |
| 🔌 **N-Channel MOSFETs (x4)**      | Acts as motor drivers, switching PWM to control motor speed          |
| 🔋 **Li-Po Battery (3.7V)**        | Power supply for drone and motors                                    |
| 📦 **Frame/Chassis**               | Holds all components; can be 3D-printed or custom-built              |
| 🔌 **UART-USB Adapter**            | Used to program the ESP32-CAM via serial                             |
| 🪛 **Jumper wires, headers, etc.** | For electrical connections                                           |

---


## 🔁 Control Flow (How It Works)


## 🌐 Communication Technologies Overview

This drone system is designed to be flexible in terms of wireless communication and can be adapted to work with **Wi-Fi**, **RF (nRF24L01)**, or **Bluetooth**, depending on the requirements of range, latency, and simplicity. Here's a brief comparison of each:

### 🔵 1. **Bluetooth**

* **Range**: \~10 meters (Classic) / \~30 meters (BLE)
* **Speed**: Moderate (up to 2 Mbps)
* **Latency**: Low
* **Pros**:

  * Simple to implement
  * Low power consumption
  * Built-in support on most phones and laptops
* **Cons**:

  * Shorter range than RF or Wi-Fi
  * Prone to interference
* **Use Case**: Suitable for indoor, short-range control or phone-controlled drones

---

### 📶 2. **RF (nRF24L01)**

* **Range**: \~100 meters (up to 1 km with PA+LNA)
* **Speed**: Up to 2 Mbps
* **Latency**: Very low
* **Pros**:

  * Long-range, reliable, low-latency communication
  * Excellent for real-time motor control
  * Works well with Arduino/ESP32
* **Cons**:

  * Requires dedicated modules and wiring
  * Needs careful antenna placement
* **Use Case**: Ideal for outdoor, long-range drone control with minimal delay

---

### 🌐 3. **Wi-Fi (UDP over ESP32)**

* **Range**: \~50 meters (can be extended with external antennas)
* **Speed**: High (up to 150 Mbps on ESP32)
* **Latency**: Low (\~10–20 ms with UDP)
* **Pros**:

  * High-speed, IP-based communication
  * Can integrate with video streaming (ESP32-CAM)
  * Works on existing home/portable routers
* **Cons**:

  * Slightly higher latency than RF
  * Connection drop if signal is weak
* **Use Case**: Perfect for development, testing, and adding camera/video or network-based control systems like LabVIEW, mobile apps, or web-based GUIs

---

### ✅ Summary

| Feature        | Bluetooth     | nRF24L01          | Wi-Fi (UDP)   |
| -------------- | ------------- | ----------------- | ------------- |
| **Range**      | Low           | High              | Medium        |
| **Speed**      | Moderate      | Moderate–High     | High          |
| **Latency**    | Low           | Very Low          | Low           |
| **Complexity** | Easy          | Medium            | Medium–High   |
| **Use Case**   | Phone control | Dedicated RC-like | Networked/FPV |

This project is versatile and can easily be switched between these modes by changing the communication layer in the firmware. All modes are supported by the ESP32 platform, giving developers full control over how the drone communicates and behaves.

---

## 🔧 Key Features

✅ Pure Wi-Fi control (or RF modules like nRF24)
✅ ESP32 dual-core allows camera + control logic
✅ Fast and responsive real-time control
✅ Modular & open-source firmware
✅ Extendable for FPV, autonomous flight, PID stabilization
✅ Beginner-friendly with low-cost hardware

---

## 🛠️ Working Principle

* Each joystick axis sends one byte (0–255) representing a control value (e.g., throttle, pitch).
* On the drone, the ESP32-CAM reads these values via Wi-Fi UDP, then converts them to PWM outputs.
* The motors are controlled via MOSFETs, with each motor driving a corner of the drone.
* The MPU6050 can be used for orientation correction and stabilization (currently optional).

---


![radio](https://github.com/user-attachments/assets/97bc4b88-0271-4c42-9c63-b53a212d4d4d)
![drone](https://github.com/user-attachments/assets/3fa8ffaa-f350-433d-b608-7065d2ec62e8)

## 🧪 Learning Objectives

This project helps you learn about:

* 🔗 Wi-Fi-based UDP communication in embedded systems
* 📶 RF wireless communication
* ⚙️ MOSFET-based motor control
* 🧠 Reading and interpreting joystick input
* 📐 Real-time motor control based on sensor or network data
* 📡 Building a networked control system
* 🔧 Using I²C sensors with ESP32 (MPU6050)

---

## ⚠️ Limitations

* Basic throttle-only control for now (stabilization must be tuned manually)
* Wi-Fi latency is low (\~10 ms) but not zero — not for acrobatic flight
* ESP32-CAM GPIOs are limited; care needed with power routing
* No PID stabilization yet — requires manual tuning or firmware expansion
* UDP is connectionless — no feedback if packets are lost (consider adding ACK for robustness)

---


## 🛫 Getting Started

1. Flash the transmitter and receiver using Arduino IDE
2. Power the drone with a Li-Po battery (3.7V, \~500mAh)
3. Power the transmitter (USB or battery)
4. Connect both to the same Wi-Fi network (or use softAP)
5. Observe serial monitor to confirm data reception
6. Motors should spin upon successful connection

---

## 🧠 Future Improvements

* Add full PID stabilization using MPU6050
* Integrate battery monitoring and low-voltage cut-off
* Implement failsafe (kill motors on disconnection)
* Add web interface to adjust motor gains
* Use the camera feed for FPV or vision-based control
* OTA updates via Wi-Fi

---

## 📜 License
Feel free to modify, remix, or expand this project for your own creative drone builds!

---

