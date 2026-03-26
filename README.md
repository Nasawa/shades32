# shades32

ESPHome configuration for motorized roller shades on an ESP32. Controls a DC motor via an H-bridge, tracks position with a rotary encoder, and exposes the shades as a `cover` entity in Home Assistant.

## What It Does

`main.yaml` is a complete ESPHome device config for a roller shade controller. It handles:

- **Open/close/stop** via a template cover entity (wired to Home Assistant)
- **Motor control** through an H-bridge using three GPIO outputs (IN1, IN2, ENABLE)
- **Limit switches** — top and bottom contact sensors to detect end positions
- **Position tracking** — rotary encoder counts rotations to know where the shade is
- **Manual buttons** — physical Up/Down buttons (internal, not exposed to HA)
- **Luminosity sensor** — light level detection (binary, not analog)
- **Rotary encoder button** — exposed as a binary sensor

## Pin Mapping

| GPIO | Function |
|------|----------|
| GPIO5 | Top contact (limit switch) |
| GPIO18 | Bottom contact (limit switch) |
| GPIO14 | Up button (internal) |
| GPIO13 | Down button (internal) |
| GPIO25 | Rotary encoder button |
| GPIO19 | Luminosity sensor |
| GPIO26 | Motor IN1 |
| GPIO27 | Motor IN2 |
| GPIO22 | Motor ENABLE |
| GPIO32 | Rotary encoder CLK |
| GPIO33 | Rotary encoder DT |

## How to Use

1. Install [ESPHome](https://esphome.io/)
2. Fill in your WiFi credentials and Home Assistant API key in the appropriate section (not committed here)
3. Flash to an ESP32: `esphome run main.yaml`

The cover will appear in Home Assistant as "Roller Shades" and can be controlled via automations, Lovelace, or voice.

## Notes

Built in 2024. The motor direction is controlled by toggling IN1/IN2 on the H-bridge while asserting ENABLE. The contact sensors use 10ms debounce filters to avoid noise on the limit switch inputs.
