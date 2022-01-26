pps-gen-gpio
============

Linux kernel PPS generator using GPIO pins.

In kernel 5.4 there is no support for using a GPIO pin as a PPS generator, only a GPIO PPS client is available. This driver is derived from the current parallel port PPS generator and provides a PPS signal through a GPIO pin specified in the device tree. The PPS signal is synchronized to the tv_sec increment of the wall clock.

We have tested the driver with kernel 5.4.152 on a Beaglebone Black where P9 pin 16 (GPIO1_19) is used as PPS output. The corresponding modified device tree file is here shown.

Usage
-----
If you want to change the output pin, update the device tree overlay file accordingly.

Please note that in order to use the module with any other board using the device tree infrastructure, the following matching definitions are required in the device tree:

		pps-gen               node defined for the PPS GPIO
		pps-gen-gpio          value of ".compatible" property in pps-gen node
		pps-gen-gpio          property in pps-gen node that defines which GPIO pin is used

After modifying the device tree, add the files into drivers/pps/generators and configure the driver to be built as a module. You need to enable PPS support in the kernel.
