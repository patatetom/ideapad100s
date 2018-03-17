# Ideapad 100s

installation of [SwagArch](https://swagarch.github.io/) on a Lenovo Ideapd 100s


![SwargArch on Ideapad 100s](https://github.com/patatetom/ideapad100s/blob/master/SwagIdeapad.png)



## prerequisites

- a fairly recent and functional GNU/Linux system *(here an ArchLinux with a root account)*
- a USB flash drive with a capacity of at least 2Gb *(here a 16Gb available from /dev/sdx)*
- the [latest release](https://github.com/SwagArch/swagarch-build/releases/latest) of SwagArch *(here 1803)*
- the `bootia32.efi` bootloader available above



## before installation

the Ideapad is delivered with 32-bit UEFI firmware and SwagArch, like many other GNU/Linux distributions, is not « mixed mode » : so it must therefore be slightly modified in order to boot.
