# BEAVS 6.7
BEAVS is a rocketry flight computer, with a comprehensive sensor suite and five servo channels.

## Features
- IMU
- Barometer
- Magnetometer
- Five 8.4V 10A servo channels with current monitoring
- Status LEDs
- Reverse polarity protection

## Parts
- RP2040 microcontroller
- ISM6HG256X IMU
- MS5607 barometer
- LIS2MDL magnetometer
- INA745 current monitors

## Pinout
| GPIO | Function            |
|------|---------------------|
|    0 | MISO                |
|    2 | SCK                 |
|    3 | MOSI                |
|    1 | Barometer CS        |
|    6 | IMU CS              |
|    4 | SDA                 |
|    5 | SCL                 |
|    7 | SD CMD              |
|    8 | SD DAT0             |
|    9 | SD DAT1             |
|   10 | SD DAT2             |
|   11 | SD DAT3             |
|   12 | SD CLK              |
|   14 | Expansion 1 (SDA)   |
|   15 | Expansion 2 (SCL)   |
|   13 | UART RX             |
|   16 | UART TX             |
|   17 | Servo power enable  |
|   28 | Efuse current       |
|   19 | Efuse status        |
|   27 | Servo 1             |
|   23 | Servo 2             |
|   24 | Servo 3             |
|   25 | Servo 4             |
|   26 | Servo 5             |
|   29 | Battery sense       |
|   22 | LED data            |
|   18 | Levelshift dir      |
|   21 | Arm switch          |

## Addresses
| Name             | Part     | I2C Address |
|------------------|----------|-------------|
| Magnetometer     | LIS2MDL  | 0x1e        |
| Servo 1 monitor  | INA745   | 0x40        |
| Servo 2 monitor  | INA745   | 0x41        |
| Servo 3 monitor  | INA745   | 0x43        |
| Servo 4 monitor  | INA745   | 0x44        |
| Servo 5 monitor  | INA745   | 0x45        |

## Notes
- The servo power enable pin is active high
- The boot and reset button on the board are enabled by the jumper J14 on the top right side of the board, this jumper must be removed before flight
- The servo pins are, from the center of the board to the edge, signal, ground, power
- The levelshift dir pin should be low in normal operation, and never floating
- The servo data pins and LED data pin should never be floating
- The arming switch should have an internal pullup, and closing the switch connects the pin to ground
- The battery sense pin is connected through a 100k-51k voltage divider, so the pin voltage is 0.3311 times the battery voltage
- Each servo channel can measure up to 39A, but continuous current shouldn't go much above 10A
- The total current consumption should be below 15A continuous
- The efuse current limit is set to 17.6A
- The addressable LEDs are WS2812-compatible, and they are chained as follows: status, magnetometer, barometer, IMU, SD
- The board can be configured to act as a USB host by swapping the CC resistors and adding a jumper, see the schematic

