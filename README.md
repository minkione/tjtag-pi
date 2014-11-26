tjtag-pi2 is a slightly modified version of [tjtag-pi][tjtag-pi] which adds support for the nTRST pin used on some devices.

Tested on an Atheros AR531X board with EJTAG 2.6 interface - works fine, both the device and the flash chip is detected through the JTAG interface.

WARNING
=======

Be warned that incorrect usage can lead to a point of no return
situation. Before you do anything besides what is described here, please
do research on how to use this tool. A good starting point is the
excellent and cautionary `guide.pdf` written by the HairyDairyMaid, the
original author. Always backup before flashing.

Requirements
============

 * A Raspberry Pi (I've only tested model B as of late 2013)
 * [Dual female jumper wires][jumper] to connect GPIO pins to the board
 * Pins soldered on the JTAG header of the target device
 * Beverege to enjoy afterward

Setup
=====

 1. Hook up the two boards as per the diagram in `wiring.jpg`
 2. Optionally, bridge GPIO8 pin on the Pi to the nTRST pin on your device
 3. Power up your device
 4. Checkout the code, compile and run it

        $ cd ~
        $ git clone https://github.com/kissg1988/tjtag-pi2.git
        $ cd tjtag-pi2
        $ make pi
        $ ./tjtag -probeonly

    If it gets stuck, try using `/noemw` option.

If at this point, your SoC and flash is recognized, you're all set.
Enjoy your beverage and look for an appropriate guide that explains how
to use tjtag to revive/upgrade your device's firmware.

Notes
=====

 * If you have issues with reliability of your connection, you can slow
   down the speed of _tjtag_ by using `/delay:N` command line option.
   `N` is the amount of time to delay flipping the clock signal. The
   higher the value, the slower the transfer rate.
 * Due to bit-banging nature of the operation of tjtag, various things
   affect the transfer speed. The one with most degrading effect is the
   progress output. Therefore it is recommended to use `/silent` command
   line option and redirect outputs to `/dev/null` (ie using
   `&> /dev/null`), after having made sure everything works OK.

[jumper]: http://www.seeedstudio.com/depot/1-pin-dualfemale-jumper-wire-100mm-50pcs-pack-p-260.html?cPath=44
[tjtag-pi]: https://github.com/oxplot/tjtag-pi/
[pi]: http://www.raspberrypi.org/
