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
the `--offset` option takes a value in bytes. 2048 is the start sector, 512 is the sector size in bytes.
running `fdisk luks.raw` again and running `p` will show you sector size and start sector.
`losetup` to check which /dev/loop* device is used for luks.raw  
`cryptsetup luksFormat /dev/loop*`  
`cryptsetup luksOpen /dev/loop* <name>`  
`mkfs.ext4 /dev/mapper/<name>` or your preferred filesystem.  
`cryptsetup luksClose <name>`  
`losetup --detach /dev/loop*`  
`qemu -bios coreboot.rom -hda luks.raw`  
