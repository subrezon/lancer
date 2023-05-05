# Lancer

The Lancer is a 36-key ortholinear keyboard with a light split and a focus on compact footprint and portability. It is a direct successor to [la_nc](https://github.com/subrezon/la_nc), and is very much inspired by other keyboards like Planck, Lumberjack and Lesovoz.

TODO photo

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

# Build guide

Here is a build guide in english. Feel free to submit better photos or translations!

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

Under construction.

## KMK

Under construction.

# Changelog

- v1.0: initial release version (current version)

# Coming soon

- ZMK and KMK support
- Soldered PCB option
- 3D-printable case options

# Special thanks

- ai03 - for the [MX_V2](https://github.com/ai03-2725/MX_V2) footprint library
- The fabulous mechanical keyboard community - for, well, everything!

# License

This hardware is licensed under the MIT License. You may use it in any way you want.
