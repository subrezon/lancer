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
| PCB | 1x | Gerber file |
| Top plate | 1x | Gerber for FR4, dxf for other materials|
| Bottom plate | 1x | Gerber for FR4, dxf for other materials |
| Pro Micro | 1x | other boards with compatible pinout also work |
| SMD Diodes | 36x | 1N4148W SOD123 |
| Hotswap sockets | 36x | Kailh or Gateron |
| Tactile button | 1x | 3x6mm 2-pin button |
| M2 screws | 16x | M2x4 or M2x5, head diameter <5mm |
| M2 standoffs | 8x | 7mm for lowest profile, 8mm for equal plate spacing |
| MX-style switches| 36x | 3-pin or 5-pin |
| 1U MX keycaps | 36x |  |

For wireless operation:

| Item | Count | Notes |
| :- | :- | :- |
| Wireless Pro Micro | 1x | nice!nano, nrfmicro, etc. |
| Rechargeable battery | 1x | usually 3.7V two-wire battery like 350926 |
| 7-pin SPDT switch | 1x | MSK-12C02 or compatible |

Optionally:

| Item | Count | Notes |
| :- | :- | :- |
| Pro Micro socket | 1-2x | either 1x 24-pin wide or 2x 12-pin single-row |
| Screen | 1x | either nice!view or SSD1306 128x32 OLED |
| Screen socket | 1x | 5-pin |
| Screen cover | 1x | dxf file |

# PCB & plates fabrication

Upload the [PCB gerber file](https://github.com/subrezon/lancer/raw/master/gerbers/lancer-pcb-hotswap/lancer-hotswap-pcb.zip) to a PCB manufacturer site like JLCPCB or PCBWay. You can keep most settings at default.

If you want FR4 plates, upload [top plate](https://github.com/subrezon/lancer/raw/master/gerbers/lancer-top-plate/lancer-top-plate.zip) and [bottom plate](https://github.com/subrezon/lancer/raw/master/gerbers/lancer-bottom-plate/lancer-bottom-plate.zip) gerbers in the same fashion. If you want plastic or metal plates, use [top plate](https://github.com/subrezon/lancer/raw/master/dxf/top-plate.dxf) and [bottom plate](https://github.com/subrezon/lancer/raw/master/dxf/bottom-plate.dxf) dxf files for cutting.

# Build guide

Here is a WIP build guide in english. Feel free to submit better photos or translations!

# Firmware

Only QMK is currently officially supported. I'm actively working to provide ZMK and KMK support.

## QMK

The keyboard ID is subrezon/lancer in QMK. It is currently pending approval in the official QMK repository, you can use my repository for now. I will post an update as soon as it is approved by QMK devs.

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

KMK board files are currently being reviewed for merging into the official KMK repository: https://github.com/KMKfw/kmk_firmware/pull/815. If the pull request hasn't been merged yet - get the files from my [KMK fork](https://github.com/subrezon/kmk_firmware), from the `subrezon/lancer` branch.

To install KMK firmware on your lancer, follow these steps:

- Download the latest release of [CircuitPython](https://circuitpython.org/downloads) for your MCU board.
- Connect your MCU board to your computer and put it into flashing mode, usually by double-tapping RESET (non-RP2040), or holding BOOT and pressing RESET (RP2040)
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

- The screen socket is a little too close to the Pro Micro, so there is very little space to install a battery underneath the Pro Micro. It is still possible, but requires a little too much fuss to get it right. This will be fixed in v1.1 by moving the socket 1.27 mm to the south.
- Most people install their thumb keycaps upside down, so the thumb row sockets would have to be reversed to maintain south-facingness. This will be fixed in v1.1, the electrical layout will remain unchanged.
- The two southmost screws were placed below the middle of switches 4 and 7 of the third row. Unless you're using screws with very small screw heads, they need to be unscrewed before pulling out those two switches. Fixing this would be a plate layout change, so this will likely never be fixed to maintain compatibility between plate/PCB revisions.

# Changelog

- v1.0: initial release version (current version)

# Coming soon

- Acrylic screen cover
- Soldered PCB option
- 3D-printable case options

# Special thanks

- ai03 - for the [MX_V2](https://github.com/ai03-2725/MX_V2) footprint library
- The fabulous mechanical keyboard community - for, well, everything!

# License

This hardware is licensed under the MIT License. You may use it in any way you want.
