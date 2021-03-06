Exar USB Serial Driver
======================
Version 1A, 1/9/2015

This driver will work with any USB UART function in these Exar devices:
	XR21V1410/1412/1414
	XR21B1411
	XR21B1420/1422/1424
	XR22801/802/804

The source code has been tested on various Linux kernels from 3.6.x.  
Tested and working with kernel 5.13.  


Installation
------------

* Compile and install the common usb serial driver module

	# make
	# insmod ./xr_usb_serial_common.ko

* Alternativley install via DKMS
	# cp -a ../xr_usb_serial_common-1a /usr/src/
	# dkms add -m xr_usb_serial_common -v 1a
	# dkms build -m xr_usb_serial_common -v 1a
	# dkms install -m xr_usb_serial_common -v 1a

* Ensure that the cdc-acm module/xr_serial is not loaded (assumig that it is not needed):
	Example:
	# echo blacklist cdc-acm > /etc/modprobe.d/blacklist-cdc-acm.conf 
	# update-initramfs -u

* Plug the device into the USB host.  You should see up to four devices created,
  typically /dev/ttyXRUSB[0-3].


Tips for Debugging
------------------

* Check that the USB UART is detected by the system

	# lsusb
	similar to this > Bus 004 Device 003: ID 04e2:1411 Exar Corp. XR21B1411

* Check that the CDC-ACM driver was not installed for the Exar USB UART

	# ls /dev/tty*

	To remove the CDC-ACM/xr_serial  driver and install the driver:

	# rmmod cdc-acm / rmmod xr_serial 
	# modprobe -r usbserial
	# modprobe usbserial
	# insmod ./xr_usb_serial_common.ko


Technical Support
-----------------
Send any technical questions/issues to uarttechsupport@exar.com. 

