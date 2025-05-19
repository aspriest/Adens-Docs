# Network Drives

## Mounting

I have a Synology NAS which is maintained by another family member that I wanted to mount on my Arch Linux Desktop machine. 

## Server Message Blok (SMB)

SMB is a client/server protocol that governs access to files and whole directories as well as other network resources like printers, routers or interfaces open to the network. The software project Samba offers a solution that enables the use of SMB in Linux and Unix distributions, thereby allowing cross-platform communication via SMB.

SMB protocol enables the client to communicate with other participants in the same network, allowing it to access files or services open to it. For this to work both the server and client must have implemented the network protocol and receive and process the client request using an SMB server application. Prior to this, both parties must first establish a connection, in IP networks, SMB uses TCP.

*source: https://www.ionos.com/digitalguide/server/know-how/server-message-block-smb/*

## FSTAB

Fstab the operating systems's **file system table**. In the earlier days on linux you had to manually mount external drives, unlike today where drives can be auto discovered. The only alternative was to to tell your machine to mount a specific device anytime it was plugged in. This is where fstab comes in. Fstab is configured to look for specific file systems and mount them automatically in a desired way.

The structure of the fstab file is:

<< File system identifier >> << mount point >> << file system type >> << options >> << dumping >> << passing >>

**common options**

- auto/noauto: Specify whether he partition should be automatically mounted on boot.
- exec/noexec: Specifies whether the partition can execute binaries.
- ro/rw: read-only and read-write respectively.
- sync/async: Sets if writing occurs immediately or over some length of time. Is useful depending ont he type of driver being mounted.

- nouser/user: his allows the user o have mounting and unmounting privileges.

The last two options can be set with a binary 0 or 1. Dumping is an outdated way of backup for cases when the system goes down. Passing tells the system the order in which to do a file system check (fsck)

*source: https://www.howtogeek.com/38125/htg-explains-what-is-the-linux-fstab-and-how-does-it-work/*

## Mounting Network Drive

1. To mount the network drive I needed to ensure I had cifs-utils installed to allow for mounting of SMB/CIFS shares. 

```bash
sudo pacman -S cifs-utils
```
2. Create a .smbcredentials file with 700 permissions. The file should have the following:

```text
username={{username}}
password={{password}}
```

3. Add the following to my fstab file:

```text
//xxx.xxx.x.x/path/to/share /path/to/mount cifs vers=2.0,credentials=/home/.smbcredentials,auto,rw 0 0
```
*Ideally we I would like to user vers=3.0 but am getting 
mount error (95) operation not supported. I believe this is due to the NAS using an older protocol version. I have checked my current cifs-utils and mount.cifs versions and they are up to date.*

4. Run to mount the network drive without rebooting, and reload the daemon.

```bash
sudo mount -a
systemctl daemon-reload 
```