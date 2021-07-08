# DukeCarge's Marlin 2.0.8.1 configuration

Hi! Welcome to my config for using an `SKR 1.3` with Marlin on an Anycubic i3 Mega. This works for both i3 Mega and i3 Mega-S. If you have any other SKR boards, you'll need to make some changes.

Note: This should serve as a jumping off point for others who are trying to get started with Marlin. As such I will list some things to watch out for in this repository.

***IMPORTANT NOTE:*** You should get a *different* LCD screen if you are going to a custom board. Any version of Marlin that needs to work with the **Stock LCD** requires a rare version of the LCD's firmware. I do not know where to get it.

## Printer Specs

- Needs 5 stepper drivers for compatibility
  - Single X-axis stepper
  - Single Y-axis stepper
  - Dual Z-axis stepper (You could get away with 4 and splice the cables together. However, it means you MUST change everything in this repository in regards to the Z-axis.)
  - BMG Clone Bowden Extruder
  - All 5 steppers are Nema 17s
- E3D v5 hotend clone (a v6 will fit, but will be shorter.)
- Anycubic Glass Ultrabase
- BIGTREETECH TFT24 V1.1 - Replaces the old LCD screen. Fits with the following [bracket](https://www.thingiverse.com/thing:4843427).

## Code changes

***WIP, this takes some time***

### `Configuration.h`
- Line 112 - uncommented `SERIAL_PORT_2` and set it to `-1`
- Line 137 - Changed `MOTHERBOARD` to `BOARD_BTT_SKR_V1_3`
- Line 141 - Defined custom machine name
-

### `pins_BTT_SKR_common.h`
- Line 80 - Changed `HEATER_0_PIN` to `P2_04` for troubleshooting. Swap with define on line 84 if not using HE1 for heating.
- Line 84 - Changed `FAN1_PIN` to `P2_07` for troubleshooting. Swap with define on line 80 if not using HE1 for heating.

## Daughterboard pinout

There is an interfacing board between the printer's peripherals (Save for Y-axis controls) and its mainboard. [This Website](https://www.auditeon.com/projects:3dprinting:anycubic_i3_mega:redesign_hub_pcb) has a great breakdown of the pins. I still recommend taking a multimeter, on the continuity setting and verifying all of these.

For my printer, I ended up replacing this board entirely with a custom soldered solution so that I could add back individual GND pins (this changes nothing in the config files)

## Additional links

- [Kris_3D's SKR 1.4 conversion guide](https://www.thingiverse.com/thing:4613998)

# Marlin 3D Printer Firmware

![GitHub](https://img.shields.io/github/license/marlinfirmware/marlin.svg)
![GitHub contributors](https://img.shields.io/github/contributors/marlinfirmware/marlin.svg)
![GitHub Release Date](https://img.shields.io/github/release-date/marlinfirmware/marlin.svg)
[![Build Status](https://github.com/MarlinFirmware/Marlin/workflows/CI/badge.svg?branch=bugfix-2.0.x)](https://github.com/MarlinFirmware/Marlin/actions)

<img align="right" width=175 src="buildroot/share/pixmaps/logo/marlin-250.png" />

Additional documentation can be found at the [Marlin Home Page](https://marlinfw.org/).
Please test this firmware and let us know if it misbehaves in any way. Volunteers are standing by!

## Marlin 2.0

Marlin 2.0 takes this popular RepRap firmware to the next level by adding support for much faster 32-bit and ARM-based boards while improving support for 8-bit AVR boards. Read about Marlin's decision to use a "Hardware Abstraction Layer" below.

Download earlier versions of Marlin on the [Releases page](https://github.com/MarlinFirmware/Marlin/releases).

## Building Marlin 2.0

To build Marlin 2.0 you'll need [Arduino IDE 1.8.8 or newer](https://www.arduino.cc/en/main/software) or [PlatformIO](http://docs.platformio.org/en/latest/ide.html#platformio-ide). Detailed build and install instructions are posted at:

  - [Installing Marlin (Arduino)](http://marlinfw.org/docs/basics/install_arduino.html)
  - [Installing Marlin (VSCode)](http://marlinfw.org/docs/basics/install_platformio_vscode.html).

### Supported Platforms

  Platform|MCU|Example Boards
  --------|---|-------
  [Arduino AVR](https://www.arduino.cc/)|ATmega|RAMPS, Melzi, RAMBo
  [Teensy++ 2.0](http://www.microchip.com/wwwproducts/en/AT90USB1286)|AT90USB1286|Printrboard
  [Arduino Due](https://www.arduino.cc/en/Guide/ArduinoDue)|SAM3X8E|RAMPS-FD, RADDS, RAMPS4DUE
  [ESP32](https://github.com/espressif/arduino-esp32)|ESP32|FYSETC E4, E4d@BOX, MRR
  [LPC1768](http://www.nxp.com/products/microcontrollers-and-processors/arm-based-processors-and-mcus/lpc-cortex-m-mcus/lpc1700-cortex-m3/512kb-flash-64kb-sram-ethernet-usb-lqfp100-package:LPC1768FBD100)|ARM® Cortex-M3|MKS SBASE, Re-ARM, Selena Compact
  [LPC1769](https://www.nxp.com/products/processors-and-microcontrollers/arm-microcontrollers/general-purpose-mcus/lpc1700-cortex-m3/512kb-flash-64kb-sram-ethernet-usb-lqfp100-package:LPC1769FBD100)|ARM® Cortex-M3|Smoothieboard, Azteeg X5 mini, TH3D EZBoard
  [STM32F103](https://www.st.com/en/microcontrollers-microprocessors/stm32f103.html)|ARM® Cortex-M3|Malyan M200, GTM32 Pro, MKS Robin, BTT SKR Mini
  [STM32F401](https://www.st.com/en/microcontrollers-microprocessors/stm32f401.html)|ARM® Cortex-M4|ARMED, Rumba32, SKR Pro, Lerdge, FYSETC S6
  [STM32F7x6](https://www.st.com/en/microcontrollers-microprocessors/stm32f7x6.html)|ARM® Cortex-M7|The Borg, RemRam V1
  [SAMD51P20A](https://www.adafruit.com/product/4064)|ARM® Cortex-M4|Adafruit Grand Central M4
  [Teensy 3.5](https://www.pjrc.com/store/teensy35.html)|ARM® Cortex-M4|
  [Teensy 3.6](https://www.pjrc.com/store/teensy36.html)|ARM® Cortex-M4|
  [Teensy 4.0](https://www.pjrc.com/store/teensy40.html)|ARM® Cortex-M7|
  [Teensy 4.1](https://www.pjrc.com/store/teensy41.html)|ARM® Cortex-M7|
  Linux Native|x86/ARM/etc.|Raspberry Pi

## License

Marlin is published under the [GPL license](/LICENSE) because we believe in open development. The GPL comes with both rights and obligations. Whether you use Marlin firmware as the driver for your open or closed-source product, you must keep Marlin open, and you must provide your compatible Marlin source code to end users upon request. The most straightforward way to comply with the Marlin license is to make a fork of Marlin on Github, perform your modifications, and direct users to your modified fork.

While we can't prevent the use of this code in products (3D printers, CNC, etc.) that are closed source or crippled by a patent, we would prefer that you choose another firmware or, better yet, make your own.
