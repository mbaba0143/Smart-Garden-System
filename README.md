# 🌱 Smart Garden System using Raspberry Pi

An IoT-based Smart Garden System built on **Raspberry Pi** that automates plant watering using soil moisture sensors and provides real-time environmental monitoring. The system helps maintain healthy plants with minimal human intervention.

## 📌 Features

- 🌧️ Automatically waters plants based on soil moisture levels
- 🌡️ Monitors temperature and humidity (DHT11)
- 📶 Sends data to the cloud using ThingSpeak or Blynk
- 📱 Access real-time readings on your mobile
- 💧 Reduces water wastage with precision irrigation

## 🔧 Hardware Components

- ✅ Raspberry Pi 4B
- ✅ Soil Moisture Sensor
- ✅ DHT11 Sensor (Temperature + Humidity)
- ✅ Relay Module (to control pump)
- ✅ Mini Water Pump (DC)
- ✅ Jumper Wires, Breadboard
- ✅ Power Supply

---

## 💻 Software & Tools

- Raspberry Pi OS (Lite or Full)
- Python 3 (main programming language)
- Libraries: `Adafruit_DHT`, `RPi.GPIO`, `requests`
- ThingSpeak / Blynk (for IoT Dashboard)
- VNC / SSH (for remote access)

---

## 🧠 System Workflow

1. Raspberry Pi reads soil moisture and DHT11 values
2. If soil is dry → relay turns on water pump
3. All sensor data is sent to ThingSpeak for live monitoring
4. Pump stops when moisture is sufficient

---



