# RBN-Autonomous-Robot
This project demonstrates an **autonomous obstacle-avoiding robot** that uses two microcontrollers — an **ESP32** and an **Arduino Nano BLE 33** — working together via serial communication.  
The system uses **ultrasonic sensors** to detect obstacles and **LED indicators** to display system status and issues.  
Motor control is handled through an **L298N motor driver**, powered by a 12V battery pack regulated by a **step-down converter**. The robot can also be manually controlled through an app using a bluetooth connection.

## Components Used

| Component | Quantity | Description |
|------------|-----------|-------------|
| **ESP32-WROOM-32** | 1 | Main microcontroller that reads ultrasonic sensors, processes distance, and sends commands to Nano BLE 33 |
| **Arduino Nano BLE 33** | 1 | Motor controller that receives movement commands from ESP32 and drives the motors via L298N |
| **Ultrasonic Sensor (HC-SR04)** | 2 | Used for obstacle detection — front-left and front-right |
| **L298N Motor Driver** | 1 | Controls two DC motors; powered by 12V for efficient operation |
| **DC Motors** | 2 | Connected to L298N for movement |
| **Caster Wheel** | 1 | Supports balance and helps with turning |
| **LEDs (Red, Yellow, Green)** | 3 | Status indicators: Red = Stop/Error, Yellow = Communication Active, Green = System Ready |
| **Resistors (220Ω - 330Ω)** | 3 | For current limiting of the LEDs |
| **Battery Pack of 4 cells (Li-on)(12V) ** | 1 | Primary power source for motors and electronics |
| **Step-Down Converter (Buck Converter)** | 1 | Regulates voltage from 12V down to 5V for logic circuits |
| **Breadboard** | 1 | For prototyping and distributing power |
| **Jumper Wires** | — | Used for all connections |
| **T-Slot Aluminium extrusion** | 3 | the pillars of this robot to make it stand up right |

## System Overview

1. The **ESP32** continuously reads distance values from two ultrasonic sensors.
2. When an obstacle is detected within **20 cm**, the ESP32 decides to change direction.
3. The ESP32 sends movement commands (forward, backward, left, right, stop) to the **Arduino Nano BLE 33**.
4. The **Nano BLE 33** drives the **L298N motor driver** according to those commands.
5. **LED indicators** show system status:
   - 🔴 **Red LED:** Stop or error
   - 🟡 **Yellow LED:** Communication active
   - 🟢 **Green LED:** System ready and moving
6. A **step-down converter** ensures stable 5V power to all logic components, while the **L298N** receives a dedicated 12V line for motor power.

## Power Management

- The **battery pack (12V)** connects to:
  - The **L298N motor driver** directly (for motor power)
  - The **step-down converter**, which outputs **5V**
- The **5V output** from the converter feeds:
  - **Breadboard 5V rail**
  - **ESP32 VIN pin**
  - **Arduino Nano BLE 33 5V pin**
  - **LEDs and Ultrasonic Sensors**

  ### Important:
- **Common Ground:** The ESP32, Nano BLE 33, and all sensors **share the same ground** for stable communication.
- The **L298N** uses **12V for motor VCC** and **5V for logic VCC**.
- The **caster wheel** ensures smooth pivoting during turns.

## Communication Setup

- **TX2 (ESP32)** → **RX (Nano BLE 33)**
- **RX2 (ESP32)** → **TX (Nano BLE 33)**
- Communication is based on **Serial UART** protocol for reliable command transfer.

## Wiring Summary

### ESP32 Connections
| ESP32 Pin | Component | Function |
|------------|------------|----------|
| 23 | Ultrasonic Sensor 1 (Trigger) | Distance sensing |
| 22 | Ultrasonic Sensor 1 (Echo) | Distance sensing |
| 21 | Ultrasonic Sensor 2 (Trigger) | Distance sensing |
| 19 | Ultrasonic Sensor 2 (Echo) | Distance sensing |
| 25 | Red LED | Stop/Error indicator |
| 26 | Yellow LED | Communication active |
| 27 | Green LED | System ready |
| VIN | Step-down 5V output | Power input |
| GND | Common ground | Shared with Nano BLE 33 and sensors |

### Arduino Nano BLE 33 + L298N Connections
| Nano BLE 33 Pin | L298N Pin | Function |
|------------------|-----------|----------|
| 9 | ENA | Motor A enable |
| 3 | IN1 | Motor A direction |
| 6 | IN2 | Motor A direction |
| 10 | ENB | Motor B enable |
| 5 | IN3 | Motor B direction |
| 11 | IN4 | Motor B direction |
| 5V | Step-down 5V output | Power input |
| GND | Common ground | Shared with ESP32 and L298N |

## Command Protocol

The **ESP32** sends single-character commands to the **Nano BLE 33**:
| Command | Action |
|----------|--------|
| `F` | Move Forward |
| `B` | Move Backward |
| `L` | Turn Left |
| `R` | Turn Right |
| `S` | Stop |
When an obstacle is detected:
- If **distance < 20 cm**, the ESP32 sends a **turn command** to avoid collision.

### Future Improvements

-Add IMU sensor (MPU6050) for motion stabilization.

-Implement PID control for smoother turns.

-Integrate camera or computer vision for object tracking.

-Add Wi-Fi dashboard for monitoring distance and battery levels.

## Author

Theophillus Ntate
A hands-on robotics enthusiast exploring embedded systems, wireless communication, and autonomous robotics design.

## These are images of the process on building this AutoBot.

![IMG_20250929_142637](https://github.com/user-attachments/assets/8171cb13-dda6-4456-b894-1602c0f49657)

![IMG_20251007_081525](https://github.com/user-attachments/assets/58a8e55d-0294-4a27-b285-a37b2c647237)

![IMG_20251008_105320](https://github.com/user-attachments/assets/2313281c-a2f6-4702-b920-61752e8c5469)


![IMG_20251008_111727](https://github.com/user-attachments/assets/0d0f644f-716c-432f-9101-c6cac7e3ac01) 


![IMG_20251008_112130](https://github.com/user-attachments/assets/77a0712f-3d7b-40af-a7f9-5657b4832d73)

![IMG_20251009_162838](https://github.com/user-attachments/assets/35ab1e0a-e7c3-4ea9-9380-d7392d8baa6e)

![IMG_20251008_115028](https://github.com/user-attachments/assets/30c8a266-6f56-4d26-8278-b78fe7f688ba)
![Screenshot_20251011_092858_com_hihonor_photos_SlotAlbumActivity](https://github.com/user-attachments/assets/146973bb-bb84-465e-a8b7-4bb4e95141f4)

![IMG_20251008_114437](https://github.com/user-attachments/assets/9e91d060-988c-4a17-913f-b33fb273fc72)

![IMG_20251009_165749](https://github.com/user-attachments/assets/2c4eab65-c691-41c1-9276-334eab97b0dd)

![IMG_20251010_143951](https://github.com/user-attachments/assets/9909cac4-71df-4c80-aa1c-465c5789b5a6)

### this is how the app will look
![Screenshot_20251011_115544_appinventor_ai_theontate1_Assistive_bot_Screen1](https://github.com/user-attachments/assets/0b76ebcf-c406-4faa-a2e3-a11241587fba)
