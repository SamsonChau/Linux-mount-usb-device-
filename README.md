# Linux-mount-usb-device-
Useful way to mount the USB device port in linux
1) Change “rgb” named usb camera to a new one.

Since opening usb port will always encounter the changing port issue:
Go to /etc/udev/rules.d/

Assuming you dont have 99-rgb.rules there already,

create a new 99-rgb.rules,

use lsusb to identify the product id and vendor id of the usb device:
e.g. Bus 003 Device 034: ID 046d:c016 Logitech, Inc.
046d = vendor id
c016 = product id

Then, put this in the new created rules


SUBSYSTEMS=="usb", ATTRS{idVendor}=="vendor_id", ATTRS{idProduct}=="product_id", SYMLINK+="rgb"


SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", ATTRS{idVendor}=="vendor_id", ATTRS{idProduct}=="product_id", SYMLINK+="rgb"

save and do this

sudo service udev restart
sudo /etc/init.d/udev restart
