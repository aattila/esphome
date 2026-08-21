# ESPHome [![Discord Chat](https://img.shields.io/discord/429907082951524364.svg)](https://discord.gg/KhAMKrd) [![GitHub release](https://img.shields.io/github/release/esphome/esphome.svg)](https://GitHub.com/esphome/esphome/releases/) [![CodSpeed](https://img.shields.io/endpoint?url=https://codspeed.io/badge.json)](https://codspeed.io/esphome/esphome)

> **Note**: This is a fork of the official ESPHome repository that adds support for the Waveshare 1.54in-b ePaper display (black and red colors). The original can be found at [esphome/esphome](https://github.com/esphome/esphome).

<a href="https://esphome.io/">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://media.esphome.io/logo/logo-text-on-dark.svg">
    <img src="https://media.esphome.io/logo/logo-text-on-light.svg" alt="ESPHome Logo">
  </picture>
</a>

---

## Solar PV Display Example

This repository includes an example configuration for a solar power monitoring display using an ESP8266 and a Waveshare 1.54" ePaper display.

![Solar PV Display Example](https://raw.githubusercontent.com/aattila/esphome/dev/example/solar-pv.jpg)


Wiring schema with NodeMCU (ESP8266)

![Wiring Example](https://raw.githubusercontent.com/aattila/esphome/refs/heads/dev/example/wiring.drawio.png)


The example shows real-time solar power data fetched from Home Assistant, displayed on an ePaper screen with low power consumption.

### Files included:
- `example/solar-pv.yaml` - Complete ESPHome configuration
- `example/solar-pv.png` - Screenshot of the display output
- `example/fonts/materialdesignicons-webfont.ttf` - Material Design Icons font
- `example/fonts/Montserrat-Black.ttf` - Montserrat Black font (optional, for alternative styling)

### Features:
- ESP8266 (ESP01-1M) board configuration
- Waveshare 1.54" black/white/red ePaper display (model 1.54in-b)
- Real-time data from Home Assistant sensors:
  - Inverter total PV power
  - Today's energy production
  - Grid power (import/export)
  - Minimum state of charge
- Control switches for night lamp and mains power
- Custom lambda rendering with word-wrapping and grey dithering
- Deep sleep cycle to conserve battery power
- OTA updates with encryption

### How to use this example:

1. **Install required fonts**:
   Copy the font files from `example/fonts/` to your ESPHome config directory (or reference them directly as shown in the YAML).

2. **Update WiFi credentials**:
   Replace `YOUR_SSID` and `YOUR_PASSWORD` with your actual WiFi network details.

3. **Update Home Assistant entity IDs**:
   Modify the `entity_id` values in the `sensor:` and `switch:` sections to match your Home Assistant entities:
   - `sensor.inverter_1_total_pv_power`
   - `sensor.inverter_1_energy_today`
   - `sensor.inverter_1_grid_power`
   - `sensor.min_soc`
   - `switch.night_lamp`
   - `switch.mains_switch_0`

4. **Update encryption key** (optional but recommended):
   Generate a new AES encryption key for the API:
   ```bash
   openssl rand -base64 32
   ```
   Replace the value in the `encryption:` key section.

5. **Compile and upload**:
   ```bash
   esphome run example/solar-pv.yaml
   ```

### Display layout:
The ePaper display shows:
- Top-left: Solar panel icon (grey when <200W, red when producing power)
- Top-center: Current power production in watts
- Top-right: Energy produced today in kWh
- Middle-left: Grid power import/export (red when >9000W)
- Middle-left: Battery state of charge percentage
- Bottom-left: Night lamp status indicator (red circle when on)
- The display updates every 3 minutes via deep sleep cycles

---

[Documentation](https://esphome.io) -- [Issues](https://github.com/esphome/esphome/issues) -- [Feature requests](https://github.com/orgs/esphome/discussions)

---

[![ESPHome - A project from the Open Home Foundation](https://www.openhomefoundation.org/badges/esphome.png)](https://www.openhomefoundation.org/)