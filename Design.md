# MOB Security System - Design Document

## Part 1: Visual Design System

### Overview
A marine safety dashboard with a dark, high-contrast design optimized for ship bridge environments. The design prioritizes instant readability with large typography, clear status indicators, and a nautical color palette. The interface is designed to allow ship officers to understand critical situations within 2 seconds.

Key characteristics:
- Dark mode first
- High visibility
- Marine aesthetic
- Mission-critical focus
- Responsive layout

---

## Part 2: Global Animations & Interactions
(unchanged – original content retained)

---

## Part 3: Content Sections
(unchanged – original content retained)

---

## Part 4: System Architecture & Data Flow  ✅ NEW

### High-Level Architecture


---

### System Components

**Wearable Device**
- ESP32 microcontroller
- MPU6050 (motion detection)
- GPS module (NEO-6M)
- Battery-powered wearable unit

**Communication**
- LoRa long-range communication
- Compact binary payloads (decoded server-side)

**Dashboard**
- Real-time telemetry display
- Interactive map
- Emergency alerts
- Event history logging

---

## Part 5: Alert & Event Logic  ✅ NEW

### Alert Types
- Man Overboard (Critical)
- GPS Fix Lost
- Low Signal Strength
- Speed Anomaly

### Man Overboard Trigger
A MOB alert is generated when:
- Fall detection flag is TRUE
- Sudden speed drop is observed
- No recovery movement detected

### Emergency Mode Behavior
- Alert banner turns RED
- Audio alarm is activated
- Map auto-centers on MOB location
- Alert persists until acknowledged

---

## Part 6: Real-Time Update Strategy  ✅ NEW

- Dashboard updates are **event-driven**
- Each received LoRa packet triggers UI updates
- Emergency state increases update frequency
- Offline state detected if packet timeout exceeds threshold

---

## Part 7: Telemetry & Payload Structure  ✅ NEW

### Core Fields
- Latitude / Longitude
- Speed / Course
- RSSI
- GPS Fix & Satellites
- Battery Voltage
- Packet Counter
- Fall Detection Flag

### Payload Design Philosophy
- No JSON transmitted over LoRa
- Compact byte-array payload
- Decoded into structured data before visualization

---

## Part 8: Data Storage & History  ✅ NEW

- All packets are timestamped
- Stored locally or server-side
- Filterable by date and status
- CSV export supported
- History capped to avoid overload

---

## Part 9: Power Optimization Strategy  ✅ NEW

- Deep sleep during idle state
- Adaptive transmit rate
- GPS enabled only during movement
- Emergency mode overrides power saving

---

## Part 10: Testing & Validation  ✅ NEW

| Scenario | Expected Result |
|--------|----------------|
| Walking | No alert |
| Jump | No alert |
| Fall | MOB alert |
| Signal loss | Warning |
| Battery low | Warning |

---

**End of Document**
