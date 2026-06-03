# Example configurations

This folder contains minimal example ESPHome configurations for different ESP boards and output options. Use these as a starting point and verify the board and GPIO pins for your hardware.

> [!WARNING] 
> Always check that the board and GPIO pins match your configuration!

## Generic examples:
- [esp8266.yaml](esp8266.yaml) — ESP8266 (NodeMCU v2) with software PWM output.
- [esp32.yaml](esp32.yaml) — ESP32 using the built-in DAC.
- [esp32_external_dac.yaml](esp32_external_dac.yaml) — ESP32 with an external GP8413 DAC (I²C).

Notes:
- These examples reference the package components [components/zehnder_base.yaml](../components/zehnder_base.yaml), [components/zehnder_fw2.yaml](../components/zehnder_fw2.yaml) and [components/fan.yaml](../components/fan.yaml).
- If using a MAX485 without automatic flow control, uncomment and configure the `modbus.flow_control_pin` in the example files.
- Substitute the pins and secrets (Wi‑Fi, API/OTA keys) as required by your setup.

For full project details and wiring, see the project root README: [README.md](../README.md).

## Kits: 
- [m5stack.yaml](m5stack.yaml) — M5Stack RS485 base + ATOM Lite kit (read-only). Parts:
  - [M5Stack Atom Lite](https://www.tinytronics.nl/en/development-boards/microcontroller-boards/with-wi-fi/m5stack-atom-lite-esp32-development-board)
  - [M5Stack RS485 Base](https://www.tinytronics.nl/en/communication-and-signals/serial/rs-485/m5stack-atomic-rs485-base)
  
Notes:
- These examples work without modifications to the code and without soldering.
- Read only by default. Optionally, pin G26 can be used to control the fan speed.
