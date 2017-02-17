# Qemu

This directory includes the files necessary for building a qemu 
coreboot rom, as well as other files to help with testing it.

## luks.raw

A raw disc image with a single luks encrypted partition, to test the 
cryptomount cmd of grub. Created with the following commands:  
`qemu-img create luks.raw 10M`
`fdisk luks.raw`

within fdisk: 
`o` to create new disk label  
`n` create new partiton, hitting enter to all the prompts  
`w` to write and quit fdisk  

`losetup --offset $((2048*512)) --find luks.raw` this will attach a 
/dev/loop* device to the first partition of *luks.raw*  
`losetup` to check which /dev/loop* device is used for luks.raw  
`cryptsetup luksFormat /dev/loop*`  
`cryptsetup luksOpen /dev/loop* <name>`  
`mkfs.ext4 /dev/loop*` or your preferred filesystem.  
`cryptsetup luksClose <name>`  
`losetup --detach /dev/loop*`  
`qemu -bios coreboot.rom -hda luks.raw`  
