# rcraid-patches

Inofficial Patches for AMD RAID linux kernel modules (rcraid.ko)

## License and Disclaimer

This is a third-party patch, it is _not from AMD_. AMD does not take any
responsibility for this patch. Read also the contents of the file `LICENSE` for
permissions and liability.

## Description

These patches bundle several fixes to the rcraid kernel module source code in
order to make it compile under newer kernel versions than those officially
supported in 2017 by AMD. It has been tested with Ubuntu 18.04, 18.10 and
19.04, but should run on other Linux flavors as well.

For a complete description of fixes, see file
[CHANGELOG.md](https://github.com/martinkarlweber/rcraid-patches/blob/master/CHANGELOG.md).


## Patching instructions

Applying the patches is done by hand and cumbersome. A more convenient way may
be to use the [rcraid-dkms package from Thomas Karl Pietrowski
(@thopiekar)](https://github.com/thopiekar/rcraid-dkms). If you still want to
use this package, follow these instructions:

First download the AMD Linux RAID driver from the [official AMD Raid driver
page](https://www.amd.com/en/support/downloads/previous-drivers.html/chipsets/am4/x370.html). 
Look for the "Linux x86 64-bit driver" section and download the "AMD Raid Driver" 
in the "Crimson ReLive Edition 17.2.1", released 2017-03-27. Download and save 
the file. (You need to accept the license.) Go to your download folder and unzip the
downloaded file,

`unzip raid_linux_driver_8_01_00_039_public.zip`

Download the file `rcraid.patch` from this repository and put it in the same
folder you saved the above zip file in. Then issue

`patch -p1 < rcraid.patch`

The output looks like:

      patching file driver_sdk/install
      patching file driver_sdk/src/Makefile
      patching file driver_sdk/src/common_shell
      patching file driver_sdk/src/install_rh
      patching file driver_sdk/src/install_suse
      patching file driver_sdk/src/rc_init.c
      patching file driver_sdk/src/rc_mem_ops.c
      patching file driver_sdk/src/rc_msg.c
      patching file driver_sdk/src/uninstall_rh
      patching file driver_sdk/src/uninstall_suse
      patching file driver_sdk/uninstall

Congratulations! You are done with patching. 

## Quick install instructions for Ubuntu 18.04

[Download the latest Ubuntu 18.04
image](https://www.ubuntu.com/download/desktop), install it on a USB stick and
boot it in UEFI mode (turn of CSM module in BIOS). After booting, download
the official [AMD RAID driver](https://www.amd.com/en/support/downloads/previous-drivers.html/chipsets/am4/x370.html).
Then open a shell and follow these instructions:

      cd Downloads/
      unzip raid_linux_driver_8_01_00_039_public.zip
      sudo apt install git
      git clone https://github.com/martinkarlweber/rcraid-patches.git
      mv rcraid-patches/rcraid.patch .
      rm -rf rcraid-patches/
      patch -p1 < rcraid.patch
      cd driver_sdk/
      sudo apt install build-essential
      sudo /bin/bash ./install
      sudo rmmod ahci libahci
      sudo modprobe rcraid
      dmesg | less

If everything goes well, you will see an output similar to

      rcraid: loading out-of-tree module taints kernel.
      rcraid: module license 'Proprietary' taints kernel.
      Disabling lock debugging due to kernel taint
      rcraid: module verification failed: signature and/or required key missing - tainting kernel
      scsi host0: AMD, Inc. AMD-RAID
      scsi 0:0:0:0: Direct-Access     AMD-RAID Array 01         8.1  PQ: 0 ANSI: 5
      scsi 0:0:24:0: Processor         AMD-RAID Configuration    V1.2 PQ: 0 ANSI: 5
      scsi 0:1:0:0: CD-ROM            HL-DT-ST DVDRAM GH22NS50  TN03 PQ: 0 ANSI: 0
      sd 0:0:0:0: Attached scsi generic sg1 type 0
      sd 0:0:0:0: [sdb] 3905925120 512-byte logical blocks: (2.00 TB/1.82 TiB)
      sd 0:0:0:0: [sdb] Write Protect is off
      sd 0:0:0:0: [sdb] Mode Sense: 00 06 00 00
      sd 0:0:0:0: [sdb] Write cache: disabled, read cache: enabled, doesn't support DPO or FUA
      scsi 0:0:24:0: Attached scsi generic sg2 type 3
      sr 0:1:0:0: [sr0] scsi-1 drive
      cdrom: Uniform CD-ROM driver Revision: 3.20
      sr 0:1:0:0: Attached scsi CD-ROM sr0
      sr 0:1:0:0: Attached scsi generic sg3 type 5
       sdb: sdb1 sdb2 sdb3
      sd 0:0:0:0: [sdb] Attached SCSI disk

