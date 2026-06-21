# Component Decisions

> Aether – Smart Air Quality Badge

**Document Version:** 1.0  
**Status:** Living Document  
**Last Updated:** June 2026

---

# Purpose

This document records major hardware component decisions made during the development of Aether.

For each decision, alternatives, trade-offs, and reasoning are documented to ensure future maintainability and prevent repeated evaluation of previously resolved questions.

---

# Decision Status

| Status | Meaning |
|---------|---------|
| Proposed | Under evaluation |
| Selected | Chosen for current revision |
| Deprecated | Previously selected but replaced |

---

# CD-001 — Main Microcontroller

Status

**Selected**

## Requirement

The MCU must provide:

- Bluetooth Low Energy
- Low-power operation
- Sufficient RAM
- OTA support
- Native USB
- Strong development ecosystem

## Candidates

| MCU | Pros | Cons |
|------|------|------|
| ESP32-C3 | Cheap, low power | Less RAM |
| ESP32-S3 | Fast, USB, BLE | Slightly higher cost |
| nRF52840 | Excellent BLE | Smaller ecosystem |
| Raspberry Pi Pico W | Easy to use | Weaker BLE ecosystem |

## Decision

ESP32-S3-WROOM-1

## Rationale

Provides the best balance of processing power, Bluetooth support, memory, and community resources.

---

# CD-002 — PM2.5 Sensor

Status

**Proposed**

## Candidates

### Sensirion SPS30

Pros

- Excellent accuracy
- Long lifetime
- Self-cleaning fan
- Stable readings

Cons

- Higher cost

---

### Plantower PMS7003

Pros

- Low cost
- Popular
- Easy to source

Cons

- More humidity sensitive
- Less stable over time

---

## Decision

Tentatively:

Sensirion SPS30

## Reason

Accuracy and reliability are prioritized over cost for the initial prototype.

---

# CD-003 — Temperature & Humidity Sensor

Status

Selected

Candidates

- DHT22
- SHT31
- BME280

Decision

Bosch BME280

Reason

- Higher precision
- Lower power
- Includes pressure sensor
- Mature software libraries

---

# CD-004 — Battery Capacity

Status

Proposed

Options

1000mAh

Pros

- Smaller

Cons

- Shorter runtime

---

1500mAh

Pros

- All-day battery

Cons

- Slightly larger

---

2000mAh

Pros

- Long runtime

Cons

- Heavy

Decision

1500mAh

Reason

Best compromise between size and endurance.

---

# CD-005 — Charging Interface

Status

Selected

Candidates

- Micro USB
- USB-C

Decision

USB Type-C

Reason

Industry standard

Reversible connector

Future-proof

---

# CD-006 — RGB Indicator

Status

Selected

Candidates

- Single LED
- RGB LED
- OLED Only

Decision

RGB LED

Reason

Provides immediate visual feedback while consuming less power than an always-on display.

---

# CD-007 — Display

Status

Open

Options

No Display

Pros

- Smaller
- Lower power

Cons

- Phone required

---

OLED

Pros

- Standalone operation

Cons

- Higher power
- Larger enclosure

Current Decision

Optional

---

# CD-008 — PCB Strategy

Status

Selected

Revision 1

Development board

Revision 2

Custom PCB

Reason

Reduces development risk.

---

# CD-009 — Enclosure

Status

Open

Prototype

3D Printed PLA

Future

Injection molded ABS

---

# CD-010 — Firmware Framework

Status

Selected

Decision

ESP-IDF

Reason

Professional framework

OTA support

Long-term maintainability

---

# Future Decisions

Upcoming engineering decisions include:

- Final enclosure dimensions
- Waterproofing
- Manufacturing process
- RF antenna placement
- PCB stack-up
- Certification strategy

---

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | June 2026 | Initial component decisions |
