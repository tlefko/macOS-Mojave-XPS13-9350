# USE THE UPGRADED GUIDE FOR 10.13.6+ IN MY PROFILE

- Hello, this is a simple guide to get OS X 10.14 working on any XPS 13 9350 model

- This guide uses files from (@syscl) (albeit edited) and full credit to him for the Deploy.sh and DSDT patches. However, his Clover folder is unbootable with Mojave and thus has been redone.

- However, his Deploy is still retained but edited to remove some DSDT patches that break things on Mojave

- I did my best to keep the guide simple and for the most part it is, it's inteded for the 6200U non iris but should work with others. (credit @syscl)

# Issues

- Fixed Lidwake Kext
- SD Card slot
- Restarts don't work (endless black screen while turning off but still on)

# Usage Notes

- USB Devices eject upon sleep (USB Patches via Deploy were major issue)
- Changing board number via Clover Config doesn't work always unless serial is changed (No idea..)
- Audio is controlled via VoodooHDA however prefpane is not necessary.
- Never tested USB C anything. Charging should be fine however I'm not sure about others, don't personally use it)


# What Works

- Everything else!

# Setup Notes

- The new AFPS file system must be used, there is no way to avoid it. Has no noticeable adverse effects except slower boot time
- It is difficult to repartition AFPS drives and resize them, recommend clean install or you could have one partition smaller than your hard drive that can't be increased unless reformatted
- Although Volumes will be converted, keep drive as GUID

# BIOS Settings

-  Set all SATA operation as AHCI
- Disable Secure Boot, Fast Boot
- For Coil Whine improvement disable C-States
- Enable UEFI Booting (Disable Legacy if easily confused)

# Recommended: Clean Install (Preinstall steps)

- Download latest Mojave version from Mac App store (Register AppleID as developer, enroll your mac, download the preview from the link onsite or google for detailed instructions.
- Make Bootable media (google how or download app to do it, it's just a terminal command) 
- Download the Latest Clover revision (currently using r4568) and install it to your USB as UEFI and ESP (no need for drivers)
- Copy The contents of this Github repository into your EFI folder on the USB (Mount the EFI Partition via clover config, efi mounter, etc.) (No Boot Folder in EFI)
- If you have the same XPS Model as me you can use stock ACPI patched files (6200u, hd 520, 3200x1800,) if not delete contents of both folders (origin, patched) and will fix later via @syscls modified deploy)

# Installing Mojave (Clean Install)

- Boot PC off the USB, select your Installer as your Boot drive from clover menu
- config is currently set to FAKESERIAL and -v. I believe (@syscl's) deploy generates serial # information
- Once installer is loaded, go to disk utility and format as a GUID Partition Table with whatever partitions you want (Don't format whole drive to afps make sure it's GUID)
- Run the Mojave installer to the drive wait for it to finish, then turn off)
- From Clover, select the name of the Mojave Partition (not preboot, recovery, etc.) and not your USB stick either
- From here the installation will continue. DO NOT CLICK ON MOUSE OR KEYBOARD (crashes installer shortly after at least for me)

# Post Install (Clean Install)

- Reboot off your USB once again, load up your Mojave drive.
- First Boot will take long, if your using my ACPI files (from @sysl's deploy, edited) and have same model you should have everything out of box (except wifi)
- Regardless, run through the installer and set it all up.
- (without acpi) At this point screen should be fine, mouse, keyboard, no wifi should be present or bluetooth. No brightness control as well.
- go to terminal to mount EFI or via clover Config, EFI Mounter, etc, of both USB and the internal disk
- Copy and REPLACE the EFI folder from the USB into your hard drive. Unplug your USB and reboot and you should be able to boot without the USB now
- Turn off PC, boot into clover. Don't select a drive and press F4 and Fn+F4 a few times, wait a few seconds, then boot back to the drive
- Plug back in the USB, mount it's EFI, and run the modified Deploy Script on your Hard Drive EFI partition
- After deploy is finished, there will be VoodooI2C error as I deleted it from Kexts, for me it breaks Trackpad and Keyboard.  For now will be using VoodooPS2.
- Replace VoodooHDA from Clover Kexts folder (the other folder) with the one NOT in the zip

# After Modded Deploy

- You should have no Internet at this point, the following next steps should resolve that. However, your Brightness, lidsleep, USB, bluetooth should be working
- Using your favourite Kext Installer (Put it on a USB or something to get it on the PC), install (credit @Rehabman's) FAKEPCIID and FAKEPCIID_Broadcomm texts that are included in the ManualKexts Folder
- Then run "Sudo kextcache -i /" from terminal, reboot, then run it again. 
- By this point your wifi should be fixed, and everything should be done

# Post Install Notes

- Your welcome to transfer whatever other kexts you want to S/L/E, personally I leave them in the CLOVER Folder injected.
- Doing upgrade via mac app store is similar, just partitioning hard drive is harder. Apart from that same process essentially, not recommended

# Credits
- Credit Hackintosher.com for basic patches (although @syscl) covered some
- Credit to @syscl (clearly...)
- Credit to @Rehabman
- Credit to @syscl Kexts, and his contributers. ex. Lidwake.kext (although not fully compatible)



# Support

- Your welcome to open any issues on this thread, I personally have little DSDT knowledge so I will do my best to help!


# Thanks for Reading!



