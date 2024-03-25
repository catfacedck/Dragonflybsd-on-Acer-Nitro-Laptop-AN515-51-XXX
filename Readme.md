# Dragonflybsd 6.5 Snapshot Release on Acer Nitro AN515-51-XXX Series Laptops

These laptops typically come in a variety of hardware sku configurations:
  - AMD 7000 and above Ryzen cpus
  - Intel I12/I13/I14 -500/700/900 cpus
  - 165 Hz or 144 Hz display panels
  - AMD Radeon Graphics
  - Integrated Intel Graphics -P GT2 Iris Xe Graphics
  - Nvidia 30XX or 40xx Graphics
  - Integrated Intel WiFi 6 AX2XX series
  - Integrated Mediatek MT7921 WiFi or variants
  - Killer Ethernet (was Realtek now Intel)
  - Realtek and Nvidia Audio
  - Two (2) nvme drive connectors and one (1) SATA drive connector - three (3) internel drives total.

What you will get after installation:
  - Working Ethernet based dragonflybsd system using scfb Xorg driver, 1920x1080 165 Hz screen, mousepad, USB support, audio, mutiple drives.

What does not work:
  - Intel integrated WiFi, Intel integrated Graphics (no drm-61-kmod -> no brightness/screen resolution control), Nvidia Graphics, suspend/sleep keys.

Note: This dragonfly installation was tested on Intel I5-12500 and Intel I7-13700 systems with Integrated Intel Graphics/Wifi, Nvidia 3050/4050 Graphics, and Killer Ethernet.
  

# **_Step-by step intall procedure:_**

Typically these laptops are delived with Windows 11 installed on an internal 500 GB or 1 TB nvme drive. For this install it is far easier to accomplish on a new 2nd drive without the worry of screwing up the base Windows 11 installation. 

However, in order to multiboot from the same or different drives one needs to use rEFind (https://www.rodsbooks.com/refind/).
Here the assumption is two (2) drives: 1 with Windows 11 and 1 with dragonfly (and other) operating systems using rEFind.

1) Prepare the laptop BIOS.
   ```
       Press F2 to enter the BIOS menu when powering the laptop on.
       Turn off UEFI secure boot in the Advanced menu.
       Enable boot menu choices (F12) - also in Advanced menu.
       Press F10 to exit.
   ```
   
2) Change the laptop mousepad from iic to psm protocol. Mousepad iic protocal is not supported. To do so one must enter the BIOS advanced mode. Not planning to use the laptop mousepad? Skip this step.
   ```
   ```
   
3) Go get the dragonflybsd image to copy onto a USB stick from here: https://mirror-master.dragonflybsd.org/snapshots/x86_64/
     ```
     Choose the DragonFly-x86_64-LATEST-BOOT.tar.bz2 file.
     Decompress this and flash to a USB stick. On Windows one can use Rufus (https://rufus.ie/en/) or dd from any Gnu/Linux or BSD system.
     ```

4) Test that the BIOS changes and USB stick are working.
   ```
     Plug in the USB stick and reboot the laptop.
     At power up when the keyboard lights flash, press F12.
     Select the USB stick from the menu to boot from it.
   ```
5) If the boot is successful inspect the dmesg boot log. If unsuccessful go look for the trouble.
   ```
   Do not install the system.
   Select: exit to shell.
   At the command prompt type: dmesg|less
   Inspect the messages to ensure Ethernet was detected as well as the mousepad.
   One must have Ethernet and driver to continue with the installation.
   View all the pci devices and their driver attachments by typing: pciconf -lvv|less
   No pci driver available is indicted by "none"
   ```

6) Install drangonflybsd from the USB stick.

