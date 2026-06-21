# Aether

> Personalized Environmental Monitoring, Worn Every Day.

**Document Version:** 1.0  
**Status:** Draft  
**Last Updated:** June 2026

---

# 1. Introduction

Aether is an open-source wearable Internet of Things (IoT) platform designed to provide personalized environmental monitoring through a compact smart badge, companion mobile application, and cloud infrastructure.

Unlike traditional air quality monitoring stations that provide regional measurements, Aether measures the air quality surrounding an individual in real time. By collecting localized environmental data, Aether enables users to better understand the conditions they experience throughout the day and make informed decisions regarding their health and activities.

The project combines embedded systems, wireless communication, cloud computing, and mobile application development into a single integrated platform.

---

# 2. Vision

To create an affordable, scalable, and open environmental monitoring platform that empowers individuals, schools, and communities with accurate, real-time air quality information.

Aether is intended to evolve beyond a personal wearable into a distributed environmental sensing network capable of generating hyperlocal environmental intelligence.

---

# 3. Mission

Build an engineering platform that:

- Continuously measures environmental conditions.
- Provides meaningful insights instead of raw sensor values.
- Encourages environmental awareness.
- Demonstrates modern embedded system design.
- Serves as an educational open-source project.

---

# 4. Problem Statement

Air quality significantly affects human health, yet most available monitoring systems only report measurements from fixed monitoring stations.

These stations often:

- represent large geographic regions
- cannot measure indoor environments
- cannot capture hyperlocal pollution sources
- provide little personalization

As a result, users rarely know the quality of the air they are personally breathing.

Aether addresses this problem by placing a compact monitoring device directly on the user.

---

# 5. Objectives

The primary objectives of Aether are:

- Measure PM2.5 concentrations in real time.
- Measure temperature and humidity.
- Display live environmental information through a mobile application.
- Store historical environmental data.
- Generate notifications when unhealthy conditions are detected.
- Provide a scalable platform for future environmental sensing.

---

# 6. Target Users

Aether is designed for:

- Students
- Teachers
- Office workers
- Cyclists
- Runners
- Outdoor enthusiasts
- Individuals with respiratory conditions
- Researchers
- Schools

---

# 7. Project Scope

## Included

- Wearable smart badge
- Bluetooth Low Energy communication
- Flutter mobile application
- Firebase backend
- Historical data storage
- Battery monitoring
- AQI calculation
- Notification system

## Future Scope

- CO₂ monitoring
- TVOC sensing
- UV monitoring
- GPS integration
- AI-powered environmental insights
- OTA firmware updates
- School dashboard
- Community environmental maps

---

# 8. Key Features

## Smart Badge

- Real-time PM2.5 sensing
- Temperature monitoring
- Humidity monitoring
- RGB status LED
- Rechargeable battery
- Bluetooth Low Energy
- Low-power operation

---

## Mobile Application

- Live AQI dashboard
- Device management
- Historical graphs
- Push notifications
- Battery monitoring
- Settings
- Firmware information

---

## Cloud Platform

- Secure authentication
- Cloud synchronization
- Historical analytics
- Multi-device support
- Data export
- Environmental dashboard

---

# 9. Technology Stack

## Firmware

- ESP32-S3
- ESP-IDF
- C++

## Mobile

- Flutter
- Dart

## Backend

- Firebase

## Database

- Cloud Firestore

## Authentication

- Firebase Authentication

## Version Control

- Git
- GitHub

---

# 10. Design Principles

The development of Aether follows several core principles.

### Simplicity

The user should understand the air quality with minimal interaction.

### Reliability

Measurements should remain consistent and recover gracefully from connection loss.

### Privacy

Users own their personal environmental data.

### Scalability

The system should support additional sensors without major redesign.

### Modularity

Hardware and software components should be replaceable and independently maintainable.

---

# 11. Success Criteria

The initial release will be considered successful if it can:

- Measure PM2.5 continuously.
- Maintain a stable BLE connection.
- Synchronize data with the mobile application.
- Store historical measurements.
- Operate on battery power for an entire school day.
- Display AQI correctly.
- Notify users when air quality becomes unhealthy.

---

# 12. Long-Term Vision

The long-term vision of Aether extends beyond a single wearable device.

As additional users adopt the platform, anonymous environmental data may be aggregated to create high-resolution environmental maps for schools, campuses, neighborhoods, and cities.

The project aims to demonstrate how affordable open-source hardware can contribute to healthier communities and smarter environmental decision-making.

---

# 13. Repository Structure

```
Aether/
├── docs/
├── firmware/
├── mobile/
├── backend/
├── hardware/
├── pcb/
├── enclosure/
├── assets/
└── scripts/
```

---

# 14. License

This project is released under the MIT License unless otherwise specified.

---

# 15. Authors

Developed by:

**Syntax**

Project Name:

**Aether**

---

# Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | June 2026 | Initial project overview |
