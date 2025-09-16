# Raven Yocto Avionics Project

## Overview

This repository contains a Yocto Project setup for building a custom Linux image for the Raven Rocket avionics system. It targets the Raspberry Pi 4 (64-bit) and includes Python-based tools for OTA commands and telemetry logging.

The build system uses a modular **layer architecture**, allowing for easy customization, package management, and feature inclusion.

---

## Yocto Layers

Yocto uses **layers** to organize recipes, configurations, and metadata. Each layer has a specific purpose:

| Layer | Purpose |
|-------|---------|
| `meta` | Core Yocto metadata and recipes from Poky |
| `meta-poky` | Standard Poky extensions and utilities |
| `meta-yocto-bsp` | Board support packages for Raspberry Pi 4 |
| `meta-raven` | Custom layer for Raven avionics image (`raven-image`) |

Layers are combined in `bblayers.conf` to determine which recipes and configuration files are available during the build.

---

## Build Process

The build process generates a **custom Linux image** for the Raspberry Pi 4:

1. **Minimal Image**  
   Command:  
   ```bash
   bitbake core-image-minimal

2. **Raven Custom Image**  
   The `raven-image` is the fully featured image for the **Raven Rocket avionics system**.  
   While the minimal image only provides a basic Linux environment to ensure the system can boot, the `raven-image` includes all tools, scripts, and Python packages required for the rocket's operations, such as:

   - **OTA Listener**: Receives and executes remote commands via MQTT.
   - **Telemetry Logger**: Captures and logs data from sensors and communication devices (e.g., LoRa modules, IMU, GPS).
   - **Python Tools**: OpenCV, NumPy, PySerial, Paho-MQTT for payload control and data processing.
   - **Utilities**: curl, socat, screen, vim, git for debugging, monitoring, and maintenance.
   - **SSH Server**: Enables remote access for debugging and updates.

   Build command:  
   ```bash
   bitbake raven-image

---

##Final Design Implementation

```mermaid
flowchart TD
    A[Yocto Build on Host PC] --> B[Generate raven-image]
    B --> C[Flash SD Card]
    C --> D[Raspberry Pi Boots Custom Image]
    D --> E[OTA Listener Active]
    D --> F[Telemetry Logger Active]
    E -->|MQTT Commands| PiPayload[Execute Commands on Payload]
    F -->|Logs Data| LogFile[Telemetry Log]
    G[Ground Station] -->|Send MQTT Commands| E
    F -->|Upload Data| G
