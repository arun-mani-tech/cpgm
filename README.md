## Flashing procedure for RV1109 Relfor

##1)Unpacking Rockchip Firmware:

##step:1) Unpacking release_update.img
		`$ img_unpack update.img img`

##step:2) unpacking update.img
		$ cd img
		`$ ./linux/Linux_Pack_Firmware/rockdev/afptool -unpack update.img update`
##step:3) Check the file tree in the update directory
		`$ cd update/`
		`$ tree`
	```	.
		├── Image
		│   ├── boot.img
		│   ├── kernel.img
		│   ├── MiniLoaderAll.bin
		│   ├── misc.img
		│   ├── parameter.txt
		│   ├── recovery.img
		│   ├── resource.img
		│   ├── trust.img
		│   └── uboot.img
		├── package-file
		└── RESERVED
	```
##2)emmc partiton:
	to change the emmc partition by using Image/parameter.txt
	And copy the parameter file to parameter

##3)To create update_new.img
	the current directory is still `update/`, which contains package-file
	`$ ./linux/Linux_Pack_Firmware/rockdev/afptool -pack . Image/update.img`
	`$ ./linux/Linux_Pack_Firmware/rockdev/rkImageMaker -RK1126 Image/MiniLoaderAll.bin
						Image/update.img update_new.img -os_type:androidos`

##4)Flash update_new.img to RV1109
	- Short jumber
	- Wait for rockchip IC in lsusb/dmesg -w
	- Remove jumper
	- `sudo upgrade_tool uf update_new.img`
