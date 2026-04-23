## User‑Specific‑Song‑Response

An embedded system that detects nearby BLE devices, identifies users by UUID, and triggers personalized audio playback through a JBL Bluetooth speaker. The system uses two ESP32 modules and an STM32 to separate BLE scanning, decision logic, and audio streaming for maximum reliability.

## Overview

When a user enters the room with a BLE beacon or smartphone, the system detects their UUID, determines which audio track belongs to them, and plays their assigned WAV file wirelessly over Bluetooth A2DP.
The design splits responsibilities across three microcontrollers:

ESP32‑A (DevKit): BLE scanner

STM32: UUID → track number mapping

ESP32‑B: Audio playback engine (WAV → A2DP)

This modular approach allows better stability, reduces timing conflicts, and keeps each device focused on a single task given the ram restrictions inside ESP32

## System Architecture

ESP32‑A — BLE Scanner -
Continuously scans for BLE beacons / phone advertisements

Extracts UUID or MAC address

Sends UUID to STM32 over UART

STM32 — Decision Engine -
Receives UUID from ESP32‑A

Looks up UUID in its internal song table

Determines the correct track number and sends track number to ESP32‑B

ESP32‑B — Audio Engine -
Receives track number from STM32 and reads the corresponding WAV file from the microSD card 
Streams WAV audio to a JBL speaker using Bluetooth A2DP

## Full System Flow

<img width="327" height="426" alt="image" src="https://github.com/user-attachments/assets/990f32d1-e23a-4d74-b0a3-652d9bbc679d" />
<img width="391" height="264" alt="image" src="https://github.com/user-attachments/assets/e19d6fbe-5031-4693-806b-d204801286e7" />
<img width="390" height="331" alt="image" src="https://github.com/user-attachments/assets/1878b1e8-61cc-48f7-a6b6-9b2a8154bdf1" />


## Authors

Davonta Dunn & Caleb Friesen

University of North Texas

Spring 26 Embedded Systems Project
