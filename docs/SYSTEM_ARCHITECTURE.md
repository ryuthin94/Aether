# System Architecture

> Aether – Smart Air Quality Badge

**Document Version:** 1.0  
**Status:** Draft  
**Last Updated:** June 2026

---

# 1. Overview

Aether is designed using a layered architecture that separates hardware, firmware, communication, mobile application, cloud backend, and data storage.

This modular approach improves maintainability, scalability, and future expansion.

---

# 2. High-Level Architecture

```
                +----------------------+
                |     User Interface   |
                |    Flutter Mobile    |
                +----------+-----------+
                           |
                     Bluetooth LE
                           |
                +----------v-----------+
                |    ESP32-S3 Badge    |
                |  Firmware + Sensors  |
                +----------+-----------+
                           |
                    Sensor Interfaces
                           |
      +---------+----------+-----------+
      |         |                      |
 PM2.5 Sensor  BME280         Battery Monitor
      |         |                      |
      +---------+----------------------+

                           |
                           |
                    Internet (via Phone)
                           |
                +----------v-----------+
                |     Firebase Cloud   |
                +----------+-----------+
                           |
                     Cloud Firestore
```

---

# 3. Layered Architecture

```
Application Layer
│
├── Flutter UI
├── Graphs
├── Notifications
└── Settings

──────────────────────────

Communication Layer
│
├── Bluetooth LE
├── JSON Encoding
└── Device Discovery

──────────────────────────

Firmware Layer
│
├── Sensor Drivers
├── AQI Calculation
├── Data Buffer
├── BLE Service
└── Power Management

──────────────────────────

Hardware Layer
│
├── ESP32-S3
├── PM Sensor
├── BME280
├── Battery
└── RGB LED
```

---

# 4. Hardware Architecture

## Microcontroller

ESP32-S3

Responsibilities:

- Read sensors
- Calculate AQI
- Manage BLE
- Store temporary measurements
- Monitor battery
- Control LED

---

## Sensors

### PM2.5

Primary environmental sensor.

Measures:

- PM1.0
- PM2.5
- PM10

---

### Temperature & Humidity

Provides:

- Ambient temperature
- Relative humidity

Also used for future sensor compensation.

---

### Battery Monitor

Measures:

- Battery voltage
- Estimated battery percentage

---

# 5. Firmware Architecture

```
main()

│

├── Sensor Manager

├── AQI Calculator

├── Battery Manager

├── BLE Manager

├── Storage Manager

└── LED Manager
```

Each module should be independent.

---

## Sensor Manager

Responsibilities:

- Initialize sensors
- Read measurements
- Validate values
- Detect sensor errors

---

## AQI Calculator

Responsibilities:

- Convert PM2.5 to AQI
- Assign AQI category
- Provide LED color

---

## BLE Manager

Responsibilities:

- Advertising
- Pairing
- Reconnection
- Data transfer

---

## Storage Manager

Responsibilities:

- Circular buffer
- Timestamp records
- Queue uploads

---

## LED Manager

Responsibilities:

Display status using RGB LED.

---

# 6. Bluetooth Architecture

BLE is used exclusively between the badge and the mobile application.

```
ESP32 Badge

↓

Advertising

↓

Flutter scans

↓

Pair

↓

Discover Services

↓

Subscribe

↓

Receive Notifications

↓

Store Data
```

---

## Proposed BLE Services

### Device Information

Contains:

- Device Name
- Firmware Version
- Hardware Revision

---

### Environmental Service

Characteristics:

- PM2.5
- Temperature
- Humidity
- AQI

---

### Battery Service

Characteristics:

- Battery %
- Charging Status

---

### Control Service

Allows:

- Change sampling interval
- Sync time
- Restart device
- Future OTA

---

# 7. Mobile Architecture

Flutter Application

```
Presentation Layer

↓

State Management

↓

BLE Repository

↓

Cloud Repository

↓

Firebase
```

Suggested folder structure:

```

lib/

├── models/

├── services/

├── screens/

├── widgets/

├── repositories/

├── providers/

└── utils/
```

---

# 8. Cloud Architecture

Firebase Services

```
Flutter

↓

Authentication

↓

Firestore

↓

Cloud Storage (future)

↓

Cloud Functions (future)
```

---

## Firestore Collections

```
users/

devices/

measurements/

settings/

firmware/
```

Each measurement contains:

```
timestamp

pm25

temperature

humidity

aqi

battery

firmwareVersion
```

---

# 9. Data Flow

## Live Mode

```
Sensor

↓

ESP32

↓

BLE

↓

Flutter

↓

Screen
```

---

## Cloud Sync

```
Sensor

↓

ESP32

↓

Flutter

↓

Firestore
```

---

## Offline Mode

```
Sensor

↓

ESP32 Buffer

↓

Reconnect

↓

Flutter

↓

Firestore
```

---

# 10. Power Architecture

```
USB-C

↓

Charging IC

↓

LiPo Battery

↓

Voltage Regulation

↓

ESP32

↓

Sensors
```

---

## Power Saving Strategy

The firmware should:

- Sleep between measurements
- Reduce BLE advertising when disconnected
- Disable unused peripherals
- Lower CPU frequency when idle

---

# 11. Security Architecture

Authentication

↓

Firebase Authentication

↓

Encrypted HTTPS

↓

Firestore Security Rules

↓

Authenticated User

BLE:

- Secure pairing
- Device authentication
- Unique device identifier

---

# 12. Error Handling

Firmware should detect:

- Sensor failure
- BLE disconnect
- Battery low
- Invalid measurements
- Flash storage full

Application should display clear error messages.

---

# 13. Scalability

Future sensors should connect through the Sensor Manager.

Examples:

- CO₂
- TVOC
- UV
- Noise
- Light

Adding new sensors should not require rewriting the mobile app architecture.

---

# 14. Future Architecture

Future versions may include:

- OTA firmware updates
- AI prediction service
- School dashboard
- Web portal
- Multi-user deployments
- Public environmental API

---

# 15. Design Principles

The architecture is designed to be:

- Modular
- Maintainable
- Scalable
- Testable
- Low Power
- Privacy Focused
- Offline Capable

---

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | June 2026 | Initial System Architecture |
