Mojave 10.14 Setup Instructions

*Step 1: Install Clover Bootloader & Copy EFI Files*

* Clover
* config.plist

Notes:
- DSDT.aml may be different as it is unique to bios version and model of computer

* DSDT.aml may be different as it is unique to bios version and model of computer

- Spoof SSDT is important for disabling the NVIDIA graphics as they won't allow for booting and will never work anyway
https://www.tonymacx86.com/threads/ssdt-gpu-graphics-card-injection.183354/

*To obtain and disassemble DSDT and other ACPI tables*
Press f4 in clover to get ACPI tables in EFI/Clover/ACPI/Origin
Copy Origin folder to desktop
Copy refs.txt to Origin 
Copy iasl binary to /usr/bin from current directory:
sudo cp iasl /usr/bin
Run script to decompile ACPI Tables:
iasl -da -dl -fe refs.txt DSDT.aml SSDT*.aml
//Make edits with the latest MaciASL!

*Step 2: Copy Hackintosh related applications to Applications folder*

*Step 3: Setup Audio*
//Some steps may not be entirely necessary but these are the steps that I followed to make stable working audio 
AppleALC.kext method
Apply DSDT patches in MaciASL

* IRQ
* HPET

Apply Clover patches
ACPI>DSDT patches
press +
Add Patch Comment: Rename HDAS to HDEF Find: 48444153 Replace: 48444546
Select fixes

* AddDTGP_0001
* FixHDA_8000

Devices>Audio

* Inject 13
* Select ResetHDA

Copy AppleALC.kext to EFI/Clover/Kexts/Other
Install CodecCommander.kext with Kext Utility
Reboot!

-Dummy Method (Working on High Sierra):-
-Install kexts with kextutility System/Library/Extensions-

* -aDummyHDA.kext-
* -CodecCommander-

1. -Run appleHDA patcher for laptop 255-
2. -Copy Clover patches and layout id from mironeaudio to config.plist-
3. -Check acpi options in config.plist AddDTGP and FixHDA-
4. -Patch DSDT with IRQ & HDEF-


*Step 4: Setup WiFi and Bluetooth*
Install Kexts

* BrcmFirmwareRepo.kext
* BrcmPatchRAM2.kext
* FakePCIID_Broadcom_WiFi.kext
* FakePCIID.kext

Add patches to KextToPatch in clover config.plist

*Step 5: Enable Graphic Acceleration*


1. set screen resolution to 1920x1080
2. Copy kexts (IntelGraphicFixup & Lilu & CoreDisplayFixup) to EFI/Clover/Kexts
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



