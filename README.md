## Flashing procedure for RV1109 Relfor

### Unpacking Rockchip Firmware:

	1. Unpacking release_update.img
		$ img_unpack update.img img

### unpacking update.img
		$ cd img
		$ ./linux/Linux_Pack_Firmware/rockdev/afptool -unpack update.img update
### Check the file tree in the update directory
		$ cd update/
		$ tree

		.
		├── Image
		│   ├── boot.img
		│   ├── MiniLoaderAll.bin
		│   ├── misc.img
		│   ├── oem.img
		│   ├── parameter.txt
		│   ├── recovery.img
		│   ├── rootfs.img
		│   ├── uboot.img
		│   └── userdata.img
		├── package-file
		└── parameter

	
### emmc partiton:
	to change the emmc partition by using Image/parameter.txt.
	And copy the parameter file to parameter.

### To create update_new.img
	the current directory is still update/, which contains package-file.
	$ ./linux/Linux_Pack_Firmware/rockdev/afptool -pack . Image/update.img
	$ ./linux/Linux_Pack_Firmware/rockdev/rkImageMaker -RK1126 Image/MiniLoaderAll.bin
						Image/update.img update_new.img -os_type:androidos

### Flash update_new.img to RV1109
	- Short jumber
	- Wait for rockchip IC in lsusb/dmesg -w
	- Remove jumper
	- sudo upgrade_tool uf update_new.img
