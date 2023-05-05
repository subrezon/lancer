# Enabling OLED support

Lancer supports a nice!view E-Ink screen, and through a happy little accident the leftmost 4 pins of the 5-pin SPI header match the pinout of an SSD1306 OLED screen. You can use those if you so desire, however I don't offer any support and you will have to set it up yourself. Here are a couple pointers on how to do that:

# Create a new keymap in QMK

Create a new keymap in QMK:

```
qmk new-keymap -kb subrezon/lancer -km my_oled_keymap
```

# rules.mk

Add the following lines at the end of `rules.mk` in your keymap folder (if the file isn't there - create it):

```
OLED_ENABLE = yes
OLED_DRIVER = SSD1306
```

# keymap.c

The default keymap is data-driven and not implemented in C code. As far as I know, this way of doing things isn't compatible with OLEDs.

First, delete the `keymap.json` file from your keymap. Then, create a `keymap.c` file. You will need to implement your keymap there, and then add your OLED code at the end. It should look something like this:

```
#include QMK_KEYBOARD_H

const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {

	// your keymap

};

#ifdef OLED_ENABLE

bool oled_task_user(void) {
	oled_write_P(PSTR("Layer:\n"), false);

    switch (get_highest_layer(layer_state)) {
    	case 0 :
            oled_write_P(PSTR("QWERTY\n"), false);
            break;

        case 1 :
            oled_write_P(PSTR("Numbers\n"), false);
            break;

        case 2 :
            oled_write_P(PSTR("Symbols\n"), false);
            break;

        case 3 :
            oled_write_P(PSTR("Options\n"), false);
            break;

        default :
        	oled_write_P(PSTR("Undefined\n"), false);
    }

    return false;
};

#endif
```

For further pointers, checkout out the QMK documentation, namely [this page](https://docs.qmk.fm/#/keymap) about C keymaps and [that page](https://docs.qmk.fm/#/feature_oled_driver) about configuring OLEDs.
