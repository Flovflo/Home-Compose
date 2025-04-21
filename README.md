# 🏡 flovflo-home-compose: Intelligent and Eco-Friendly Home Management

Welcome to **flovflo-home-compose**, your one-stop solution for a connected, adaptable, and energy-optimized home. Leveraging Home Assistant, ESPHome, Docker, and Frigate, this project walks you through building a powerful domotics ecosystem centered on solar energy management.

> "Imagine a home that anticipates your needs, adjusts lighting and temperature, and prioritizes solar production—now a reality!"

---

## 📂 Repository Structure

```text
flovflo-home-compose/
├── README.md
├── automatisation/
│   ├── detect.yaml
│   ├── Smart-Plug.yaml
│   ├── Smart-Plug2.yaml
│   └── smart-water heater.yaml
├── docker-composHA/
│   ├── docker-compose-frigate.yml
│   └── docker-compose-HA.yaml
├── ESPhome/
│   ├── detect.yaml
│   └── linky.yaml
└── Frigate/
    └── config.yml
```

- **ESPhome/**: Firmware definitions for sensors and teleinfo
- **automatisation/**: Home Assistant automation scripts (YAML)
- **docker-composHA/**: Docker compositions for HA, Frigate, MQTT, Watchtower...
- **Frigate/**: Smart video surveillance configuration

---

## ⚡ ESPHome Components

1. **detect.yaml**
   - **Hardware**: ESP32-S2 Mini + LD2410 presence sensor
   - **Features**:
     - Presence, movement, and ambient light detection
     - Dynamic `light_threshold` and `timeout` adjustments
     - UART at 256 000 bps, detailed INFO-level logs
   - **Integration**: Native Home Assistant API for real-time automations

2. **linky.yaml**
   - **Hardware**: NodeMCU (ESP8266)
   - **Teleinfo (3-phase)**:
     - Measures consumed and injected energy (kWh), instantaneous power (VA/W)
     - Phase currents (A) and voltages (V) with state_class filters (`multiply`, lambda functions)
   - **Resilience**: Wi-Fi fallback hotspot, SNTP (Europe/Paris), secure OTA
      ![Dessin sans titre](https://github.com/Flovflo/Home-Compose/assets/86321847/9f77e768-4ed2-41b6-a4af-5c379ecb825c)

---

## 🤖 Home Assistant Automations

1. **detect.yaml**
   - Toggle Yeelight on presence detection
   - 100% brightness only when presence is active

2. **Smart-Plug.yaml** & **Smart-Plug2.yaml**
   - Automatic control of plugs 4 & 5 based on solar production (> 1 kW) and master device state
   - Turns off if grid consumption > 200 W or if conditions reverse
   - Push notifications on state changes
   - Scheduled checks every 10 min (/10) and 15 min (/15)

3. **smart-water heater.yaml**
   - Controls solar water heater when production > 1.8 kW or during off-peak hours (21:30–23:30, 02:30–06:30)
   - Turns off if consumption > 300 W outside off-peak periods
   - Maximizes savings while ensuring comfort

---

## 🐳 Docker Orchestration (docker-composHA)

### docker-compose-HA.yaml
- **homeassistant**: Official image, persistent volumes
- **esphome**: Firmware deployment service
- **cloudflared**: Secure tunnel to your instance
- **watchtower**: Automatic updates at 04:00 daily (`0 0 4 * * *`)
- **scrypted** & **matter-server**: Media integrations and Matter support

### docker-compose-frigate.yml
- **Mosquitto**: Robust MQTT broker (ports 1883 & 9001)
- **Frigate**: Real-time object detection (person, car, dog, cat)
  - Custom detection zones (entry), motion masks
  - tmpfs for performance (1 GB)

---

## 🎥 Frigate Video Surveillance

- **config.yml**:
  - MQTT connection with TLS
  - Single RTSP camera at 1920×1080 @2 fps
  - Tracked objects & custom zones
  - CPU detector with 6 threads

---

## 🚀 Quick Start

1. **Clone** the repo:
   ```bash
   git clone https://github.com/Flovflo/Home-Compose.git
   cd flovflo-home-compose
   ```
2. **Configure** your secrets (`!secret`) and environment vars (`$cloudflared-token`, `$mdp-rtsp`, etc.)
3. **Launch** services:
   ```bash
   docker-compose -f docker-composHA/docker-compose-HA.yaml up -d
   docker-compose -f docker-composHA/docker-compose-frigate.yml up -d
   ```
4. **Monitor** logs and verify Lovelace integration

---

## 🤝 Contributing & Support

Contributions, issues, and suggestions are welcome!
- Open an **issue** for bugs or feature requests
- Submit a **PR** to share your use case

