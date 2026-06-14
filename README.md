# Carrier board for Embedded RIO

This is the PCB for the master thesis "Embedded Radar-Inertial Odometry". It is a carrier board built around a Teensy 4.0 that holds all the sensors and plugs into a Pixhawk flight controller.

The firmware that runs on it lives in a separate repo:
https://github.com/NicolaiAdil/embedded_rio

## What is on the board

- Teensy 4.0 microcontroller (runs the estimator)
- TI IWR6843AOPEVM mmWave radar (connected with the samtec 60 pin connector)
- Bosch BMI088 IMU
- Bosch BMP388 barometer
- micro-SD card slot for logging
- status LEDs
- connector to the Pixhawk 6C mini (TELEM1 port)

## Power

Power comes in as a single 5V rail from the Pixhawk TELEM1 port. The radar runs
straight off the 5V. The Teensy makes its own 3.3V rail that powers the IMU, the
barometer, and the SD card.

## Buses and links

- I2C at 400 kHz shared by the IMU and the barometer
- UART to the radar for config at 115200 baud
- UART from the radar for the detection stream at 921600 baud
- UART to the Pixhawk carrying MAVLink at 921600 baud

## Files

This is a normal KiCad project. Open `carrierboard_teensy_v3.kicad_pro` in KiCad to see the schematic and the layout. Fabrication outputs are generated with the
Fabrication Toolkit plugin (settings are in `fabrication-toolkit-options.json`).

## Known issue, read before ordering more boards

The mounting holes are not quite right, but it works. The hole dimensions and positions are a little off, so before sending this off for a new batch they should be adjusted slightly. Changing the holes will move things around a bit, so expect to redo some of the routing (rewiring) after the fix.
