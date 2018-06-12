# rcraid
Inofficial Patches for AMD RAID linux kernel modules (rcraid.ko)

## License and Disclaimer

This is a third-party patch, it is _not from AMD_. AMD does not take any
responsibility for this patch. Read also the contents of the file `LICENSE` for
permissions and liability.

## Description

This patch incorporates the changes from `init_timer()` to `timer_setup()`
which are necessary in Linux kernel starting from version 4.15. Since it tests
for the kernel version, it should also run on kernels with versions below
4.15. The patch has been successfully tested on Ubuntu 18.04.

## Patching instructions

First download the AMD Linux RAID driver from the [official AMD Raid driver
page](https://support.amd.com/de-de/download/chipset?os=Linux+x86_64). (You
need to accept the license.) Go to your download folder and unzip the
downloaded file,

`unzip raid_linux_driver_8_01_00_039_public.zip`

Download the file `rcraid.patch` from this repository and put it in the same
folder you saved the above zip file in. Then issue

`patch -p0 < rcraid.patch`

If the output looks like 

    patching file driver_sdk/src/rc_init.c
    patching file driver_sdk/src/rc_mem_ops.c
    patching file driver_sdk/src/rc_msg.c

Congratulations! You are done. Proceed with the installation as usual.

## Installing and using patched driver

For a complete set of instructions on how to install and use the AMD RAID
Linux driver, have a look at [How to dual boot Windows and Ubuntu on AMD RAID](https://www.kwikr.de//Howto_Windows_Ubuntu_AMD-RAID.html).
