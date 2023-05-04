# Build guide

This guide is very detailed and will describe the most efficient way of building the Lancer keyboard. As such, this guide assumes you're right-handed. If you hold the soldering iron with your left hand, mirror the steps for diode and socket soldering - do left pads first, then right pads.

Some photos are missing for now, I'll add them at a later point in time.

#

# Diodes

Start by placing your PCB face-down on your working surface. Heat up your soldering iron.

TODO

Locate the diode footprints, this is what they look like:

TODO

The line marking on the diode shows its orientation. The side with the line is called cathode. You must place them so that the arrow marking on the PCB points towards the cathode. All arrows point towards the center of the board, solder all diodes with their cathodes facing the center.

Put a dab of solder on the right pad of all 36 diode footprints. Then pick up a diode using tweezers, reflow the solder by holding the soldering iron up to it, place the diode in the correct position, and continue holding it in place as you pull away the soldering iron, allowing the solder to solidify again. Repeat this 35 more times.

Now that all 36 diodes are soldered by one leg, let's solder the others. Turn the board 180 degrees, now the unsoldered pads are all comfortably on the right. Solder the remaining 36 pads. This is what the final result should look like:

TODO

# Hotswap sockets

Turn the board back around 180 degrees. Locate the hotswap socket footprints, this is what they look like:

TODO

Tin the right pad of each footprint, it should look like a comfy pillow. Then place a hotswap socket on the footprint, making sure that the socket pins match up with the holes in the PCB. Then, start heating the pad again, while pushing the right contact into the melted solder using tweezers. Once the socket is completely inserted, hold the soldering iron for a couple of seconds to make sure the solder makes good contact, then let it cool and solidify. Repeat 35 more times.

Now that all 36 sockets are soldered by one contact, let's solder the others. Turn the board around 180 degrees, now the unsoldered contacts are all comfortably on the right. Solder the remaining 36 contacts, making sure to use enough solder and to hold the soldering iron for a bit to make sure the solder makes good contact. This is what the final result should look like:

TODO

# Power switch

This step is required for wireless boards, however I recommend you solder it now even if you don't currently plan to use wireless controllers. It's easier to do this without a Pro Micro installed.

Place the power switch on the footprint found at the top center of the board's back side. Put a bit of solder on the tip of your iron, and while holding the switch in place using tweezers, tack any 2 pins in place. After that, solder the remaining pins. This is what the final result should look like:

TODO

# Pro Micro (without socket)

Grab your Pro Micro along with its pin headers:

If you have a breadboard - stick the headers into it (shorter pins go in), then put your Pro Micro in as flush as possible, then trim the longer pins so that they barely stick out. MAKE SURE TO WEAR EYE PROTECTION WHILE TRIMMING PINS!!! It should look like this:

TODO

Now solder the pins to the Pro Micro. The final result should look like this:

TODO

If you don't have a breadboard - you'll need to tape the headers to the Pro Micro somehow, or hold it in with one hand while soldering with another. Or just get a breadboard, it's very useful and usually costs under $2.

# Pro Micro (with socket)

If you want to use a socket - stick the socket into the breadboard. Put tape over the socket to prevent solder from flowing into the socket when soldering the pins. Stick the pins through the tape into the socket, then put the Pro Micro in. Trim the pins if they're too long. Again, WEAR EYE PROTECTION WHILE TRIMMING PINS!!! It should look like this:

TODO

Solder in the pins. Take the Pro Micro out of the socket, remove the tape from the socket and put the Pro Micro back into the socket. Insert the socketed Pro Micro into the PCB from the top, making sure it's fully in. Now tape it down firmly and flip the PCB around. Solder the socket pins and then remove the tape. The result should look like this:

TODO

# OLED / nice!view / socket

Insert a screen, socketed or not, into the top of the PCB and tape it down firmly. Solder the pins, the result should look like this:

TODO

# Reset button

Put the reset button in from the top, flip the board and solder the pins. The result should look like this:

TODO

# Final assembly

The PCB is done. Now let's assemble the board. Screw the 8x M2 standoffs into the top plate using M2 screws:

TODO

Now insert 8 switches into these positions:

TODO

Then, put the plate and switches into the PCB. After that, insert the rest of the switches:

TODO

Flip the board around and put the bottom plate in place. Screw it into the standoffs and put rubber feet in these positions:

TODO

Flip the board back around and put on the keycaps:

TODO

# Flashing firmware

Consult the readme for the firmware you wish to install. If you're unsure which to use - go with QMK.

QMK is a very mature and reliable firmware, basically the industry standard. It is also your only option for AVR microcontrollers like the atmega32u4 found in most Pro Micros. It's a good start if you're new to custom keyboards. However, it has very wireless support.

ZMK is a more modern firmware based on Zephyr RTOS, with great wireless support. However, it requires a 32-bit microcontroller, so no AVR support. Use this if you have an ARM-based Pro Micro board (STM, RP2040, etc.)

KMK is the newest kid on the firmware block. While it requires powerful microcontrollers with CircuitPython support, it is very feature rich and extremely easy to reconfigure, not requiring any flashing after the first time. Use this if you want to reconfigure your board on the go without DFU or other dev tools.