# TheoBot Bluetooth App User Manual

This document describes how to use the **TheoBot Control App** to manually control the autonomous robot via Bluetooth.  
It is intended for users who want to understand how to connect to the robot and operate it using their mobile device.

---

## 1. Overview

The **TheoBot Control App** allows the user to manually override the robot’s autonomous mode.  
When connected via Bluetooth, you can move the robot **Forward**, **Backward**, **Left**, **Right**, or **Stop** using simple on-screen buttons.

The app communicates directly with the **ESP32-WROOM32** microcontroller inside the robot, which then relays movement commands to the **Arduino Nano BLE33**.

---

## 2. Interface Layout

The app interface consists of the following controls:

| Section | Description |
|----------|--------------|
| **Top Button** | `Available Devices` — Displays all Bluetooth devices that are currently paired with your phone. |
| **Directional Buttons** | `L`, `R`, `F`, `B`, and `S` — Control the robot’s movement. |

### Button Layout (Example Visualization)


     [ Available Devices ]
             
            [  F  ]
    [  L  ] [  S  ] [  R  ]
            [  B  ]


- **F** – Move Forward  
- **B** – Move Backward  
- **L** – Turn Left  
- **R** – Turn Right  
- **S** – Stop (center button)

---

## 3. Connecting to TheoBot

1. **Turn ON** the TheoBot robot.
2. Wait for the **Yellow LED** to light up, indicating that the Bluetooth module (ESP32) is active.
3. Open the **TheoBot Control App** on your smartphone.
4. Tap on **“Available Devices”** at the top of the app.
5. A list of paired Bluetooth devices will appear.
   - If you’ve paired before, **TheoBot** should appear automatically in the list.
6. Tap **“TheoBot”** to connect.
7. Once connected:
   - The app will display that the robot is **“Waiting for signal…”** or **“Connected to TheoBot”**.
   - The **Yellow LED** on the robot will blink to indicate manual control mode is active.

---

## 4. Controlling the Robot

After a successful connection:

| Button | Command Sent | Action |
|---------|---------------|--------|
| **F** | `F` | Moves robot forward |
| **B** | `B` | Moves robot backward |
| **L** | `L` | Turns robot left |
| **R** | `R` | Turns robot right |
| **S** | `S` | Stops the robot immediately |

### Tips
- Hold or tap **F**, **B**, **L**, or **R** for continuous movement.
- Hold **S** to halt movement at any time.
- The robot remains in **manual control mode** until the `A` (autonomous) command is received, or until the app disconnects.

---

## 5. Switching Back to Autonomous Mode

1. Exit the app or disconnect from Bluetooth.
2. The ESP32 will stop receiving manual commands.
3. The **Green LED** will turn on, and the robot will resume **autonomous navigation**.

---

## 6. Troubleshooting

| Issue | Possible Cause | Solution |
|--------|----------------|----------|
| TheoBot not visible in “Available Devices” | Not paired yet | Pair TheoBot in your phone’s Bluetooth settings first. |
| App says “Waiting for signal…” indefinitely | ESP32 not ready / wrong device selected | Restart TheoBot and reconnect. |
| Commands not responding | Serial link between ESP32 and Nano BLE33 disconnected | Check TX/RX connections and baud rate (115000). |
| Robot keeps stopping | Weak Bluetooth connection | Stay within 10 meters of the robot. |

---

## 7. Additional Notes

- Bluetooth name: **TheoBot**
- Default pairing PIN (if required): `1234`
- Communication mode: **Serial over Bluetooth**
- Baud rate: **115000**
- The app can be used on **Android** devices supporting Bluetooth SPP (Serial Port Profile).

---
