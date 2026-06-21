# Hardware Specification

> Aether – Smart Air Quality Badge

**Document Version:** 1.0  
**Status:** Draft  
**Last Updated:** June 2026

---

# 1. Purpose

This document defines the hardware architecture and component selection for the Aether Smart Air Quality Badge.

It serves as the primary reference for electronics design, PCB development, firmware implementation, enclosure design, and future hardware revisions.

---

# 2. Design Goals

The hardware platform shall be:

- Compact enough to wear comfortably
- Battery-powered for all-day operation
- Low-power
- Modular
- Easy to prototype
- Easy to manufacture
- Expandable for future sensors

---

# 3. System Overview

```
+-----------------------------------------+
|             Aether Badge                |
|                                         |
|  PM2.5 Sensor                           |
|  Temperature/Humidity Sensor            |
|          │                              |
|          ▼                              |
|      ESP32-S3 MCU                       |
|          │                              |
| ┌────────┼────────┐                     |
| │        │        │                     |
| BLE    RGB LED  Battery Monitor         |
| │                                   USB-C
| ▼                                      │
| Mobile App ←→ Firebase                 │
+-----------------------------------------+
```

---

# 4. Component Selection

| Component | Selected Part | Status |
|------------|---------------|--------|
| MCU | ESP32-S3-WROOM-1 | Selected |
| PM Sensor | Sensirion SPS30 *(Preferred)* | Candidate |
| Temperature & Humidity | Bosch BME280 | Selected |
| Battery | 3.7V LiPo 1500mAh | Selected |
| Charging IC | TP4056 (Prototype) | Selected |
| USB Connector | USB Type-C | Selected |
| RGB Indicator | WS2812B Mini | Selected |
| Push Button | 6×6 mm Tactile | Selected |
| Voltage Regulation | 3.3V LDO | TBD |
| Flash Memory | Built into ESP32 | Selected |

---

# 5. Microcontroller

## ESP32-S3-WROOM-1

### Reason for Selection

- Dual-core Xtensa LX7
- Bluetooth Low Energy 5.0
- Large Flash options
- Excellent community support
- Native USB
- Low power modes
- OTA capable
- Plenty of GPIO

---

## Responsibilities

The ESP32 shall:

- Read sensors
- Calculate AQI
- Manage Bluetooth
- Buffer measurements
- Monitor battery
- Control RGB LED
- Execute firmware updates (future)

---

# 6. Environmental Sensors

## PM2.5 Sensor

### Preferred

Sensirion SPS30

Advantages

- High accuracy
- Laser-based
- Long lifetime
- Automatic fan cleaning
- Better long-term stability

---

### Alternative

Plantower PMS7003

Advantages

- Lower cost
- Good documentation
- Easy to source

Disadvantages

- Lower long-term accuracy
- More affected by humidity

---

## Temperature & Humidity

Bosch BME280

Measures

- Temperature
- Humidity
- Atmospheric Pressure

Reasons

- Accurate
- Low power
- Small package
- Widely supported

---

# 7. Battery System

## Battery

Type

Rechargeable Lithium Polymer

Capacity

1500 mAh

Nominal Voltage

3.7V

Expected Runtime

> 12 hours

---

## Charging

USB Type-C

Prototype Charger

TP4056

Future PCB

Integrated USB-C charging circuit

---

## Protection

Battery protection circuit shall include

- Overcharge protection
- Over-discharge protection
- Short-circuit protection
- Thermal protection

---

# 8. User Interface Hardware

## RGB LED

Purpose

Quick status indication

| Status | Color |
|---------|--------|
| Good AQI | Green |
| Moderate | Yellow |
| Unhealthy | Orange |
| Hazardous | Red |
| Pairing | Blue |
| Charging | Cyan |
| Updating | Purple |
| Error | White |

---

## Push Button

Functions

Single Press

- Wake display
- Check battery

Double Press

- Show AQI

Long Press

- Enter pairing mode

Very Long Press

- Factory reset

---

# 9. Battery Monitoring

The ESP32 shall monitor battery voltage using an ADC through a resistor divider.

Measurements

- Voltage
- Estimated battery %
- Charging state

Low Battery Warning

20%

Critical Battery

10%

---

# 10. Communication Interfaces

## Bluetooth

Bluetooth Low Energy 5.0

Purpose

- Live data
- Configuration
- Firmware information
- Future OTA

---

## USB

USB Type-C

Purpose

- Charging
- Debugging
- Firmware flashing

---

# 11. Mechanical Design

Target Dimensions

Approximately

```
60 × 40 × 15 mm
```

Maximum Weight

```
70 g
```

Target Mounting

- Lanyard
- Shirt clip
- Backpack clip

Future

Magnetic attachment

---

# 12. Environmental Requirements

Operating Temperature

```
0–45°C
```

Storage Temperature

```
-20–60°C
```

Humidity

```
10–90%
```

Indoor and outdoor operation

---

# 13. Estimated Power Budget

| Component | Typical Current |
|------------|----------------|
| ESP32-S3 | 20–80 mA |
| SPS30 | ~60 mA |
| BME280 | <1 mA |
| RGB LED | 5–20 mA |
| Total (Typical) | ~90–150 mA |

Estimated Runtime

```
10–15 hours
```

(Target to improve with firmware optimization.)

---

# 14. PCB Design Goals

Revision 1

- Prototype using breakout modules
- Perfboard or breadboard

Revision 2

Custom PCB

Goals

- Two-layer PCB
- USB-C
- JST battery connector
- Programming header
- Test pads

Revision 3

Production PCB

- Smaller footprint
- Improved RF layout
- Better thermal management

---

# 15. Manufacturing Considerations

The hardware should be designed with:

- Standard SMD components
- Easily sourced parts
- Modular sensor replacement
- Low assembly complexity

---

# 16. Future Hardware Expansion

Reserved interfaces shall support

- CO₂ sensor
- TVOC sensor
- UV sensor
- Ambient light sensor
- Noise sensor
- GPS module
- Accelerometer

---

# 17. Open Decisions

The following items remain under evaluation:

- Final PM2.5 sensor selection
- Final battery capacity
- OLED display inclusion
- Waterproof enclosure
- Custom charging IC
- Wireless firmware update hardware validation

---

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | June 2026 | Initial hardware specification |
