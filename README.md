## TempleOS respins

##### <a href="https://github.com/tinkeros/TempleOS/releases/download/v0/TempleOS_USB.img">TempleOS_USB.img</a> - Vanilla TempleOS booted to a RAM disk with the help of a modified kernel and memdisk.
##### <a href="https://github.com/tinkeros/TempleOS/releases/download/v0/TempleOS_vanilla_no_HPET.ISO.C">TempleOS_vanilla_no_HPET.ISO.C</a> - Vanilla TempleOS with HPET disabled (it prevents TempleOS from booting on some machines)

The USB boot version is mainly for testing.  With this you can run TempleOS on some machines which might otherwise not boot it because they do not have legacy drive support or because of HPET issues.

If you have IDE drives or SATA in compatability / legacy mode, have a DOS (NOT GPT) partition table and have pre-made FAT32 partitions (of reasonably small size < 16GB), then maybe you can mount them and possibly do a manual install.  Installation is completely unsupported, the automated installer will defintiely not work as-is in many cases and tryinig to do so is at your own risk!

This might also be useful for recovery purposes by booting via USB, running AutoMountIDE and then fixing your broken distro.
