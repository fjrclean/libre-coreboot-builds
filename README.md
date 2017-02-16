# libre-coreboot-builds -- WIP, do not use
Builds for the coreboot systems I have using no non-free options. I 
will provide both the source files (build *config* file, *grub.cfg*, 
etc) and releases of built roms.

## TODO

* memtest86+ through grub for all systems with enough flash space.
 * only textmode grub? launch memtest86+ in textmode from graphical 
grub?
* linux+busybox recovery OS in flash for x200 (8&16MB only?)
* separate builds for discrete gpu support?
* refine general *grub.cfg*. Credit to libreboot for original.
 * eg: return values on cryptomount, to not continue if fail?
