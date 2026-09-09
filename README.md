# ESP32 Based Interactive Quadruped Robot with Wireless Motion Control

## Project Overview

This project is an ESP32-based interactive quadruped robot with:
- 8 MG90S servo motors (8-DOF)
- SSD1306 0.96-inch 128×64 OLED display
- Wi-Fi wireless motion control
- Predefined walking and interactive movements
- 3D-printed PLA mechanical body

## CAD / Mechanical Design

The mechanical/CAD design of this project was taken from the **Dorian Borian Sesame Robot** project.

The official Sesame repository provides CAD designs and identifies the robot as an ESP32-based quadruped platform.

Official repository:
https://github.com/dorianborian/sesame-robot

CAD source:
https://github.com/dorianborian/sesame-robot/tree/main/hardware/cad

The specific CAD files referenced by the source repository are:
- Sesame-ESP32-v122.f3z
- Sesame-ESP32-v122.step

## Our Implementation

The project report documents an implementation using:
- ESP32-WROOM-32
- 8 × MG90S servo motors
- SSD1306 OLED
- 5V 3A buck converter
- 2 × 10440 Li-ion batteries
- Wi-Fi access-point control
- Browser-based web controller

The project therefore uses the Sesame mechanical/CAD platform while the electronics, firmware configuration, documentation, and implementation are specific to this project.

## Included

- `Documentation/capstone_report.pdf` — corrected 28-page project report
- `Figures/` — figures extracted from the report
- `CAD_Source/README.md` — exact official CAD source and filenames

## Important

The actual CAD binary files are not duplicated in this ZIP because they could not be downloaded through the available GitHub file connector. Use the official CAD source link above to obtain the original `.f3z` and `.step` files.

No separate LICENSE file has been added to this ZIP.
