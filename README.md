
# 💨 Ventilation System Controller

An embedded system project for intelligent **airflow and pressure control** in indoor environments. Built using Raspberry Pi Pico, industrial sensors, and MQTT connectivity, the system ensures optimal ventilation through local and remote control.

> 🏫 Developed by Mong Phan, Xuan Dang, Sami Barbaglia, Hanh Hoang  
> 🎓 Metropolia University of Applied Sciences, School of ICT  
> 📅 Spring 2024

---

## 📌 Key Features

- Manual and automatic fan control (0–100% fan speed or 0–120 Pa pressure)
- MQTT communication with JSON-formatted messages
- Live environment monitoring (CO₂, temperature, humidity, pressure)
- EEPROM-based configuration for Wi-Fi and MQTT broker
- Local interface: OLED, rotary encoder, and push buttons

---

## 🧭 How to Use the System

### 🖥️ Local User Interface (OLED + Encoder)

- **Startup** → Displays MQTT connection status
- **Main Menu** (navigate with knob, confirm with OK):
  - **Set Fan Speed**: Manual mode, adjust 0–100%
  - **Set Pressure**: Automatic mode, adjust 0–120 Pa
  - **Show Status**: Live values (updated every 3 seconds)
  - **WiFi and MQTT**: Configure SSID, password, MQTT broker IP

### 🔧 Button Functions

| Button         | Action                                     |
|----------------|--------------------------------------------|
| OK (SW_0)      | Confirm / edit / save                      |
| BACK (SW_2)    | Return to main menu                        |
| Rotary Knob    | Scroll/select menu items or characters     |

### ⚠️ Error Handling

If the target pressure cannot be reached in automatic mode within 1 minute, an error screen is shown and `error=true` is published over MQTT.

---

## 🌐 MQTT Integration

### Topics

- `controller/settings` – receive control settings
- `controller/status` – publish current status

### Example Messages

**Manual Mode**
```json
{
  "auto": false,
  "speed": 35
}
```

**Automatic Mode**
```json
{
  "auto": true,
  "pressure": 45
}
```

**Status Update**
```json
{
  "nr": 5,
  "speed": 35,
  "setpoint": 35,
  "pressure": 8,
  "auto": false,
  "error": false,
  "co2": 412,
  "rh": 45,
  "temp": 21
}
```

---

## 🛠️ Hardware Components

| Component              | Description                                |
|------------------------|--------------------------------------------|
| Raspberry Pi Pico      | Main MCU                                    |
| Produal MIO 12-V       | Modbus IO device for fan control            |
| GMP252                 | Modbus CO₂ sensor                           |
| HMP60                  | Modbus RH + Temperature sensor              |
| SDP610                 | I²C differential pressure sensor            |
| OLED (SSD1306)         | Local UI display                            |
| Rotary Encoder + Btns  | User input interface                        |

---

## 🧠 Software Overview

- Written in C++ with Pico SDK
- Modbus and MQTT libraries with C++ wrappers
- Local OLED UI for mode switching and configuration
- EEPROM I²C interface for persistent settings

---

## 📂 Project Structure

```
/src
 ├── main.cpp
 ├── modbus.cpp
 ├── mqtt.cpp
 ├── ui.cpp
 ├── sensors.cpp
 ├── storage.cpp
/Docs
 ├── Ventilation_controller_project_specification.pdf
 ├── Ventilation_controller_project_report.pdf
 ├── User_Manual.pdf
```

---

## 📋 Documentation

- [📄 System Specification (PDF)](./Docs/Ventilation_controller_project_specification.pdf)
- [📄 Project Report (PDF)](./Docs/Ventilation_controller_project_report.pdf)
- [📄 User Manual (PDF)](./Docs/User_Manual.pdf)

---

## 👨‍💻 Contributors

- **Mong Phan**
- **Xuan Dang**
- **Sami Barbaglia**
- **Hanh Hoang**

---

## 📜 License

This project was created for academic purposes at **Metropolia University of Applied Sciences**. Users can freely use this project for educational purpose ONLY.
