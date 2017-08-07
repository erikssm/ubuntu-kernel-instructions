# How To Update Linux Kernel On Ubuntu

This article describes process of updating Linux kernel to newer version on
Ubuntu.

**Warning!** These instructions might break things so use them at your own risk.

## Installing New Kernel

To update kernel please follow these steps:
- download kernel from here http://kernel.ubuntu.com/~kernel-ppa/mainline/
    * you will need header files ("all", files for your architecture i.e.
    "amd64", generic and "extra" if exist), generic image file for your architecture + "extra" file if it exists
- login as root (sudo -i)
- install the kernel by running "dpkg -i \*.deb"
- update grub: "update-grub2"
- reboot your PC and make sure the new kernel version works as expected

## In Case of Issues

In case of any issues you can always reboot your pc using the previous kernel
version by holding ALT key while your PC is starting up and selecting the
previous kernel in grub startup menu. At this point you can login as root and
uninstall the previously kernel version. Don't forget to update grub afterwards.

## NVIDIA Drivers

If you have proprietary NVIDIA drivers installed you will also need to reinstall
these by following steps below:
- download latest NVIDIA driver for your gpu
- make sure your PC boots with the new kernel
- login as root and run the following commands:
    * ./NVIDIA-Linux-x86_64-DRIVER_VERSION.run -a
    * update-initramfs -k $(uname -r) -u
    * reboot
- once rebooted make sure the new driver works as expected

## Restoring The Default NVIDIA Driver Package

To restore the default drivers please follow these steps:
- remove any manually installed drivers by running installer used with
--unistall parameter
- run the following commands to reinstall default driver package:
    * sudo apt remove --purge nvidia*
    * sudo apt install nvidia-<LATEST_VERSION_HERE>-updates -y
