# Arch Linux Installation

This document tracks my personal installation of Arch Linux onto a HP intel core i7 machine. As this is my first instllation of Arch Linux (excluding the archinstall script) I used [How to Install Arch Linux: Step-by-Step Guide](https://www.youtube.com/watch?v=FxeriGuJKTM) resource to aid me through my first install.

## General process and commands of interest

### Partitioning

`lsblk` lists the available drives on the machine. We use this command to determine where we want to install Arch Linux. I used the size field to help identify the drive given that both the boot media and the solid state drive were called sda and sdb respectively.

`fdisk` allows us to set up partitions. There are other options but the tutorial opted for this.

The command to target the storage device of interest:

```bash
fdisk /dev/sda
```

Running this command opens the fdisk utility for sda and allows us to configure the storage media.

- `p` command shows how the storage media is currently partitioned.
- `g` creates an empty partition table.

Running p again would show there is no partitions on the storage device anymore (this is only in memory not and enforced change).

- `n` creates a new partition.
  - I followed the defaults here and specified `+1G` for the Last sector.

We are creating two partitions one for Boot and one for EFI.

> The EFI system partition (also called ESP) is an OS independent partition that acts as the storage place for the UEFI boot loaders, applications and drivers to be launched by the UEFI firmware. It is mandatory for UEFI boot.

We now create another partition for LVM, this used to install Linux.

> Logical Volume Manager (LVM) is a device mapper framework that provides logical volume management for the Linux kernel. LVM is a tool for managing storage space, offering flexibility in resizing and moving volumes.

After the partition is created we used the command `t` to set the partition type of sda3 to 44 which corresponds to Linux LVM.

`w` command writes the changes.

### Formatting partitions

We want to formart our boot partiton as FAT32. We do this is the command `mkfs.fat -F32 /dev/sda1`

**FAT definition**:

> A FAT (File Allocation Table) partition is a file system that uses a table to track the location of files and directories on a storage device. It was the default file system for older versions of Windows and MS-DOS, and is still used in some contexts like USB flash drives and embedded systems.

The second partition sda2 is formatted to ext4 using the following command `mkfs.ext4 /dev/sda2`

**ext4 definition**

> ext4 (fourth extended filesystem) is a journaling file system for Linux

Encrypt sda3 as this is data will be stored. Do this with the following command: `cryptsetup luksFormat /dev/sda3`

To open the partition use the following command: `cryptsetup open --type luks /dev/sda3 [name]`

Now create a physical volume for lvm: `pvcreate /dev/mapper/lvm`

Create volume group: `vgcreate volgroup0 /dev/mapper/lvm`

Create two logical group one for the root fs and the home.

With the logical groups and volume groups created we then format mount the volumes. I formatted the lv_root and lv_home to ext4. I then mount the volume group to /mnt. I mount /dev/sda2 to /mnt/boot, lv_home to /mnt/home,

** Brief explanation of Physical, Group, and Logical volumes**

> In Logical Volume Management (LVM), a physical volume (PV) is a raw disk or partition that LVM uses for storage. A volume group (VG) is a collection of one or more PVs, effectively creating a pool of storage space. A logical volume (LV) is a virtual partition within a VG, offering flexibility in how storage is managed.

** fstab definition **

> The fstab file, short for "file system table," is a configuration file in Linux and Unix-like systems that specifies how file systems should be mounted during boot or at any other time

Use `arch-chroot /mnt` to login into arch linux in a safe manner while at this point of installation.

Can now set password for root used passwd

Create user using `useradd -m -g users -G wheel aden` where -G wheel allows for sudo and added to group users.

Installed using pacamn the following packages:

- base-devel
- dosfstools
- grub
- efibootmgr
- lvm2
- mtools
- vim
- sudo
- openssh
- os-prober
- networkmanager

The install linux, linux-headers and linux-lts (a failsafe if linux kernel fails for any reason). Optionally install linux-firmware.

Now setting up GPU driver. use `lspci` to find GPU. Install `mesa` for intel or amd GPU.

Update hooks in `/etc/mkinitcpio.conf` to inlcude lvm2 and encrypt.

Ran `mkinticpio -p linux`

Update `/etc/default/grub` to include: `cryptdevice=/dev/sda3:volgroup0` in GRUB_CMDLINE_LINUX_DEFAULT

Now moutt sda1 to /boot/EFI

Run grub-install --taregt=x86_64-efi --bootloader-id=grub_uefi --recheck
