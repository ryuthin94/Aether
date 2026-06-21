# Product Requirements Document (PRD)

> Aether – Smart Air Quality Badge

**Document Version:** 1.0  
**Status:** Draft  
**Last Updated:** June 2026

---

# 1. Purpose

This document defines the functional and non-functional requirements for the Aether platform.

It serves as the primary engineering reference for firmware, mobile application, backend, and hardware development.

---

# 2. Product Summary

Aether is a wearable IoT device that continuously monitors environmental conditions and communicates with a companion mobile application using Bluetooth Low Energy (BLE).

The application stores historical measurements locally and in the cloud while providing alerts, analytics, and device management.

---

# 3. Stakeholders

| Role | Responsibility |
|------|----------------|
| End User | Uses the badge and mobile application |
| Firmware Developer | ESP32 firmware |
| Mobile Developer | Flutter application |
| Backend Developer | Firebase backend |
| Hardware Engineer | Electronics and PCB |
| Tester | Validation and testing |

---

# 4. Functional Requirements

## FR-001 Device Boot

Priority: High

The badge shall boot within **5 seconds** after power-on.

---

## FR-002 Air Quality Measurement

Priority: Critical

The device shall measure:

- PM2.5 concentration
- Temperature
- Humidity

Sampling interval shall be configurable.

Default interval:

```
Every 5 seconds
```

---

## FR-003 AQI Calculation

Priority: Critical

The firmware shall convert PM2.5 concentration into an Air Quality Index (AQI) using a configurable calculation method.

Future firmware versions should support multiple AQI standards.

---

## FR-004 Bluetooth Connection

Priority: Critical

The badge shall communicate with the mobile application using Bluetooth Low Energy.

Requirements:

- Automatic reconnection
- Pairing support
- Device discovery
- Signal strength reporting

---

## FR-005 Live Data Streaming

Priority: High

The badge shall stream sensor data to the mobile application while connected.

Latency target:

```
< 1 second
```

---

## FR-006 Local Buffering

Priority: High

If Bluetooth is unavailable, the badge shall store measurements locally.

Requirements:

- Circular buffer
- Timestamp every record
- Automatic upload after reconnection

---

## FR-007 Battery Monitoring

Priority: High

The badge shall monitor battery voltage.

Battery percentage shall be reported to the mobile application.

Low battery threshold:

```
20%
```

Critical battery threshold:

```
10%
```

---

## FR-008 RGB Status Indicator

Priority: Medium

LED colors:

| AQI | Color |
|------|-------|
| Good | Green |
| Moderate | Yellow |
| Unhealthy for Sensitive Groups | Orange |
| Unhealthy | Red |
| Pairing | Blue |
| Firmware Update | Purple |

---

## FR-009 Mobile Dashboard

Priority: Critical

The Flutter application shall display:

- Current AQI
- PM2.5
- Temperature
- Humidity
- Battery
- Connection status
- Last update time

---

## FR-010 Historical Data

Priority: High

Users shall be able to view:

- Hourly graph
- Daily graph
- Weekly graph
- Monthly graph

---

## FR-011 Notifications

Priority: High

The application shall notify users when:

- AQI exceeds threshold
- Battery is low
- Device disconnects
- Device reconnects

---

## FR-012 Cloud Synchronization

Priority: Medium

Measurements shall synchronize automatically when internet connectivity becomes available.

---

## FR-013 User Authentication

Priority: Medium

Users shall authenticate using Firebase Authentication.

Supported methods:

- Email & Password

Future:

- Google Sign-In
- Apple Sign-In

---

## FR-014 Multiple Devices

Priority: Low

One account may own multiple badges.

Each badge shall have:

- Name
- Device ID
- Firmware Version

---

## FR-015 Settings

Users shall configure:

- Sampling interval
- Notification thresholds
- Display units
- Dark mode

---

# 5. Non-Functional Requirements

## Performance

- BLE latency < 1 second
- App startup < 2 seconds
- Cloud sync < 5 seconds
- Sensor update every 5 seconds

---

## Reliability

The system shall:

- Recover automatically from BLE disconnects
- Prevent data loss
- Continue logging without internet

---

## Battery

Target runtime:

```
12+ hours
```

Charging:

```
USB-C
```

Maximum charging time:

```
< 2 hours
```

---

## Security

- Authentication required
- HTTPS communication
- Secure BLE pairing
- Encrypted cloud communication

---

## Maintainability

The software shall support:

- Modular firmware
- OTA-ready partition layout
- Versioned APIs
- Versioned database schema

---

## Scalability

Future sensors should require minimal firmware modifications.

---

# 6. Hardware Requirements

Minimum MCU:

```
ESP32-S3
```

Required peripherals:

- BLE 5.0
- I²C
- UART
- ADC

Required sensors:

- PM2.5
- Temperature
- Humidity

Power source:

```
Rechargeable Li-Po
```

---

# 7. Mobile Requirements

Platform:

```
Android
```

Future:

```
iOS
```

Framework:

```
Flutter
```

Minimum Android Version:

```
Android 10
```

---

# 8. Backend Requirements

Platform:

```
Firebase
```

Services:

- Authentication
- Firestore
- Cloud Storage (future)
- Cloud Functions (future)
- Analytics (future)

---

# 9. User Experience Requirements

The application shall:

- Display current AQI immediately after connection.
- Minimize user interaction.
- Use clear color coding.
- Support dark mode.
- Provide smooth animations.

---

# 10. Acceptance Criteria

The MVP is considered complete when:

- ✅ Badge measures PM2.5
- ✅ Badge measures temperature
- ✅ Badge measures humidity
- ✅ BLE connection is stable
- ✅ Flutter app displays live data
- ✅ Historical data is stored
- ✅ Battery percentage is displayed
- ✅ Notifications function correctly
- ✅ Firebase synchronization works
- ✅ Documentation is complete

---

# 11. Future Requirements

Potential future capabilities include:

- CO₂ sensing
- TVOC sensing
- GPS logging
- Environmental heatmaps
- AI prediction
- OTA firmware updates
- Apple Watch integration
- Wear OS support
- Web dashboard
- Classroom analytics

---

# 12. Out of Scope (Version 1)

The following features are intentionally excluded from the initial release:

- Wi-Fi operation
- Cellular connectivity
- Voice assistant integration
- Machine learning on-device
- Custom ASIC hardware
- Waterproof enclosure certification
- Medical-grade certification

---

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | June 2026 | Initial Product Requirements Document |
