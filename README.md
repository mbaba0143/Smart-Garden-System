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



## Code (main.py)

python
import RPi.GPIO as GPIO
import Adafruit_DHT
import time
import requests

# Pins
DHT_PIN = 4
SOIL_PIN = 17
RELAY_PIN = 27

# Setup
GPIO.setmode(GPIO.BCM)
GPIO.setup(SOIL_PIN, GPIO.IN)
GPIO.setup(RELAY_PIN, GPIO.OUT)

DHT_SENSOR = Adafruit_DHT.DHT11

def read_soil():
    return GPIO.input(SOIL_PIN)  # 0 = wet, 1 = dry

def read_temp_humidity():
    humidity, temperature = Adafruit_DHT.read(DHT_SENSOR, DHT_PIN)
    return temperature, humidity

def send_to_thingspeak(temp, humidity, soil):
    api_key = "YOUR_THINGSPEAK_WRITE_API"
    url = f"https://api.thingspeak.com/update?api_key={api_key}&field1={temp}&field2={humidity}&field3={soil}"
    requests.get(url)

try:
    while True:
        soil = read_soil()
        temp, humidity = read_temp_humidity()

        print(f"Soil: {'Dry' if soil else 'Wet'}, Temp: {temp}, Humidity: {humidity}")
        
        # Watering logic
        if soil == 1:  # Dry
            GPIO.output(RELAY_PIN, GPIO.HIGH)
            print("Pump ON")
        else:
            GPIO.output(RELAY_PIN, GPIO.LOW)
            print("Pump OFF")

        send_to_thingspeak(temp, humidity, soil)
        time.sleep(60)

except KeyboardInterrupt:
    GPIO.cleanup()


    

  ##  👨‍💻 MY Role in Project
I designed and implemented a Smart Garden System using Raspberry Pi. I wrote the Python code for sensor reading, IoT communication, and automation logic. I also handled the circuit wiring and connected the system to ThingSpeak for live monitoring.


✅ How to Run
Install dependencies:

sudo pip3 install Adafruit_DHT RPi.GPIO requests

2Run the code:

python3 main.py




