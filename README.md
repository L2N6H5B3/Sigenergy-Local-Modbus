# 📘 Sigenergy ESS Integration for Home Assistant
[![HACS](https://img.shields.io/badge/HACS-Default-blue)](https://hacs.xyz/) [![Release](https://img.shields.io/github/v/release/TypQxQ/HACS-Sigenergy-Local-Modbus)](https://github.com/TypQxQ/HACS-Sigenergy-Local-Modbus/releases) [![License](https://img.shields.io/github/license/TypQxQ/HACS-Sigenergy-Local-Modbus)](LICENSE)

## Overview
The Sigenergy ESS Integration brings local Modbus‑TCP monitoring and control of your Sigenergy Energy Storage System (ESS) directly into Home Assistant. Gain real‑time insights, dynamic device management, and seamless UI‑based setup.

## Features
- **UI‑Driven Setup** with DHCP discovery  
- **Dynamic Device Management** (Plants, Inverters, AC/DC Chargers)  
- **Auto‑Detect** supported registers via Modbus probing  
- **Real‑Time Metrics** for power flows, energy statistics, SoC/SoH  
- **Control Capabilities** for EMS work modes and more

## Requirements
- Home Assistant **2024.4.1** or newer  
- Home Assistant Community Store (HACS)  
- Sigenergy ESS with Modbus‑TCP enabled  
- Network connectivity between HA and Sigenergy devices

## Installation
### HACS (Recommended)
1. Go to **HACS > Integrations** in Home Assistant  
2. Click the three dots and select **Custom repositories**  
3. Add repository `TypQxQ/HACS-Sigenergy-Local-Modbus` as **Integration**  
4. Install **Sigenergy ESS Integration**  
5. Restart Home Assistant

### Manual
1. Download the latest `.zip` from the [Releases](https://github.com/TypQxQ/HACS-Sigenergy-Local-Modbus/releases) page  
2. Extract and copy `custom_components/sigen` into your HA `custom_components/` folder  
3. Restart Home Assistant

## Quickstart Automation Example
```yaml
alias: "Notify on Low Battery"
trigger:
  - platform: state
    entity_id: sensor.plant_battery_soc
    to: "<20"
action:
  - service: notify.mobile_app
    data:
      title: "Battery Low"
      message: "SoC dropped below 20%"
```

## Configuration & Usage
### Plant Concept
Central **Plant** entry groups devices by Host/IP and Port.  
```mermaid
graph TD
  P[Plant (IP:Port)] --> I1[Inverter 1 (ID 1)]
  P --> I2[Inverter 2 (ID 2)]
  P --> AC1[AC Charger (ID 3)]
  I1 --> DC1[DC Charger (via Inverter 1)]
```

### Initial Setup
1. Navigate to **Settings > Devices & Services > Add Integration**  
2. Search for **Sigenergy**  
3. If discovered, click **Configure**; otherwise select manually  
4. Enter **Host IP**, **Port** (default 502), and first **Slave ID**  
5. Add additional Inverters/Chargers via the same Plant entry

### Reconfiguration
Go to **Settings > Devices & Services**, locate **Sigenergy**, and click **Configure** to modify host, slave IDs, scan intervals, or remove devices.

## Entities & Controls
**Plant Entities:** active/reactive power, PV power, SoC, grid flows, EMS mode  
**Inverter Entities:** MPPT metrics, battery SoC/SoH, phase data  
**AC Charger:** charging power, total energy, system state  
**DC Charger:** charging power, status  
**Controls:** EMS work modes via `select`, optional `button`/`switch`

## Troubleshooting
- Verify IP, port, and firewall settings  
- Ensure Modbus‑TCP is enabled on your ESS  
- Check Home Assistant logs for `sigen` errors  
- Confirm correct Slave IDs and allow probe time after adding devices

## Contributing
Contributions welcome!  
1. Fork the repo and create a branch  
2. Add tests under `tests/components/sigen/`  
3. Follow Home Assistant coding and config‑flow patterns  
4. Submit a Pull Request

## Support & Links
- Issues: https://github.com/TypQxQ/HACS-Sigenergy-Local-Modbus/issues  
- Discussions: https://github.com/TypQxQ/HACS-Sigenergy-Local-Modbus/discussions  
- HACS docs: https://hacs.xyz/

## License
MIT License © [Your Name]