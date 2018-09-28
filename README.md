# N552VWHackintosh
Mojave 10.14 Setup Instructions

*Step 1: Install Clover Bootloader & Copy EFI Files*

* Clover
* config.plist

Notes:
 - DSDT.aml may be different as it is unique to bios version and model of computer

* DSDT.aml may be different as it is unique to bios version and model of computer

 - Spoof SSDT is important for disabling the NVIDIA graphics as they won't allow for booting and will never work anyway

*Step 2: Copy Hackintosh related applications to Applications folder*

*Step 3: Setup Audio*
No DSDT patch method:

1. Run appleHDA patcher for laptop 255
2. copy clover patches and inject audio id 2 for Mojave 3 for High Sierra in clover / ignoring dsdt files
3. Make backup of appleHDA.kext in /System/Library/Extensions
4. install full patched appleHDA codec commander and HDAEnabler with kext utility
5. Reboot!

Dummy Method:
Copy to EFI/Clover/Kexts 

* aDummyHDA.kext
* CodecCommander

1. Run appleHDA patcher for laptop 255
2. Copy Clover patches and layout id from mironeaudio to config.plist
3. Check acpi options in config.plist AddDTGP and FixHDA
4. Patch DSDT with IRQ & HDEF


*Step 4: Setup WiFi and Bluetooth*
Install Kexts

* BrcmFirmwareRepo.kext
* BrcmPatchRAM2.kext
* FakePCIID_Broadcom_WiFi.kext
* FakePCIID.kext

Add patches to KextToPatch in clover config.plist

*Step 5: Enable Graphic Acceleration*


1. set screen resolution to 1920x1080
2. Copy kexts to EFI/Clover/Kexts
3. With 0x12345678 fake id and no value for ig-platform-id  do the following terminal command and reboot

 sudo kextcache -i /

1. Remove Fake id from plist by using 0x0 and add 0x19160000 to the plist
2. Reboot and you have accelerated graphics! 1536 MB


*Step 6: Enable Battery Status*

1. Install kext: ACPIBatteryManager.kext
2. Apply included patch to DSDT

*Step 7: Enable Trackpad*

* Install all DSDT patches in folder with specific windows version laptop shipped with “windows 10”
* Install all kexts in folder



