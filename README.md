# libre-coreboot-builds -- WIP, do not use
Builds for the coreboot systems I have using no non-free options. I 
will provide both the source files (build *config* file, *grub.cfg*, 
etc) and releases of built roms.

## TODO

* memtest86+ through grub for all systems with enough flash space.
 * only textmode grub? launch memtest86+ in textmode from graphical 
grub?
 * launch secondary grub img from memtest menuentry in textmode?
  * chainloader or multiboot? force textmode on second grub?
* linux+busybox recovery OS in flash for x200 (8&16MB only?)
* separate builds for discrete gpu support?
* refine general *grub.cfg*. Credit to libreboot for original.
 * eg: return values on cryptomount, to not continue if fail?

## Discrete GPUs

Generally, your computer will need to run a proprietary VBIOS located on your external GPU to initialize on startup, even for use with textmode.  
Coreboot has native graphics initialization for some integrated GPUs (all the intel systems in this repository) which means you don't need the 
VBIOS for those.

At the moment, using an external GPU as your primary GPU will only give output in coreboot payload's like grub if you allow coreboot to run it's 
proprietary VBIOS, and this may not even work. However both the libre nouveau (for nvidia) and radeon (for AMD Radeon) drivers are able to setup 
external GPUs for Linux without running a VBIOS in coreboot. This will mean you have no display in an intermediary environment like grub or seabios?

The other option is to use the integrated GPU with native init as your primary display, and "soft-boot" the external GPU from within GNU+Linux. Using 
PRIME, you can have all programs by default rendering on the dedicated display, and run specific programs that need it on the more powerful external. 
This may also save power? This is only anecdotal, but in my experience Nouveau never crashes/freezes when only used through PRIME.
