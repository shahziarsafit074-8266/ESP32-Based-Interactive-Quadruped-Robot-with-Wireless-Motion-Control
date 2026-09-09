# ESP32-Based Interactive Quadruped Robot with Wireless Motion Control

An ESP32-based interactive quadruped robot featuring 8-DOF coordinated movement, Wi-Fi wireless control, and an animated OLED face. The mechanical/CAD structure of the robot is based on the open-source **Sesame Robot** project by Dorian Borian, while this project implements its own ESP32-based hardware integration, firmware, motion sequences, and project documentation.

---

## 📌 Project Overview

Quadruped robots provide a useful platform for learning robotics, embedded systems, wireless communication, servo control, and mechanical design. Commercial quadruped robots can be expensive and difficult for students and hobbyists to access.

This project develops a low-cost interactive quadruped robot using an **ESP32-WROOM-32** as the main controller. The robot uses eight **MG90S metal gear servo motors** to control four legs with a total of **8 degrees of freedom (8-DOF)**.

An **SSD1306 0.96-inch 128×64 OLED display** is integrated into the robot to provide animated facial expressions synchronized with robot activities.

The ESP32's built-in Wi-Fi capability is used for wireless control. The robot can create its own Wi-Fi access point and host a browser-based controller, allowing a smartphone or computer to send movement commands without requiring an external Wi-Fi router.

---

## ✨ Main Features

- 🤖 ESP32-WROOM-32 based quadruped robot
- 🦿 4-legged mechanical structure
- ⚙️ 8 × MG90S metal gear servo motors
- 🎯 8 degrees of freedom (8-DOF)
- 📡 Built-in ESP32 Wi-Fi wireless control
- 🌐 Browser-based web controller
- 📱 Smartphone/computer control through Wi-Fi
- 👀 0.96-inch SSD1306 128×64 OLED display
- 😊 Animated facial expressions
- 🚶 Forward and backward walking
- ↩️ Left and right turning
- 👋 Waving
- 💃 Dancing
- 💪 Push-up and other predefined poses
- 🧍 Standing/resting poses
- 🔧 Servo calibration and sub-trim support
- 🧩 Modular and expandable architecture
- 🖨️ 3D-printed PLA mechanical structure

---

## 🧠 System Architecture

The ESP32 works as the central controller of the robot.

```text
                    ┌─────────────────────┐
                    │       ESP32         │
                    │   Main Controller   │
                    └──────────┬──────────┘
                               │
              ┌────────────────┼────────────────┐
              │                │                │
              ▼                ▼                ▼
       ┌────────────┐   ┌────────────┐   ┌──────────────┐
       │ 8× MG90S   │   │ SSD1306    │   │ Wi-Fi / Web  │
       │  Servos    │   │   OLED     │   │  Controller  │
       └────────────┘   └────────────┘   └──────────────┘
              │                │                │
              ▼                ▼                ▼
        Leg Movement      Facial Display    User Commands
```

The user sends a command through the wireless web interface. The ESP32 receives the command, selects the corresponding predefined movement sequence, controls the servo motors, and updates the OLED facial animation.

---

## 🦿 Degrees of Freedom

The robot contains four legs, with two independently controlled servo joints per leg:

**4 legs × 2 servo joints = 8 DOF**

The firmware identifies the servo channels using symbolic names such as:

- R1
- R2
- L1
- L2
- R3
- R4
- L3
- L4

This makes the movement functions easier to understand and modify.

---

## ⚙️ Hardware Components

| Component | Specification | Quantity | Function |
|---|---|---:|---|
| ESP32-WROOM-32 | Dual-core MCU with Wi-Fi | 1 | Main controller |
| MG90S Servo Motor | Metal gear servo | 8 | Leg/joint movement |
| SSD1306 OLED | 0.96", 128×64 | 1 | Facial expressions/status |
| Buck Converter | 5V, 3A | 1 | Regulated power |
| 10440 Li-ion Battery | Rechargeable | 2 | Power source |
| Battery Holder | 2-cell holder | 1 | Battery mounting |
| Rocker Switch | ON/OFF | 1 | Main power control |
| USB Data Cable | Micro USB | 1 | Programming/debugging |
| Prototype Board | PCB | 1 | Circuit assembly |
| PLA Filament | 3D printing | — | Mechanical body |
| Wires | 22 AWG / 30 AWG | — | Electrical connections |
| M2/M2.5 Screws | Mounting hardware | — | Mechanical assembly |

The report estimates the overall project cost at approximately **BDT 7,200**.

---

## 🔌 Power System

The robot uses two 10440 Li-ion batteries as the power source.

The battery supply is passed through a **5V, 3A buck converter** to provide regulated power for the ESP32 and servo system.

```text
10440 Li-ion Batteries
          │
          ▼
     Rocker Switch
          │
          ▼
    5V Buck Converter
          │
       ┌──┴──┐
       ▼     ▼
     ESP32  Servos
```

Proper power distribution and cable management are important because multiple servo motors can draw significant current during movement.

---

## 📡 Wireless Control

The ESP32 is configured to create its own Wi-Fi Access Point.

The report uses:

```text
SSID: Sesame-Controller
Password: 12345678
```

After powering the robot:

1. ESP32 starts.
2. ESP32 creates its own Wi-Fi network.
3. User connects a smartphone/computer to the robot's Wi-Fi.
4. User opens the ESP32-hosted web controller.
5. A movement command is selected.
6. The ESP32 receives the command.
7. The corresponding motion sequence is executed.

No external Wi-Fi router is required for the documented access-point mode.

---

## 🌐 Web Controller

The ESP32 runs a web server on HTTP port 80.

Important routes documented in the project include:

```text
/
 /cmd
 /getSettings
 /setSettings
 /api/status
 /api/command
```

The web interface is responsible for sending movement commands to the ESP32.

The command is stored internally and processed by the main program rather than directly controlling individual servo angles.

---

## 🚶 Motion Control

The robot uses predefined servo-angle sequences for different movements.

Documented motion functions include:

```text
runWalkPose()
runWalkBackward()
runTurnLeft()
runTurnRight()
runStandPose()
runWavePose()
runDancePose()
runPushupPose()
runBowPose()
runCrabPose()
```

The ESP32 executes these sequences by changing the angular positions of the eight servo motors in a coordinated order.

The movement system also supports interruption of continuous commands through command-state checking.

---

## 🎯 Servo Control

The firmware configures the servo motors at:

```text
Frequency: 50 Hz
Minimum pulse width: ≈732 µs
Maximum pulse width: ≈2929 µs
```

Servo position commands are constrained to the normal:

```text
0° – 180°
```

The firmware also uses **servo sub-trim values** to compensate for small mechanical alignment differences between individual servos.

This helps improve synchronization between the four legs.

---

## 😊 OLED Facial Display

A **128×64 SSD1306 OLED** is used for interactive facial expressions.

The documented I²C configuration is:

```text
SDA → GPIO 21
SCL → GPIO 22
I²C Address → 0x3C
```

Facial expressions are stored as bitmap frames.

The firmware can display different expressions for activities such as:

- Idle
- Walking
- Dancing
- Resting
- Blinking
- Other gestures

Multiple bitmap frames are displayed sequentially to create facial animation.

---

## 👀 Idle and Blink Animation

When the robot is idle, an idle facial animation is displayed.

The firmware can schedule a blink at a random interval of approximately **3–7 seconds**, producing a more natural interactive behavior.

---

## 💻 Software & Libraries

The project is developed using the **Arduino IDE**.

The report documents the use of libraries including:

```cpp
#include <DNSServer.h>
#include <ESPmDNS.h>
#include <Wire.h>
#include <ESP32Servo.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include <WiFi.h>
#include <WebServer.h>
```

Project-specific header files include:

```cpp
#include "face-bitmaps.h"
#include "movement-sequences.h"
#include "captive-portal.h"
```

These modules separate facial animation, movement sequences, and captive-portal functionality from the main firmware.

---

## 🔄 Overall Software Operation

```text
Power ON
   ↓
ESP32 Initialization
   ↓
Initialize OLED & Servo Motors
   ↓
Create Wi-Fi Access Point
   ↓
Start DNS & Web Server
   ↓
User Connects to Robot Wi-Fi
   ↓
Open Web Controller
   ↓
Select Movement
   ↓
Command Received by ESP32
   ↓
Select Predefined Motion Function
   ↓
Execute Servo Angle Sequence
   ↓
Robot Movement
   ↓
Update OLED Facial Animation
   ↓
Wait for Next Command
```

---

## 🖨️ Mechanical Design / CAD

The robot's mechanical/CAD structure was taken from the **Sesame Robot** project by **Dorian Borian**.

Official repository:

https://github.com/dorianborian/sesame-robot

Official CAD directory:

https://github.com/dorianborian/sesame-robot/tree/main/hardware/cad

The source repository contains the following CAD files:

```text
Sesame-ESP32-v122.f3z
Sesame-ESP32-v122.step
```

The mechanical structure is therefore based on the Sesame Robot CAD design, while this project focuses on its own **ESP32-based implementation, electronics integration, firmware, wireless control, motion sequences, OLED interaction, and academic documentation**.

---

## 📚 Project Development Methodology

The documented development process includes:

1. System study
2. Hardware component selection
3. Mechanical/CAD preparation
4. 3D printing using PLA
5. Electronic circuit integration
6. ESP32 firmware development
7. Wi-Fi control implementation
8. Servo calibration
9. OLED animation integration
10. Motion testing
11. Performance evaluation
12. Final documentation

---

## 🧪 Testing & Results

The report states that the completed robot was tested for:

- Servo operation
- Four-leg coordinated movement
- Wireless Wi-Fi control
- OLED facial animation
- Power-system stability
- Predefined motion sequences
- Overall system performance

Documented movements such as walking, waving, dancing, pointing, and resting were successfully demonstrated during testing.

The report concludes that the system achieved its intended objectives under normal working conditions.

---

## ⚠️ Current Limitations

The current implementation has several limitations:

- Motion is based on predefined sequences.
- No autonomous navigation is implemented.
- No obstacle avoidance is currently implemented.
- No computer vision system is included.
- No voice recognition is included.
- No AI-based decision-making is included.
- Battery operating time is limited.
- MG90S servos limit payload capacity.
- The robot is mainly intended for indoor educational/research use.
- Performance may be limited on rough or uneven terrain.

---

## 🚀 Future Improvements

Potential future enhancements include:

- 🤖 Artificial Intelligence
- 👁️ Computer Vision
- 🎤 Voice Recognition
- 📡 IoT connectivity
- 🧭 Autonomous navigation
- 🚧 Obstacle detection and avoidance
- 📷 Camera integration
- 📏 Ultrasonic/LiDAR-based sensing
- 🔋 Higher-capacity battery system
- ⚙️ Higher-torque servo motors
- 🗣️ Voice-controlled interaction
- 🐍 Python-based external control
- ☁️ Cloud-connected robotic applications

---

## 📁 Repository Structure

A recommended GitHub repository structure is:

```text
ESP32-Based-Interactive-Quadruped/
│
├── CAD_Source/
│   └── README.md
│
├── Firmware/
│   ├── main/
│   ├── face-bitmaps.h
│   ├── movement-sequences.h
│   └── captive-portal.h
│
├── Hardware/
│   ├── Circuit_Diagram/
│   └── Wiring/
│
├── Figures/
│
├── Documentation/
│   └── capstone_report.pdf
│
└── README.md
```

> The actual firmware/CAD binaries should only be placed in the repository when the corresponding files are available and their redistribution terms are satisfied.

---

## 📖 Reference

### Sesame Robot

Dorian Borian, **Sesame Robot — An open and affordable mini quadruped robot based on ESP32.**

GitHub:
https://github.com/dorianborian/sesame-robot

The Sesame Robot project is used as the mechanical/CAD source/reference for this implementation.

---

## 👨‍💻 Author

**Shahziar Karim Safit**  
Roll: **2001074**  
Department of Electrical & Electronic Engineering  
Rajshahi University of Engineering & Technology (RUET)

### Project Supervisor

**Dr. Ajay Krishno Sarkar**  
Professor  
Department of Electrical & Electronic Engineering  
Rajshahi University of Engineering & Technology

---

## 📄 Project Report

The complete project report is available in:

```text
Documentation/capstone_report.pdf
```

Project title:

**ESP32 Based Interactive Quadruped Robot with Wireless Motion Control**

---

## ⭐ Project Highlights

This project demonstrates the integration of:

**Embedded Systems + Robotics + Servo Control + Wi-Fi Communication + Web Control + OLED Animation + 3D-Printed Mechanical Design**

into a single low-cost interactive quadruped robotic platform.
