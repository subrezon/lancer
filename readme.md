# Lancer

The Lancer is a 36-key ortholinear keyboard with a light split and a focus on compact footprint and portability. It is a direct successor to [la_nc](https://github.com/subrezon/la_nc), and is very much inspired by other keyboards like Planck, Lumberjack and Lesovoz.

![](https://github.com/subrezon/lancer/raw/master/docs/lancer-1.png)
![](https://github.com/subrezon/lancer/raw/master/docs/lancer-2.png)
![](https://github.com/subrezon/lancer/raw/master/docs/lancer-3.png)

# Features

- Width of just 11U, the smallest possible with 10 columns and a top-mounted Pro Micro
- More focused thumb row, featuring 6 easily accessible keys
- Powered by a Pro Micro or any other compatible MCU board
- Hotswap sockets in south-facing orientation
- Integrated battery support with a power switch
- Native 3-wire SPI for nice!view support without any bodge wires
- Backwards compatible with oldschool SSD1306 OLEDs (4 leftmost pins of the SPI header)  

# BOM

| Item | Count | Notes |
| :- | :- | :- |
| PCB | 1x | [Gerber file](https://github.com/subrezon/lancer/raw/master/gerbers/lancer-pcb-hotswap/lancer-hotswap-pcb.zip) |
| Top plate | 1x | [Gerber for FR4](https://github.com/subrezon/lancer/raw/master/gerbers/lancer-top-plate/lancer-top-plate.zip), [dxf for other materials](https://github.com/subrezon/lancer/raw/master/dxf/top-plate.dxf) |
| Bottom plate | 1x | [Gerber for FR4](https://github.com/subrezon/lancer/raw/master/gerbers/lancer-bottom-plate/lancer-bottom-plate.zip), [dxf for other materials](https://github.com/subrezon/lancer/raw/master/dxf/bottom-plate.dxf) |
| Pro Micro | 1x | other boards with compatible pinout also work |
| SMD Diodes | 36x | 1N4148W SOD123 |
| MX Hotswap sockets | 36x | Kailh or Gateron |
| Tactile button | 1x | 3x6mm 2-pin button |
| M2 screws | 16x | M2x4 or M2x5, head diameter <5mm |
| M2 standoffs | 8x | 8mm recommended[^1] |
| MX-style switches| 36x | 3-pin or 5-pin |
| 1U MX keycaps | 36x |  |

For wireless operation:

| Item | Count | Notes |
| :- | :- | :- |
| Wireless Pro Micro | 1x | nice!nano, nrfmicro, etc. |
| Rechargeable battery | 1x | 3.7V two-wire battery (eg. 350926) |
| 7-pin SPDT switch | 1x | MSK-12C02 or compatible |

Optionally:

| Item | Count | Notes |
| :- | :- | :- |
| Pro Micro socket | 1-2x | either 1x 24-pin wide or 2x 12-pin single-row |
| Screen | 1x | either nice!view or SSD1306 128x32 OLED |
| Screen socket | 1x | 5-pin |
| Screen cover | 1x | dxf file (coming soon) |

[^1]: 8mm is recommended and will result in equal spacing between top plate, PCB and bottom plate. 7mm can be used for the lowest possible profile, however it is only compatible with Kailh sockets - Gateron sockets slightly thicker.

# Tools

Required:

- Soldering iron/station (+ solder, flux, etc.)
- Screwdriver for the screws
- Side cutters (regular wire cutters will do in a pinch)

Optional (but very recommended):

- Tweezers (preferably reverse ones, for placing diodes & sockets)
- Breadboard (for aligning ProMicro pins)
- Tape (for holding components in place)

Safety measures:

- Fan (for blowing solder fumes away from your face)
- Eye protection (for trimming pins)

# PCB & plates fabrication

Upload the [PCB gerber file](https://github.com/subrezon/lancer/raw/master/gerbers/lancer-pcb-hotswap/lancer-hotswap-pcb.zip) to a PCB manufacturer site like JLCPCB or PCBWay. You can keep settings at default and just pick the color.

If you want FR4 plates, upload [top plate](https://github.com/subrezon/lancer/raw/master/gerbers/lancer-top-plate/lancer-top-plate.zip) and [bottom plate](https://github.com/subrezon/lancer/raw/master/gerbers/lancer-bottom-plate/lancer-bottom-plate.zip) gerbers in the same fashion. If you want plastic or metal plates, use [top plate](https://github.com/subrezon/lancer/raw/master/dxf/top-plate.dxf) and [bottom plate](https://github.com/subrezon/lancer/raw/master/dxf/bottom-plate.dxf) dxf files for cutting.

# Build guide

[Here is a WIP build guide in english](https://github.com/subrezon/lancer/blob/master/docs/build-guide.md). Feel free to submit better photos or translations!

# Firmware

Lancer supports all 3 major firmwares: QMK, ZMK and KMK.

Lancer support in QMK and KMK has been merged into their respective official repositories.

ZMK is user config repository only. Merging into official ZMK repository is currently not planned.

## QMK

The keyboard ID is `subrezon/lancer` in QMK.

Here is an example of flashing the keyboard with the default firmware using the QMK CLI:

```
qmk flash -kb subrezon/lancer -km default
```

If you're unsure what to do with this information, check out the [QMK Documentation](https://docs.qmk.fm/#/) for information on how to get started with QMK.

- I currently do not offer VIA support.
- QMK currently does not support nice!view E-Ink screens.
- If you want to use an SSD1306 OLED, [read this](https://docs.qmk.fm/#/feature_oled_driver) to make it work. The default firmware does not feature any screen support.
- The default firmware is set up for oldschool atmega32u4-based Pro Micros with the caterina bootloader. If you're using an STM or RP2040-based board, you will need to set CONVERT_TO accordingly in your keymap's rules.mk file. [Read this](https://docs.qmk.fm/#/feature_converters?id=converters) for further information.

## ZMK

You can use [this ZMK user config repository](https://github.com/subrezon/zmk-config-lancer) to build ZMK firmware for Lancer. You can:

- Download pre-built firmware from that repository. It is configured for nice!nano v2 and uses the default keymap.
- If you wish to change the keymap and/or use an MCU board other than nice!nano v2, fork that repository and edit the files to suit your needs. The keymap is under `config/boards/shields/lancer/lancer.keymap`.
- If you already have a ZMK user config repository, you may integrate the contents of that repository into your own. Copy the `config/boards/shields/lancer` directory into your repository, then edit your build.yaml to include Lancer:

```
---
include:
  - board: your_other_board
    shield: your_other_shield
  - board: nice_nano_v2
    shield: lancer
```

If you are using an MCU board other than nice!nano v2, change the `nice_nano_v2` board identifier to whatever your board's identifier is. You can find supported boards and their respective identifiers [here](https://zmk.dev/docs/hardware#pro_micro).

If you're new to ZMK, check out the [ZMK documentation](https://zmk.dev/docs) on how to get started.

Note: I might get around to get Lancer officially supported in ZMK main repo, but I feel like Lancer would need to become at least moderately popular first to justify the work. A public user config repo will do for now.

## KMK

To install KMK firmware on your Lancer, follow these steps:

- Download the latest release of [CircuitPython](https://circuitpython.org/downloads) for your MCU board.
- Connect your MCU board to the computer and put it into flashing mode, usually by double-tapping RESET (non-RP2040), or holding BOOT and pressing RESET (RP2040)
- A USB storage device will appear. Copy the `adafruit-circuitpython-*.uf2` you just downloaded onto it and wait. The board will reboot and appear again as a USB storage device named `CIRCUITPY`.
- Download or clone the [KMK Firmware Repository](https://github.com/KMKfw/kmk_firmware). Copy the `kmk` folder and the `boot.py` file onto the MCU.
  - If you use a nice!nano or another MCU board with only 1MB of flash, you will need to [compile the firmware](http://kmkfw.io/docs/Officially_Supported_Microcontrollers#pre-compiling-kmk-for-nicenano) first.
- Delete the `code.py` file, and copy `main.py` and `kb.py` from the `boards/subrezon/lancer` folder.

The `kb.py` file has been set up for nice!nano v2. If you have another MCU board - open the `kb.py` folder and look at line 5. It says:

```
from kmk.quickpin.pro_micro.nice_nano import pinout as pins
```

Change `nice_nano` to match your MCU board. [These ones are supported](https://github.com/KMKfw/kmk_firmware/tree/master/kmk/quickpin/pro_micro).

If yours isn't in the list, you will have to edit the board's pinout yourself.

# Known issues

- The two southmost screws were placed below the middle of switches 4 and 7 of the third row. Unless you're using screws with very small screw heads, they need to be unscrewed before pulling out those two switches. Fixing this would be a plate layout change, so this will likely never be fixed to maintain compatibility between plate/PCB revisions.

# Changelog
- v1.1: first minor revision (latest version, not tested yet)
  - Screen socket moved 1.27mm to the south to make installing a battery underneath the MCU board easier. Hopefully 1.27mm is enough, otherwise it will be move even further away in the next revision.
  - North-facing footprints in thumb cluster, most people install their thumb keycaps upside down, so to maintain south-facingness switches had to be turned 180 degrees as well.
  - Added "ON" and "OFF" silkscreening on the PCB's top side to indicate how the power switch operates.
- v1.0: initial release version (tested, verified working)

# Coming soon

- Acrylic screen cover
- Soldered PCB option
- 3D-printable case options

# Special thanks

- ai03 - for the [MX_V2](https://github.com/ai03-2725/MX_V2) footprint library
- The fabulous mechanical keyboard community - for, well, everything!

# License

This hardware is licensed under the MIT License. You may use it in any way you want.
