# Raspberry Pi Based Accident Detection System

## 📌 Project Overview

This project presents a Raspberry Pi based accident detection system designed to detect vehicle accidents and provide the accident location through GPS and GSM communication.

The system uses a vibration sensor to identify a possible accident event. When an accident is detected, the Raspberry Pi processes the event and obtains the vehicle's location using a GPS module. The location information can then be transmitted through a GSM module to provide an accident alert.

## 🎯 Objectives

* Detect possible vehicle accidents using a vibration sensor.
* Process the sensor data using Raspberry Pi.
* Obtain the vehicle's geographical location using GPS.
* Transmit accident information using GSM communication.
* Develop a low-cost prototype for accident monitoring and emergency notification.

## 🛠️ Hardware Used

* Raspberry Pi
* SW-420 Vibration Sensor
* NEO-6M GPS Module
* SIM800A GSM Module
* Power Supply
* Jumper Wires

## 💻 Software & Technologies

* Raspberry Pi OS
* Python
* Thonny IDE
* Serial Communication
* GPS Communication
* GSM Communication

## 🔄 System Workflow

```text
Vibration Sensor
       ↓
Accident Detection
       ↓
Raspberry Pi
       ↓
GPS Module
       ↓
Location Acquisition
       ↓
GSM Module
       ↓
Accident Alert / Location Message
```

## ⚙️ Working Principle

The vibration sensor continuously monitors for a significant vibration that may indicate an accident.

When the detected vibration crosses the defined threshold, the Raspberry Pi identifies a possible accident event. The system then communicates with the GPS module to obtain the current geographical coordinates.

The acquired location information is processed by the Raspberry Pi and transmitted through the GSM module as part of the accident notification.

## 🐍 Python Implementation

The project software was developed in Python and executed on Raspberry Pi OS using the Thonny IDE.

The Python program handles:

* Sensor monitoring
* Accident event detection
* Communication with the GPS module
* Processing of location information
* GSM-based communication

## 📁 Repository Structure

```text
raspberry-pi-accident-detection/
│
├── README.md
├── .gitignore
│
├── src/
│   └── accident_detection.py
│
└── docs/
    ├── project-report.pdf
    └── project-presentation.pptx
```

## 📊 Expected Output

When an accident event is detected, the system processes the event and obtains the corresponding GPS location. The GSM module is then used to communicate the accident information for emergency notification.

## 👨‍💻 My Contribution

* Developed the Raspberry Pi based accident detection prototype.
* Interfaced the vibration sensor with Raspberry Pi.
* Worked with GPS-based location acquisition.
* Implemented GSM communication.
* Developed and tested the Python program using Thonny IDE on Raspberry Pi OS.
* Integrated the hardware modules and tested the overall system.

## 🚀 Future Scope

* Integration with a mobile application or web dashboard.
* Cloud-based accident monitoring.
* Improved accident detection using multiple sensors.
* Automatic emergency-service notification.
* Real-time tracking and monitoring.
* Improved false-accident detection and reliability.

## 📄 Documentation

Additional technical information about the project is available in the project report and presentation included in the `docs` directory.

## 📌 Project Status

Completed Academic Project
