# Changelog

### 9dfb036 Updated README.md

Updated driver download link. Thanks to @manio for helping out.

### 34222c2 Kernel 5.0.0 changes

Added fix from @Herrie82 for kernel version 5.0.0 and above. Documentation updated.

### 06d6476 Kernel 4.20 (missing symbols)

Due to changes to the kernel build system, the rcblob was not picked up in the
linking stage, leading to missing symbols in the rcraid.ko kernel module.
Fixed by changing Makefile destinations and rules.

### b128f38 Added conditional define for SECTOR_SIZE to avoid compile time warning

### c1b10e0 Made platform detection portable (use of "uname -m"), updated README.md, added CHANGELOG.md

Replaced `uname -i` to `uname -m` in Makefile for platform detection, since
`uname -i` is not portable across Linux flavors. Also added CHANGELOG.md and
updated README.md. 

### ed4f557 Changed shell from /bin/sh to /bin/bash in all shell scripts

In legacy Linux versions, `/bin/sh` was a link to `/bin/bash`. Nowadays the
two shells differ. The shell scripts from AMD are in `bash` syntax and
therefore the change was necessary. 

### 219a078 Added patch for linux kernel version >= 4.15 Incorporates changes from `init_timer()` to `timer_setup()`

With kernel versions starting from 4.15, the interface for using timers was
changed.

### 97c3f18 Added disclaimer, description and installation instructions

### 7dd9d09 Initial commit
