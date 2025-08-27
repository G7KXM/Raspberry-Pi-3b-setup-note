# Raspberry-Pi-3b-(maybe pi2 also)-setup-note

This is just to help me with setting up my Pi's

Boot from SSD on USB
use Rapberry Pi Imager to put image onto SSD

Boot Raspian on Pi from SD Card

If never set Pi 3B to boot USB:

sudo apt update && sudo apt upgrade && sudo reboot

echo program_usb_boot_mode=1 | sudo tee -a /boot/config.txt   (it maybe now /boot/firmware/config.txt)

Reboot and the bit is now perminantly set in the Pi's firware to allow usb booting.

In Raspian booted from SD card with your USB boot drive attached to the PI, run the following to find which device the system has allocated to your USB disk, in my case it was /dev/sda, with 2 partitions, sda1 and sda2. 

lsblk

sudo parted /dev/sda print

We now need to resize the 2nd partition to use the remaining space on the disk:

sudo parted /dev/sda resizepart 2 100%

sudo resize2fs /dev/sda2

Shutdown the Pi, remove the SD card and power on the Pi, wait a few seconds and the Pi should now boot from the SSD.
