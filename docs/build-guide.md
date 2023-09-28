# Build guide

This guide is very detailed and will describe the most efficient way of building the Lancer keyboard. As such, this guide assumes you're right-handed. If you hold the soldering iron with your left hand, mirror the steps for diode and socket soldering - do left pads first, then right pads.

Some photos are missing for now, I'll add them at a later point in time.

# Diodes

Start by placing your PCB face-down on your working surface. Heat up your soldering iron.

TODO PHOTO

Locate the diode footprints, this is what they look like:

TODO PHOTO

Put a dab of solder on the right pad of all 36 diode footprints. Then pick up a diode using tweezers with your left hand, reflow the solder with the soldering iron in your right hand, place the diode in the correct position, pull away the the iron and let the solder cool down again, while holding the diode still until it is fixed in place. Repeat 35 more times.

When soldering the first diode pin, focus on positioning the diode well. Because the solder is heated up twice and for a long time, the flux in it burns out, and the joint may look ugly for now, but that can be fixed later.

When placing the diodes, watch the orientation. The side with the line is called cathode. Place the diodes so that the arrow marking on the PCB points towards the cathode. All arrows point towards the center of the board, solder all diodes with their cathodes facing the center!

After soldering all 36 diodes by one pin, solder the others. Turn the board 180 degrees, now the unsoldered pads are all comfortably on the right. Solder the remaining 36 pins.

You can now go back to fix ugly joints from before by just putting some flux onto them and re-heating them briefly.

This is what the final result should look like:

TODO PHOTO

# Hotswap sockets

Locate the hotswap socket footprints, this is what they look like:

TODO PHOTO

Put a dab of solder on the right pad of all 36 socket footprint, it should look like a sofa pillow:

TODO PHOTO

Place a hotswap socket on the footprint, making sure that the socket pins match with the holes in the PCB. Heat the pad again, while pushing the right contact into the melted solder using tweezers. Make sure to push the metal part, not the plastic!

Once the socket is completely inserted, hold the soldering iron for a second or two to make sure the solder makes good contact, then let it cool and solidify. Repeat 35 more times.

After soldering all 36 sockets by one contact, solder the others. Turn the board 180 degrees, now the unsoldered contacts are all comfortably on the right. Solder the remaining 36 contacts, making sure to use enough solder and to hold the soldering iron for a bit to make sure the solder makes good contact. This is what the final result should look like:

TODO PHOTO

# Power switch

This step is only required for wireless boards, however I recommend you solder it now even if you don't currently plan to use wireless controllers. It's easier to do this without a Pro Micro installed, you'll save yourself a lot of hassle if you do ever decide to try out wireless.

Place the power switch on its footprint (top center of the board's back side). Make sure that the two plastic pegs go inside the holes in the PCB and that the pins line up with the pads.

Put a bit of solder on the tip of your iron, and while holding the switch in place using tweezers, tack any 2 pins in place. After that, solder the remaining pins. This is what the final result should look like:

TODO PHOTO

# Reset button

Put the reset button in from the top, flip the board and solder the pins. The result should look like this:

TODO PHOTO

# Pro Micro (without socket)

If you have a breadboard - stick the pin headers into it (with the longer pins side), place your Pro Micro onto the headers as flush as possible. You can optionally trim the pins so that they barely stick out (WHILE WEARING EYE PROTECTION!!!), or leave them as is. Now solder the pins to the Pro Micro. The final result should look like this:

TODO PHOTO

If you don't have a breadboard - you'll need to tape the headers to the Pro Micro somehow, or hold it in with one hand while soldering with another. Or just, like, get a breadboard, they're very useful and usually cost under $2.

# Prepare Pro Micro (with socket)

If you want to use a socket - stick the socket into the breadboard. Put tape over the socket to prevent solder from flowing into the socket when soldering the pins, like this:

TODO PHOTO

Stick the pins through the tape into the socket, then put the Pro Micro onto them. Trim the pins if they're too long (WHILE WEARING EYE PROTECTION!!!). It should look like this:

TODO PHOTO

Solder in the pins. Take the Pro Micro out of the socket and remove the tape from the socket and put the Pro Micro back into the socket.

TODO PHOTO

# Solder Pro Micro & battery

Take your Pro Micro assembly (either with headers directly soldered in or attached to a socket) and place it onto its footprint. If you're going wireless - also place the battery under it now. Make sure everything fits together, fix it in place with tape, turn the board around, then solder in all the pins.

TODO PHOTO

# OLED / nice!view / socket

Insert a screen, socketed or not, into the top of the PCB and tape it down firmly. Solder the pins, the result should look like this:

TODO PHOTO

# Final assembly

The PCB is done. Now let's assemble the board. Screw the 8x M2 standoffs into the top plate using M2 screws:

TODO PHOTO

Now insert 8 switches into these positions:

TODO PHOTO

Then, put the plate and switches into the PCB. After that, insert the rest of the switches:

TODO PHOTO

Flip the board around and put the bottom plate in place. Screw it into the standoffs and put rubber feet in these positions:

TODO PHOTO

Flip the board back around and put on the keycaps:

TODO PHOTO

# Flashing firmware

Consult the readme for the firmware you wish to install. If you're unsure which to use - go with QMK.

QMK is a very mature and reliable firmware, basically the industry standard. It is also your only option for AVR microcontrollers like the atmega32u4 found in most Pro Micros. It's a good start if you're new to custom keyboards. However, it has extremely limited wireless support.

ZMK is a more modern firmware based on Zephyr RTOS, with great wireless support. However, it requires a 32-bit microcontroller, so no AVR support. Use this if you have an ARM-based Pro Micro board (STM, RP2040, etc.)

KMK is the newest kid on the firmware block. While it requires powerful microcontrollers with CircuitPython support, it is very feature rich and extremely easy to reconfigure by just editing files in the keyboard's onboard storage, not requiring any tooling after initial installation. Use this if you want to reconfigure your board on the go without DFU or other dev tools.
