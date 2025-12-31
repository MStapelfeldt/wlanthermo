
# Wlanthermo Home Assistant Integration

This project provides a custom integration for WlanThermo with Home Assistant. If you have struggled to get WlanThermo working with existing solutions, this package offers a structured, ready-to-use approach.

## Credits
This code is based on the work of others. Special thanks to:
- [mfdir](https://github.com/mfdlr/homeassistant-wlanthermo)
- [m0uH](https://github.com/m0uH/homeassistant-wlanthermo)
- [dermichahc](https://wlanthermo.de/threads/home-assistant-wlanthermo-nano.575/#post-5576)

For questions, visit the [WlanThermo Forum](https://wlanthermo.de/threads/home-assistant-wlanthermo-nano.575/).

## Features
- Integrates WlanThermo data into Home Assistant
- Pre-configured sensors, numbers, and templates
- Example dashboard layout and MQTT setup

## Getting Started

### 1. Update `configuration.yaml`
Add the following to your Home Assistant `configuration.yaml`:
```yaml
homeassistant:
  packages: !include_dir_named packages
```

### 2. Folder Structure
Create the following folders and upload the files as organized in this repository: (DO NOT UPLOAD FOLDER `old`)
```
/homeassistant/packages/
/homeassistant/packages/wlanthermo/
/homeassistant/packages/wlanthermo/template/
```

Within the `wlanthermo` folder, there is a `secrets.yaml` file containing the MQTT topic settings used for communication with your WlanThermo device. Update these topics if your device uses different MQTT topics or a different device name. The default topics are:

```yaml
wlanthermo_data_topic: WLanThermo/MINI-V3/status/data
wlanthermo_settings_topic: WLanThermo/MINI-V3/status/settings
wlanthermo_set_topic: WLanThermo/MINI-V3/set/channels
```

Adjust these values to match your WlanThermo's MQTT configuration if necessary. Then copy these secrets to your Home Assistant secrets file at `/homeassistant/secrets.yaml`

### 3. Additional Plugins for Dashboard
To use the provided dashboard layout (see `bbq.yaml`), install these custom components via HACS:
- [lovelace-badge-card](https://github.com/thomasloven/lovelace-badge-card)
- [lovelace-layout-card](https://github.com/thomasloven/lovelace-layout-card)
- [config-template-card](https://github.com/iantrich/config-template-card)
- [button-card](https://github.com/custom-cards/button-card)
- [kiosk-mode](https://github.com/maykar/kiosk-mode)
- [vertical-stack-in-card](https://github.com/ofekashery/vertical-stack-in-card)
- [apexcharts-card](https://github.com/RomRider/apexcharts-card)

Refer to the documentation in each repository for installation instructions. For editing files, the easiest way is to use the "File editor" add-on from the Home Assistant Add-on Store. Create files with the same names, add the content, and save.

For `bbq.yaml`, create a new dashboard, open the menu (three dots at the top right), select "Edit dashboard," then "Edit raw configuration," and paste the content.

### 4. MQTT Setup
To receive data from WlanThermo, you need an MQTT broker. [Mosquitto broker](https://github.com/home-assistant/addons/blob/master/mosquitto/DOCS.md) is recommended. Set up WlanThermo to use your Home Assistant IP address:

![MQTT](https://raw.githubusercontent.com/MStapelfeldt/wlanthermo/main/WT-MQTT.PNG "MQTT")

**Important:** Set your host to **MINI-V3** for the files to work without changes. Otherwise, update `secrets.yaml` to match your device name.

![System](https://raw.githubusercontent.com/MStapelfeldt/wlanthermo/main/WT%20system.PNG "System")
```yaml
# with the secrets file we have a variable to change relative path:
"WLanThermo/${wlanthermo_model}/status/data"
```

### 5. Final Dashboard
After adding all files, updating `configuration.yaml`, setting up MQTT, and installing the required add-ons, you should see a dashboard like this:

![Dashboard](https://raw.githubusercontent.com/MStapelfeldt/wlanthermo/main/WT%20Dashboard.PNG "Dashboard")

- **Top row:** Temperatures of all 8 channels. Click a channel for a detailed view (third row).
- **Second row:** Timer (left) shows estimated BBQ readiness. Pitmaster1 settings (right) allow you to set temperature, mode, and profile. It is recommended to keep the channel set to 9.
- **Third row:** Left shows the selected channel (from top row). Adjust temperature and alarms for each channel or Pitmaster 2. Right shows a graph of all temperature history.
