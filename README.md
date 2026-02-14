## ESPHome Zehnder ComfoAir E300/E400
ESPHome component for communication with the Zehnder ComfoAir E300/E400 heat recovering ventilation units.

### Setup 
The unit uses RS485 serial communication at 19200:8:EVEN:1. Connect using a twisted pair wired to the C3 port on the Zehnder unit.

The C3 connector is located at the top right of display. To access it, remove the cover surrounding the display by removing three torx screws. 
The pin-out is shown in the image below
![C3 port pinout](docs/connector.png)

### Example of minimal configuration yaml
```yaml
packages:
  remote_package:
    url: https://github.com/CodedCactus/zehnder-comfoair
    ref: main
    files: [components/zehnder.yaml]
    refresh: 0s
    
logger:
  level: VERBOSE
  baud_rate: 0 # disable logger for hardware UART support

uart:
  id: uart_modbus
  tx_pin: GPIO01
  rx_pin: GPIO03
  baud_rate: 19200
  data_bits: 8
  parity: EVEN
  stop_bits: 1

modbus:
  uart_id: uart_modbus
  id: modbus1
#  flow_control_pin: GPIOXX # used for the MAX485 chip without automatic flow control

modbus_controller:
- id: modbus_device
  address: 0x1
  modbus_id: modbus1
  setup_priority: -10
  update_interval: 5s
```

### Registry table

holding registers

| Adress | Name                                | Datatype | Unit  | Note                     |
|--------|-------------------------------------|----------|-------|--------------------------|
| 0x136  | Exhaust fan duty cycle              | U_WORD   | %*10  |                          |
| 0x137  | Supply fan duty cycle               | U_WORD   | %*10  |                          |
| 0x138  | Exhaust fan air flow                | U_WORD   | m³/h  |                          |
| 0x139  | Supply fan air flow                 | U_WORD   | m³/h  |                          |
| 0x13A  | Exhaust fan speed                   | U_WORD   | RPM   |                          |
| 0x13B  | Supply fan speed                    | U_WORD   | RPM   |                          |
| 0x12C  | Outdoor air temperature             | S_WORD   | °C*10 |                          |
| 0x12D  | Pre-heater temperature              | S_WORD   | °C*10 |                          |
| 0x12F  | Supply air temperature              | S_WORD   | °C*10 |                          |
| 0x130  | Extract air temperature             | S_WORD   | °C*10 |                          |
| 0x131  | Exhaust air temperature             | S_WORD   | °C*10 |                          |
| 0x14A  | 3-way switch ventilation setpoint   | U_WORD   | -     | 0:low;50:medium;100:high |
| 0x148  | 0-10 V ventilation setpoint         | u_word   | -     | 0:low;50:medium;100:high |
| 0x149  | RF ventilation setpoint             | U_WORD   | -     | 0:low;50:medium;100:high |
| 0x13D  | RF input voltage                    | U_WORD   | V*10  | steering signal (0-10)   |