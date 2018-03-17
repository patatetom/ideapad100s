# Ideapad 100s

installation of [SwagArch](https://swagarch.github.io/) on a Lenovo Ideapd 100s


![SwargArch on Ideapad 100s](https://github.com/patatetom/ideapad100s/blob/master/SwagIdeapad.png)



## prerequisites

- a fairly recent and functional GNU/Linux system *(here an ArchLinux with a root account)*
- a USB flash drive with a capacity of at least 2Gb *(here a 16Gb available from /dev/sdx)*
- the [latest release](https://github.com/SwagArch/swagarch-build/releases/latest) of SwagArch *(here 18.03)*
- the [bootia32.efi](https://github.com/patatetom/ideapad100s/raw/master/bootia32.efi) bootloader available above



## before installation

the Ideapad is delivered with 32-bit UEFI firmware and SwagArch, like many other GNU/Linux distributions, is not « mixed mode » : so it must therefore be slightly modified in order to boot.

- prepare the USB flash drive
```
fdisk /dev/sdx <<<g$'\n'n$'\n\n\n\n't$'\n'1$'\n'w
blockdev --rereadpt /dev/sdx
mkfs.vfat -F 32 -n SWAGARCHXX /dev/sdx1
```
*note that **all data on /dev/sdx will be deleted***

- copy all data from the SwagArch release to the USB flash drive
```
```
