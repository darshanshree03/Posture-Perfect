# Posture-Prefect 🎧

A wearable posture monitoring neckband that looks like a regular audio device but continuously tracks your posture using an IMU and flex sensor — alerting you through audio feedback and a companion Android app when poor posture is detected.

> **Status:** PCB design complete (Gerber ready). Firmware and Android app in active development.

---

## The Problem

IT professionals and desk workers who sit for long hours frequently develop back pain and posture-related health issues. Most posture correction solutions are either too obvious to wear in public or too passive to be effective.

## Our Solution

A neckband that blends in as a regular audio accessory. It uses a gyroscope and flex sensor to continuously monitor neck and back posture. When slouching or poor posture is detected, it delivers real-time audio alerts through the built-in speaker and push notifications via the companion app.

---

## System Architecture

```
[BMI160 IMU] ──┐
               ├──► [ESP32-PICO-D4] ──► Bluetooth ──► [Android App] ──► Firebase
[Flex Sensor] ─┘         │
                          └──► [MAX9B357A Audio Amp] ──► Speaker (Voice Alert)
```

---

## Hardware

### Components
| Component | Function |
|---|---|
| ESP32-PICO-D4 | Main MCU — processing, Bluetooth, Firebase sync |
| BMI160 IMU | Gyroscope + accelerometer for neck angle detection |
| Resistive Flex Sensor | Detects spinal bending/slouching |
| MAX9B357A | Class D audio amplifier for voice alerts |
| USB-C | Charging interface |

### PCB Design
The hardware is split into two custom PCBs designed in KiCad:

**Neckband PCB** — Main control board
- ESP32-PICO-D4, tactile buttons (SW1, SW2, SW3), USB-C charging, power management
- Slim vertical form factor to fit inside the neckband

**Earbud PCB** — Sensor board
- BMI160 IMU, MAX9B357A audio amp, flex sensor connector
- Compact L-shaped footprint

#### Neckband PCB — 3D View

| Front | Back |
|---|---|
| ![Neckband PCB Front](hardware/Neckband_pcb3DFront.png) | ![Neckband PCB Back](hardware/Neckband_pcb3DBack.png) |

#### Earbud PCB — 3D View
![Earbud PCB](hardware/earbud_pcb3D.png)

> ⚠️ PCB routing is currently in progress (94 unrouted connections on the neckband board). Gerber files will be updated once routing is complete.

---

## Software

### Firmware (ESP32)
- Reads BMI160 IMU data over I2C
- Reads flex sensor via ADC
- Posture detection logic with configurable thresholds
- Triggers audio alert via MAX9B357A when poor posture is detected
- Sends posture status to Android app via Bluetooth

### Android App (Android Studio)
- Receives real-time posture data from ESP32 over Bluetooth
- Displays current posture status
- Push notification alerts
- Syncs session data to Firebase

> App is functional for data display. Full notification and history features in progress.

---

## Tools Used

| Tool | Purpose |
|---|---|
| KiCad | PCB schematic and layout design |
| Android Studio | Companion app development |
| Firebase | Cloud database for posture session data |

---

## Demo

Demo video available in the `/demo` folder of this repository.

---

## Team

4-member project team:
- **PCB Design** — Shree Dharshan S, Harshinivarsa SK
- **Firmware & App** — Abishek M, Harini C

*Originally developed as a hackathon prototype. Currently being refined into a wearable product.*

---

## Project Status

- [x] Breadboard prototype (hackathon)
- [x] PCB schematic complete
- [x] PCB 3D layout complete
- [ ] PCB routing complete
- [ ] Gerber fabrication
- [ ] Firmware finalized
- [ ] Android app completed

