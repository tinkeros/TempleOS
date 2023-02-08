## TempleOS respins

##### <a href="https://github.com/tinkeros/TempleOS/releases/download/v0/TempleOS_USB.img">TempleOS_USB.img</a> - Vanilla TempleOS booted to a RAM disk with the help of a modified kernel and memdisk.
##### <a href="https://github.com/tinkeros/TempleOS/releases/download/v0/TempleOS_vanilla_no_HPET.ISO.C">TempleOS_vanilla_no_HPET.ISO.C</a> - Vanilla TempleOS with HPET disabled (it prevents TempleOS from booting on some machines)

The USB boot version is mainly for testing.  With this you can run TempleOS on some machines which might otherwise not boot it because they do not have legacy drive support or because of HPET issues.  The USB version boots to a RAM disk so nothing you do is saved and your drives are not touched unless you specifically try to mount or install to them.  When it asks you if you want to "Install onto hard drive (y or n)?" Choose n.

If you have IDE drives or SATA in compatibility / legacy mode, have a DOS (NOT GPT) partition table have pre-made/formatted FAT32 partitions (of reasonably small size < 16GB) and your system supports CSM or legacy boot (this does not boot with UEFI or secure boot), then maybe you can mount them and possibly do a manual install.  Installation is completely unsupported, the automated installer will defintiely not work as-is in many cases and trying to do so is at your own risk!  I've tested this on many of my machines and am able to mount my drives, load/save files, and even rebuild/fix the bootloader/kernel on them if need be.  This might also be useful for recovery purposes by booting via USB, running MountIDEAuto and then fixing your broken distro.

This runs TempleOS baremetal, ring-0, not in a VM.  This is not a way to install/run TempleOS on modern machines (it adds no additional hardware support or other code to TempleOS). That being said booting from USB to RAM does eliminate the need for any physical disk drives that TempleOS supports so this may allow running TempleOS on some machines that normally could not run it due to lacking IDE/legacy drive support.  This does not add USB support to TempleOS (memdisk just provides enough support to load the kernel and ramdisk into memory from USB, then TempleOS takes over which has no USB support).  If you don't see video it is likely you are trying to run it on a computer which is way too new and probably doesn't even have VGA support/VGA BIOS/support for the old VGA registers TempleOS requires  (TinkeroOS/Zeal might work if you want to try them instead).  If it boots, but your keyboard and/or mouse do not work, again you're trying to run it on a computer that is too new and lacks PS/2 keyboard/mouse emulation.

These versions should be fully compatible with older 3rd party software written by Alec which use the VGA registers for graphics stuff instead of a linear framebuffer obtained from VBE (as is the case with TinkerOS/Zeal).

FreeDOS and older versions of clonezilla/ttylinux are provided to help with formatting/partitioning drives TempleOS cannot handle and also for finding IO ports TempleOS needs to know to install on some machines.  Sometimes the drive contents/size/existing partitioning or the probing TempleOS does prevents it from being installed by the normal installer.  I have found many machines where the normal installer fails, but it is possible to make a completely working TempleOS install if you manually partition/format the drives and manually enter the IO ports for them.  IDE support has been removed from most linux kernels, but the version of clonezilla included on this has IDE support.  You can boot it and use it to manually partition/format disks and/or run lspci -vv to find IO ports with it from the command line.

The USB version extracts <a href="https://templeos.org/Downloads/TempleOS.ISO">TempleOS.ISO</a> (md5 hash: 2facf5d7cfa08de4c47aede4a64cfb44) onto the ram disk.  TempleOS.ISO on the thumb drive is simply a redsea ISO that contains the special ramdisk loader kernel and Terry's original ISO file prepended with: BASESTARTBASESTART and appended with ISOENDISOENDISOEND (these are what the kernel uses to find it in memory).

If you want to verify the USB installer extracts the original TempleOS:

### If you're paranoid and want to know what ISO is actually being extracted to the RAM disk:

#### Get the hash of the Terry's original (assuming Linux command line):
```
wget https://templeos.org/Downloads/TempleOS.ISO
md5sum TempleOS.ISO
2facf5d7cfa08de4c47aede4a64cfb44 TempleOS.ISO
```
#### Extracting the original ISO from that which is on the USB image (assuming Linux command line and TempleOS competency):
- Extract TempleOS.ISO from the USB disk and copy it inside TempleOS.
- Rename it with an ".ISO.C" extension to make it contiguous (so it can be mounted), ex: `Move("C:/TempleOS.ISO","C:/tmp.ISO.C");`
- Mount it ex: `MountFile("C:/tmp.ISO.C");`
- Copy off the embedded ISO ex: `Copy("M:/TempleOS.ISO.C","C:/");` The resulting ISO is 17350693 in side, 37 bytes larger than the 17350656 original (17350693=17350656 original + 18 bytes of "BASESTARTBASESTART" + 18 bytes of "ISOENDISOENDISOEND" + 1 null byte.
- You can verify the hash of this equals that of above by stripping off the prefix and suffix as follows:
`cat /mnt/qemu_disk/TempleOS.ISO.C | sed 's/.*BASESTARTBASESTART//' | sed 's/ISOENDISOENDISO.*//' | md5sum` which if you have done everything write will return the same hash as above.
- Congratulations!  If you've got this far and understand everything along the way you probably can replace the original distro with your own distro and make a USB boot version of your own distro by simply reversing these steps and re-using my existing loader kernel.  If you try this, know that your ISO must be < 64MB in size.




