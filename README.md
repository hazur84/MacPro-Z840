# HP840 + MacPro = The MacProZ840
 HP Z840 Workstation - 2x 8-Core Intel Xeon E5-26XX - 64GB RAM - AMD Radeon RX560 

# Custom MacPro HP Z840 Workstation Hackintosh Guide

This is a complete installation guide to install macOS Mojave 10.14.6 on your custom built hardware featuring 64GB RAM paired with 2x 8-Core Intel Xeon E5-26XX and SSD 960 GB. The purpose of this guide is to provide a step-by-step guide to install Mojave using Clover UEFI.

## Introduction: 

This Workstation for extreme application used to be a Beast with Dual CPUs and a lot of of RAM (64 GB), I Know it is now normal to get that much cores in a Desktop but it is still a very decent machine for me (As a Programmer), and I thought it would be a good idea to Install MOJAVE MacOS 10.14.6 as the Daily Driver also. 

## Specifications

- Motherboard: HP Z840
- Chipset: 
- CPU: 2x 8-Core Intel Xeon E5-26XX 
- RAM: 64 GB DDR4 XXXXMHz ECC Memory
- Ethernet: 
- Audio: 
- PSU: XXXX Watts 

# Hardware upgrades

1. WIFI: Fenvi FV-HB1200 Broadcom 94360CS2 Wifi/Bluetooth PCI Adapter AC 1300mb/s
1. Optival Drive: COMBO DVD-RW + Bluray ROM
1. Graphics: GIGABYTE AMD Radeon RX560 4GB; output 4k monitors (DVI, HDMI and Display port)
1. Monitor: LG SMART TV OLED 4K 55"
1. HD: ADATA SATA 960GB SSD
1. Keyboard: Apple USB (A1243)
1. Mouse: Apple Magic Trackpad 2 (A1535)

## Working

## Not Working

# HP Z840 Workstation Resources

- User Guide [PDF](http://h10032.www1.hp.com/ctg/Manual/c04823811)
- Quick Specs [PDF](https://h20195.www2.hp.com/v2/getpdf.aspx/c04400043.pdf)
- Maintenance and Service Guide [PDF](http://h10032.www1.hp.com/ctg/Manual/c04823811)

## Install a Supported Graphic Card Out Of The Box (OOB)

### Supported Nvidia Kepler Graphics Cards

Most people know that Nvidia has never released Web drivers for Mojave. What you may not know is that there is still support for many Nvidia Kepler cards right within Mojave. No drivers need to be installed for these cards to work in either High Sierra or Mojave. We don't know how long support will last for these but as of today they are fully supported.

The Following Cards are all Mojave and Catalina compatible:

**Kepler Gen 2:**
GTX 770,
GTX 760/ti,
GT 740,
GT 730,
GT 720,
GT 710

**Kepler Gen 1:**
GTX 680,
GTX 670,
GTX 660/TI(MUST BE RUNNING A GK 104 core, NOT GK 106),
GTX 650(MUST BE RUNNING A GK 107 core, NOT GK 106),
GTX 645(GT 645 is Fermi),
GT 640(Kepler edition, GK 107/208 core),
GT 630(Kepler edition, GK 208 core).

**Quadro:**
Quadro 410,
Quadro K420,
Quadro K600 Card (4K at 60Hz via DisplayPort, is the cheapest 4k),
Quadro K2000/D,
Quadro K4000/D,
NVS 510.

### Supported ATI graphics cards RX 5XX series.

RX 550,
RX 560 (Best option relaible, not require power connector),
RX 570,
RX 580 (NITRO SAPPHIRE),
RX 590 (NITRO SAPPHIRE).


## Preliminary Steps

1. Replace the Existing Thermal Paste on the CPU IHS (Integrated Heat Spreader)
Even if you bought your Dell from a professional refurbisher, it's highly unlikely that they took the time to replace the thermal compound between the CPU and heatsink. After four or five years, it needs to have the old compound removed and a fresh coat applied. Use 99% isopropyl alcohol and some guaze pads to remove it. Then apply some new paste like the Arctic MX4 which is available on Amazon or Newegg. If you don't have experience doing this look for some online video tutorials that show you how. A new coat of thermal paste will help keep temps much lower when you are pushing your CPU during gaming or video/photo editing.

1. Replace the CMOS Battery
These Dell Optiplex PCs are about 5 years old and may have sat on a shelf for two years unplugged from power. When Lithium batteries stay in a fully discharged state for long periods it greatly reduces their ability to hold a charge. My 9020 MT model had a battery like this. I kept getting a black screen at boot up. Was not able to even access the BIOS until I removed the battery for a minute and reseated it. I had checked the battery with a multimeter and it read 3.0v. Should be good right ? Even if it reads 3.0 volts it still may not be able to provide adequate voltage under load. When I test new CR2032 batteries the reading is often from 3.4 to 3.5 volts. That's how a good battery should test out.

Replace yours with a fresh new one before you make the BIOS changes in Step #2. Once you remove it from your board, all BIOS setting changes will be lost and you'll have to reapply them. Link to amazon to purchase a 2 pack is found above.
source: https://www.computerhope.com/issues/ch000239.htm

1. Remove any Add in Cards
If your Dell has any kind of wireless adapter installed (USB, PCIe or Mini PCIe) remove it before attempting the installation of macOS. Use Ethernet until after you've got everything else working properly. Then you can work on Wifi function after that. If you have a supported Broadcom card like the Fenvi FV-HB1200 you can keep that in a PCIe Slot during initial install.


## Step 1. Create your Mojave Unibeast Installer
Download Mojave from the Mac App Store on a Apple computer or whatever Hackintosh with Mojave OS.x

## If you don't have access to a Mac capable of making the Unibeast Installer

Create your UniBeast installer by following the standard tonymacx86 guide. Use a 16 or 32GB USB flash drive. Anything larger than 32GB in size must be partitioned to less than 32GB. Use UniBeast for Mojave only. Version 9.2.0.

There is one critical step to remember when formatting your USB or other drives in Disk Utility. Always click View and then Show All Devices instead of leaving it at "Show Only Volumes" when using High Sierra or Mojave to make the installer. After you select the Parent name, click on the Erase tab and format the USB as directed in the tonymacx86 guide.

Once creation of the UniBeast installer has completed, you will need to replace the UniBeast created config.plist with the custom one attached below. Do this before ejecting the UniBeast installer or you'll have to mount the EFI manually later. Now go to Finder -> Preferences and then select the "Show Hard Disks on the Desktop" option.

A. There will be an external drive on your desktop that represents the UniBeast USB's EFI partition
B. Double click that EFI drive icon to open it up and reveal the EFI folder on that partition
C. Now open the Clover folder inside of that EFI folder
D. Download the Custom Clover config.plist (zip file) Attached below
E. Delete the existing config.plist and then add in the new Custom one you just downloaded
F. Open up the kexts/other folder and drag and drop the release version USBInjectAll.kext into that folder
G. Download "SSDTs" zip file from the end of this post and place those files in the /Clover/ACPI/patched folder
H. Add the HFSPlus.efi driver to the Drivers64-UEFI folder. This is also attached below.

## Step 2. Update BIOS to last available 

1. Donwload the latest BIOS version.

BIOS 2.50 Rev.A Nov 12,2019 [link](https://ftp.hp.com/pub/softpaq/sp100001-100500/sp100084.exe) Install over Windows 10 (64-bit)

1. Flashing te BIOS to a newer Revision

## Step 3. Recommended BIOS Settings

If you're installing on a recommended CustoMac desktop with AMI UEFI BIOS, the options are simple. For other systems make sure to set your BIOS to Optimized Defaults, and your hard drive to AHCI mode. Here are standard AMI UEFI BIOS settings for
Gigabyte AMI UEFI BIOS, Gigabyte AWARD BIOS, ASUS AMI UEFI BIOS, and MSI AMI UEFI BIOS.

1. To access BIOS/UEFI Setup, press and hold Delete on a USB Keyboard while the system is booting up
1. Load Optimized Defaults
1. If your CPU supports VT-d, disable it
1. If your system has CFG-Lock, disable it
1. If your system has Secure Boot Mode, disable it
1. Set OS Type to Other OS
1. If your system has IO Serial Port, disable it
1. Set XHCI Handoff to Enabled
1. If you have a 6 series or x58 system with AWARD BIOS, disable USB 3.0
1. Save and exit.

## Step 4. FUll patched DSDT

It's fully described here how to patch the DSDT. **NOTE: You can NOT use my patched DSDT.aml or anyone's else. You must do it yourself!** Short story:

1. Boot into Clover. Press F4 and then boot into macOS.
1. Clone iasl to a folder of your choice (git clone https://github.com/RehabMan/Intel-iasl iasl).
1. make && sudo make install to build and put the binary at the default path for binaries.
1. Download the latest MaciASL from here.
1. Mount the EFI partition and copy over the .aml files in EFI/CLOVER/ACPI/origin that start with DSDT or SSDT to a new folder somewhere.
1. Run iasl -da -dl DSDT.aml SSDT*.aml in that directory.
1. Open MaciASL and open the outputted DSDT.dsl.
1. Apply patches. In my case, I wanted proper sleep (it was waking up by USB events):

 into_all method label _PRW  remove_entry;
 into_all all code_regex Name.*_PRW.*\n.*\n.*\n.*\n.*\}\) remove_matched;
 
1. Save as ACPI Machine Language Binary to EFI/CLOVER/ACPI/patched/DSDT.aml.
1. Reboot.

You might find other issues that you want to patch. Good luck!

# BENCHMARKING

