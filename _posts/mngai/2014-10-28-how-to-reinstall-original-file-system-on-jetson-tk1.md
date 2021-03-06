---
layout: post
title: "How to Reinstall the Original File System on Jetson TK1"
description: "What to do in case you broke your Jetson TK1"
category: jetson
tags: [tutorial, jetson, board, repair, reinstall, factory, settings]
author: mngai
---

In case something goes awry while programming the Jetson TK1, you may need to repair the file system 
on the Jetson TK1. Ramy and I realized we messed something up while trying to follow [this guide](https://devtalk.nvidia.com/default/topic/766276/guide-playstation-eye-on-jetson-tk1/)
to install the PS3 Eye on the board. The realization came when we had internet access (via ethernet) but
could not connect to the internet or even ping an IP address.

To fix the file system, we followed [these steps](https://cyclicredundancy.wordpress.com/category/linux/)
which essentially is paraphrasing of the steps [here](https://developer.nvidia.com/sites/default/files/akamai/mobile/files/L4T/l4t_quick_start_guide.txt)
from the [Linux for Tegra](https://developer.nvidia.com/linux-tegra-rel-19) website. I will paraphrase the
paraphrasing here for ease of access later.

### Materials Needed
1. Linux host PC. There is one in the MicroP's lab available for Jetson. It is the one with non-
standard tower. The username is big-Jetson (if I recall correctly). Contact me, Ramy, Da Eun, or Spjut
for the password. 
2. micro USB to USB cable (should be included with the Jetson TK1 kit) 

### Steps

1. Prepare the diretory on the host PC

        mkdir tk1_reflash
		cd tk1_reflash

2. Get Jetson TK1 board support package aka BSP (called Tegra124_Linux_R19.2.0_armhf.tbz2)

		wget https://developer.nvidia.com/sites/default/files/akamai/mobile/files/L4T/Tegra124_Linux_R19.2.0_armhf.tbz2

3. Get sample file system file (called Tegra_Linux_Sample-Root-Filesystem_R19.2.0_armhf.tbz2)

		wget https://developer.nvidia.com/sites/default/files/akamai/mobile/files/L4T/Tegra_Linux_Sample-Root-Filesystem_R19.2.0_armhf.tbz2

4. Extract the BSP tarball 

		sudo tar xpf Tegra124_Linux_R19.2.0_armhf.tbz2

5. Extract the FS tarball into a particular sub directory

		sudo tar xpf Tegra124_Linux_R19.2.0_armhf.tbz2

6. Extract the FS tarball into a particular sub directory

		cd Linux_for_Tegra/rootfs
		sudo tar xpf ../../Tegra_Linux_Sample-Root-Filesystem_R19.2.0_armhf.tbz2

7. Apply binaries

		cd ..
		sudo ./apply_binaries.sh
		The following output will be seen:

8. Expect to see this

		Using rootfs directory of: /home/you/tk1_reflash/Linux_for_Tegra/rootfs
		Extracting the NVIDIA user space components to /home/you/tk1_reflash/Linux_for_Tegra/rootfs
		Extracting the NVIDIA gst test applications to /home/you/tk1_reflash/Linux_for_Tegra/rootfs
		Extracting the configuration files for the supplied root filesystem to /home/you/tk1_reflash/Linux_for_Tegra/rootfs
		Creating a symbolic link nvgstplayer pointing to nvgstplayer-0.10
		Adding symlink libcuda.so --> libcuda.so.1.1
		Extracting the firmwares and kernel modules to /home/you/tk1_reflash/Linux_for_Tegra/rootfs
		Installing the board *.dtb files into /home/you/tk1_reflash/Linux_for_Tegra/rootfs/boot
		Success!

9. Write to eMMC over USB. Hold "RECOVERY" buttom on board and press "RESET" button once on board. 
This puts the board in recovery mode. Connect host computer to target board through USB 

10. Verify board is connected by running

		lsusb | grep -i nvidia

11. You should see the following

		Bus 002 Device 004: ID 0955:7140 NVidia Corp.

12. Run the following.

		sudo ./flash.sh -S 14580MiB jetson-tk1 mmcblk0p1

	But if that doesn't work run

		sudo ./flash.sh -S 8GiB jetson-tk1 mmcblk0p1

13. This should print something similar to the following. It will take a while to run.

		copying dtbfile(/home/foobar/l4t/Linux_for_Tegra/kernel/dtb/tegra124-pm375.dtb) to tegra124-pm375.dtb... done.
		Making system.img... 
		 populating rootfs from /home/foobar/l4t/Linux_for_Tegra/rootfs... done.
		 Sync'ing... done.
		System.img built successfully. 
		copying bctfile(/home/foobar/l4t/Linux_for_Tegra/bootloader/ardbeg/BCT/PM375_Hynix_2GB_H5TC4G63AFR_RDA_924MHz.cfg) to bct.cfg... done.
		copying cfgfile(/home/foobar/l4t/Linux_for_Tegra/bootloader/ardbeg/cfg/gnu_linux_fastboot_emmc_full.cfg) to flash.cfg... done.
		creating gpt(ppt.img)... 
		*** GPT Parameters ***
		device size -------------- 15766388736
		bootpart size ------------ 8388608
		userpart size ------------ 15758000128
		Erase Block Size --------- 2097152
		sector size -------------- 4096
		Partition Config file ---- flash.cfg
		Visible partition flag --- GP1
		Primary GPT output ------- PPT->ppt.img
		Secondary GPT output ----- GPT->gpt.img
		Target device name ------- none
		*** PARTITION LAYOUT(16 partitions) ***
		[ BCT] BH 0 16383 8.0MiB 
		[ PPT] UH 0 4095 2.0MiB ppt.img
		[ PT] UH 4096 8191 2.0MiB 
		[ EBT] UH 8192 16383 4.0MiB fastboot.bin
		[ LNX] UH 16384 32767 8.0MiB boot.img
		[ SOS] UH 32768 45055 6.0MiB 
		[ GP1] UH 45056 49151 2.0MiB 
		[ APP] UV 49152 16826367 8192.0MiB system.img
		[ DTB] UV 16826368 16834559 4.0MiB tegra124-pm375.dtb
		[ EFI] UV 16834560 16965631 64.0MiB 
		[ USP] UV 16965632 16973823 4.0MiB 
		[ TP1] UV 16973824 16982015 4.0MiB 
		[ TP2] UV 16982016 16990207 4.0MiB 
		[ TP3] UV 16990208 16998399 4.0MiB 
		[ UDA] UV 16998400 30773247 6726.0MiB 
		[ GPT] UH 30773248 30777343 2.0MiB gpt.img
		done.
		copying bootloader(/home/foobar/l4t/Linux_for_Tegra/bootloader/ardbeg/fastboot.bin)... done.
		Bootloader(/home/foobar/l4t/Linux_for_Tegra/bootloader/ardbeg/fastboot.bin) used as flasher.
		Existing flash application(/home/foobar/l4t/Linux_for_Tegra/bootloader/nvflash) reused.
		making zero initrd... 
		done.
		Making Boot image... done
		*** Flashing target device started. ***
		./nvflash --bct bct.cfg --setbct --configfile flash.cfg --create --bl fastboot.bin --odmdata 0x6009C000 --go
		Nvflash 4.13.0000 started
		chip uid from BR is: 0x340010017408c1431c00000016018080
		rcm version 0X400001
		Skipping BoardID read at miniloader level
		System Information:
		 chip name: unknown
		 chip id: 0x40 major: 1 minor: 1
		 chip sku: 0x81
		 chip uid: 0x000000017408c1431c00000016018080
		 macrovision: disabled
		 hdcp: enabled
		 jtag: enabled
		 sbk burned: false
		 board id: 0
		 warranty fuse: 0
		 dk burned: true
		 boot device: emmc
		 operating mode: 3
		 device config strap: 0
		 device config fuse: 0
		 sdram config strap: 3
		RCM communication completed
		BCT sent successfully
		odm data: 0x6009c000
		downloading bootloader -- load address: 0x80108000 entry point: 0x80108000
		sending file: fastboot.bin
		- 900492/900492 bytes sent
		fastboot.bin sent successfully
		waiting for bootloader to initialize
		bootloader downloaded successfully
		ML execution and Cpu Handover took 1 Secs
		Partition backup took 0 Secs
		setting device: 2 3
		deleting device partitions
		creating partition: BCT
		creating partition: PPT
		creating partition: PT
		creating partition: EBT
		creating partition: LNX
		creating partition: SOS
		creating partition: GP1
		creating partition: APP
		creating partition: DTB
		creating partition: EFI
		creating partition: USP
		creating partition: TP1
		creating partition: TP2
		creating partition: TP3
		creating partition: UDA
		creating partition: GPT
		sending file: ppt.img
		\ 2097152/2097152 bytes sent
		ppt.img sent successfully
		padded 4 bytes to bootloader
		sending file: fastboot.bin
		- 900496/900496 bytes sent
		fastboot.bin sent successfully
		sending file: boot.img
		\ 5912576/5912576 bytes sent
		boot.img sent successfully
		sending file: system.img
		/ 8589934592/8589934592 bytes sent
		system.img sent successfully
		sending file: tegra124-pm375.dtb
		- 34723/34723 bytes sent
		tegra124-pm375.dtb sent successfully
		sending file: gpt.img
		\ 2097152/2097152 bytes sent
		gpt.img sent successfully
		Create, format and download took 1515 Secs
		Time taken for flashing 1516 Secs
		*** The target ardbeg has been flashed successfully. ***
		Reset the board to boot from internal eMMC.
		~/l4t/Linux_for_Tegra >

### You're done!
See [this link](https://cyclicredundancy.wordpress.com/category/linux/) for some
post-install housekeeping.
