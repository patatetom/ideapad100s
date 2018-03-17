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
umount /dev/sdx*
fdisk /dev/sdx <<<g$'\n'n$'\n\n\n\n't$'\n'1$'\n'w
blockdev --rereadpt /dev/sdx
mkfs.vfat -F 32 -n SWAGARCHXX /dev/sdx1
```
*note that **all data on /dev/sdx will be deleted***

- copy data from the SwagArch release to the USB flash drive
```
mount /tmp/swagarch-1803_x86_64.iso /mnt/cdrom
mount /dev/sdx1 /mnt/flash
cp -a /mnt/cdrom/* /mnt/flash
```

- copy the 32-bit bootloader to the USB flash drive
```
cp /tmp/bootia32.efi /mnt/flash/EFI/boot/
umount /mnt/cdrom /mnt/flash
```
*the USB flash drive is now ready*

- disable Secure Boot on the Ideapad
```text
power on the Ideapad,
press F2 key (with Fn key) to access the UEFI firmware,
go to the Configuration tab,
turn off the Secure Boot
and finally press F10 key to save changes and exit
```
