# BEAVS 6
BEAVS is a rocketry flight computer, with a comprehensive sensor suite and six servo channels.

## Features
- GPS
- Radio
- IMU
- Barometer
- Magnetometer
- Six 8.4V 10A servo channels with current monitoring
- Status LEDs
- Reverse polarity protection

## Parts
- RP2040 microcontroller
- u-blox MAX-M10S GPS
- RFM95W-915 radio (SX1276)
- ISM6HG256X IMU
- MS5607 barometer
- LIS2MDL magnetometer
- INA745 current monitors

## Pinout
| GPIO | Function            |
|------|---------------------|
|    3 | Levelshift dir      |
|    6 | Arm switch          |
|    4 | SDA                 |
|    5 | SCL                 |
|   27 | GPS EXTINT          |
|    9 | MOSI                |
|   10 | MISO                |
|   11 | SCK                 |
|   14 | IMU CS              |
|   13 | Barometer CS        |
|    0 | Radio CS            |
|    1 | Radio D0            |
|    2 | Radio reset         |
|   12 | LED data            |
|    7 | Expansion pin       |
|   15 | Expansion pin       |
|   18 | SD CMD              |
|   19 | SD data 0           |
|   20 | SD data 1           |
|   21 | SD data 2           |
|   22 | SD data 3           |
|   23 | SD clock            |
|    8 | Servo power enable  |
|   28 | Servo 1             |
|   29 | Servo 2             |
|   25 | Servo 3             |
|   24 | Servo 4             |
|   17 | Servo 5             |
|   16 | Servo 6             |
|   26 | Battery sense       |

## Addresses
| Name             | Part     | I2C Address |
|------------------|----------|-------------|
| Magnetometer     | LIS2MDL  | 0x1e        |
| GPS              | MAX-M10S | 0x42        |
| Servo 1 monitor  | INA745   | 0x40        |
| Servo 2 monitor  | INA745   | 0x41        |
| Servo 3 monitor  | INA745   | 0x43        |
| Servo 4 monitor  | INA745   | 0x44        |
| Servo 5 monitor  | INA745   | 0x45        |
| Servo 6 monitor  | INA745   | 0x47        |

## Notes
- The servo power **must be disabled** for the first second or two after power-on, to allow the capacitors to slow-charge without destroying the MOSFETs or causing a brownout.  The enable pin is active high.
- The boot and reset button on the board are enabled by the jumper J14 on the top right side of the board, this jumper must be removed before flight
- The radio **may be damaged** if it is run without an antenna attached
- The servo pins are, from the edge of the board to the center, signal, ground, power
- The levelshift dir pin should be low in normal operation, and never floating
- The servo data pins and LED data pin should never be floating
- The arming switch should have an internal pullup, and closing the switch connects the pin to ground
- The battery sense pin is connected through a 100k-51k voltage divider, so the pin voltage is 0.3311 times the battery voltage
- Each servo channel can measure up to 39A, but continuous current shouldn't go much above 10A
- The total current consumption should be below 30A continuous
- The GPS will blink an LED near the bottom of the board once per second once it gets a fix
- The addressable LEDs are WS2812-compatible, and they are chained as follows: SD, radio, IMU, barometer, magnetometer, status
- The INA745 currently lacks an arduino library

