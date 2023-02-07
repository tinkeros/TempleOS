## TempleOS respins

##### <a href="https://github.com/tinkeros/TempleOS/releases/download/v0/TempleOS_USB.img">TempleOS_USB.img</a> - Vanilla TempleOS booted to a RAM disk with the help of a modified kernel and memdisk.
##### <a href="https://github.com/tinkeros/TempleOS/releases/download/v0/TempleOS_vanilla_no_HPET.ISO.C">TempleOS_vanilla_no_HPET.ISO.C</a> - Vanilla TempleOS with HPET disabled (it prevents TempleOS from booting on some machines)

The USB boot version is mainly for testing.  With this you can run TempleOS on some machines which might otherwise not boot it because they do not have legacy drive support or because of HPET issues.  The USB version boots to a RAM disk so nothing you do is saved and your drives are not touched unless you specifically try to mount or install to them.  When it asks you if you want to "Install onto hard drive (y or n)?" Choose n.

If you have IDE drives or SATA in compatability / legacy mode, have a DOS (NOT GPT) partition table and have pre-made/formatted FAT32 partitions (of reasonably small size < 16GB), then maybe you can mount them and possibly do a manual install.  Installation is completely unsupported, the automated installer will defintiely not work as-is in many cases and tryinig to do so is at your own risk!  I've tested this on many of my machines and am able to mount my drives, load/save files, and even rebuild/fix the bootloader/kernel on them if need be.  This might also be useful for recovery purposes by booting via USB, running AutoMountIDE and then fixing your broken distro.

This is not a way to run TempleOS on modern machines.  This does not add USB support to TempleOS.  If you don't see video it is likely you are trying to run it on a computer which is way too new and probably doesn't even have VGA support/VGA BIOS/support for the old VGA registers TempleOS requires.  If it boots, but your keyboard and/or mouse do not work, again you're trying to run it on a computer that is too new.
