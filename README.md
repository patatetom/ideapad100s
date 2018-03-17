# Ideapad 100s

installation of [SwagArch](https://swagarch.github.io/) on a Lenovo Ideapd 100s


![SwargArch on Ideapad 100s](https://github.com/patatetom/ideapad100s/blob/master/SwagIdeapad.png)



## prerequisites

- a fairly recent and functional GNU/Linux system *(here an ArchLinux)*
- a USB flash drive with a capacity of at least 2Gb *(here a 16Gb available from /dev/sdx)*
- the [latest release](https://github.com/SwagArch/swagarch-build/releases/latest) of SwagArch *(here 18.03)*
- the [bootia32.efi](https://github.com/patatetom/ideapad100s/raw/master/bootia32.efi) bootloader available above



## before installation

the Ideapad is delivered with 32-bit UEFI firmware and SwagArch, like many other GNU/Linux distributions, is not « mixed mode » : so it must therefore be slightly modified in order to boot.

in a terminal, on the GNU/Linux system with the USB flash drive plugged :

- prepare the USB flash drive
```bash
sudo -i
umount /dev/sdx*
fdisk /dev/sdx <<<g$'\n'n$'\n\n\n\n't$'\n'1$'\n'w
blockdev --rereadpt /dev/sdx
mkfs.vfat -F 32 -n SWAGARCHXX /dev/sdx1
```
*:warning: note that all data on /dev/sdx will be deleted*

- copy data from the SwagArch release to the USB flash drive
```bash
mount /tmp/swagarch-1803_x86_64.iso /mnt/cdrom
mount /dev/sdx1 /mnt/flash
cp -a /mnt/cdrom/* /mnt/flash
```

- copy the 32-bit bootloader to the USB flash drive
```bash
cp /tmp/bootia32.efi /mnt/flash/EFI/boot/
umount /mnt/cdrom /mnt/flash
```
**the USB flash drive is now ready**

on the Ideapad :

- disable Secure Boot
```text
power on the computer,
press [F2] key (use [Fn] key) to enter in the UEFI firmware,
go to the Configuration tab,
turn off the Secure Boot
and finally press [F10] key to save change and exit
```



## installation

on the Ideapad with the USB flash drive plugged :

- access the boot menu
```text
power off/on the computer (reboot),
press [F12] key (use [Fn] key) to show the boot menu,
```

- in the boot menu, boot live SwagArch (step 1/2)
```
select entry EFI USB Device (USB Mass Storage Driver)
and presse [Enter] key
```

- in the Grub console, boot live SwagArch (step 2/2)
```bash
linux /arch/boot/x86_64/vmlinux archisobasedir=arch archisolabel=SWAGARCHXX
initrd /arch/boot/intel_ucode.img /arch/boot/x86_64/archiso.img
boot
```
*note that the keyboard is defined as [QWERTY] and that the [Tab] key is available in the Grub console*

**after a few seconds, you should be in SwagArch, ready to install it on your internal device, using the installer provided for this purpose.**

> if there is enough free space (~30Gb) on the USB flash disk, the previous system can be saved before the installation
> ```
> sudo -i
> df -h /run/archiso/bootmnt/
> mkdir /run/archiso/bootmnt/backup/
> gzip < /dev/mmcblk1 | split -d -b 1G - /run/archiso/bootmnt/backup/Ideapad-
> sync
> ```



## after installation

### wifi

### sound
